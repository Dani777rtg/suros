# SURÓS / PRORED: ingeniería inversa

Sistema web de gestión de información para clínicas y hospitales (Colombia), de SoftProject. Instancia observada: PRORED (red de IPS con sedes en Caquetá, Cauca, Nariño, Risaralda, Quindío, Huila, Tolima, Santander, entre otras). Fecha de observación: 2026-10-14.

**Método:** se observó la aplicación en producción con un usuario SUPER ADMINISTRADOR, solo en modo lectura. Cada pantalla del menú se cargó y se extrajo su estructura: campos, valores de listas, botones, grillas y ventanas emergentes, incluidas las ocultas (cada una revela un subflujo). No se creó, guardó ni borró nada, no se abrió ningún paciente y no se copiaron datos personales.

## Arquitectura observada

- ASP.NET WebForms con Ext.NET (Ext JS). Un "shell" (`/SUROS/Inicio.aspx`) tiene un árbol de módulos, y cada opción abre una pestaña con un iframe.
- Sub-aplicaciones por ruta: `/SUROS` (núcleo y configuración), `/SUROSHistoriaClinica` (agenda, historia clínica, informes), `/SUROSFacturacion`, `/SUROSAlmacen`, `/SUROSPaginaWeb` (CMS), `/SUROSTurnero` (atención al usuario), `/SurosTickets` (soporte). El punto de venta vive en otro dominio (`puntoventa.suros.co`).
- El menú depende del rol (tabla de páginas → roles → usuarios). Historia clínica carga un árbol distinto por área o especialidad (`ListaArbol(id)`).
- Componentes globales en todas las páginas: sesión finalizada, cambio obligatorio de contraseña, cambio de rol, selección de sede, notificación médica por rol o especialidad, chat clínico y mensajería interna, videollamada, soporte, notificaciones.

## Módulos

| # | Documento | Contenido | Pantallas |
|---|---|---|---|
| 1 | [Citas médicas](modulos/01-citas-medicas.md) | Agenda médica y franjas (BOT App/Web, demanda inducida), cita unificada, activación, autorizaciones, bitácora de llamadas, turnos (procedimientos, rayos X, laboratorio, urgencias) | 13 |
| 2 | [Configuración, seguridad y pacientes](modulos/02-configuracion-seguridad-pacientes.md) | Funcionarios, usuarios, roles, páginas, entidad, especialidades, laboratorio, SISPRO, empresas, subplanes, unificación de historias, diseñador de consentimientos, mi cuenta, pacientes | 21 |
| 3 | [Facturación](modulos/03-facturacion.md) | Facturas (automática, manual, global), RIPS, caja, homologadores, notas crédito y débito, contratación con EPS, parámetros, facturación electrónica DIAN | 19 |
| 4 | [Informes y catálogos](modulos/04-informes-catalogos.md) | Informes por especialidad, remisiones, citas; plantillas de medicamentos e insumos, agendas de consultas terminadas y hospitalización, atención al usuario, tickets, punto de venta | 16 |
| 5 | [Almacén y farmacia](modulos/05-almacen-farmacia.md) | Catálogos, compras (plan, solicitud, orden, pedido interno, despacho), inventarios, lotes y vencimientos, bodegas y almacenes, terceros, farmacia, enfermería, configuración, CMS | 32 |
| 6 | [Historia clínica](modulos/06-historia-clinica.md) | Urgencias (triage, historia, observación, hospitalización, cirugía, entrega de turno), consulta general y especializada, odontología, apoyo terapéutico, PyP y crónicos, laboratorio, procedimientos externos | 24 |

La extracción cruda de cada pantalla está en [pantallas/](pantallas/), con los nombres de personas y las credenciales omitidos.

## Integraciones visibles

DIAN (factura electrónica, notas crédito y débito, POS), RIPS y Res. 3280/1888 (RDA al Ministerio), SISPRO/WebSisPro, BOT de agendamiento (App y Web), WhatsApp (estados en cola, enviado, entregado, leído y fallido), NEOSAGE, dispositivos de firma, huella y foto, y videollamada (telemedicina).

## Cobertura y límites

- Cubierto: 69 opciones del menú principal, 34 áreas de historia clínica con sus árboles y 60 pantallas de submódulos. En total, unas 125 pantallas únicas.
- No cubierto:
  - Los formularios clínicos internos, porque solo se abren desde la atención de un paciente real.
  - La lista de informes, porque depende de la especialidad del usuario y el SUPER ADMINISTRADOR no tiene ninguna.
  - Punto de venta, que es otro dominio, y "punto local", que apunta a localhost.
  - Tienda en línea, porque da error del servidor.
  - Empresas y Datos personales, que cargan vacías.
  - Las reglas de negocio que el servidor aplica y que la interfaz no muestra.
- Lo marcado "(inferido)" en los módulos es deducción a partir de la interfaz; lo marcado "(confirmado en código)" o "(corregido según código)" se verificó con el JavaScript de cliente.

## Hallazgos transversales del código

Fuente: JavaScript de cliente de las pantallas y archivos compartidos (`pantallas/_codigo-js.md`). Son hechos del cliente; lo que decide el servidor sigue sin verse.

- **Patrón de ventanas:** cada pantalla vive en un iframe dentro del shell y llama a funciones de la ventana madre (`parent.SF()` sesión finalizada, `parent.AccionSGR(...)` SignalR, `parent.GAJ(acción, datos)` auditoría, `parent.CargaTab(...)` abrir pestaña). Las pantallas no hablan con SignalR directamente.
- **Sesión y reautenticación:** el shell tiene un cambio obligatorio de clave (`CP`, mínimo 6 caracteres) distinto del de Mi cuenta (`IN`, mínimo 8); ninguno exige complejidad. Hay confirmación "Esta seguro de salir de la Sesión?" al cerrar. Las pantallas del turnero cargan periódicamente un script (`MantenerSesion.ashx`) para evitar el cierre por inactividad. La ventana "Sesión finalizada" se abre desde cualquier hijo con `SF()`.
- **Notificaciones:** notificaciones emergentes de Ext (`Ext.net.Notification`, helper `notificar(título, html, duración)`), alertas SweetAlert2 en pantallas nuevas (Empresas, Datos paciente) frente a `Ext.Msg` en las antiguas, contador de mensajes de chat pendientes que parpadea y un audio de notificación que se repite cada 10 s. No hay notificaciones push del navegador. El archivo `NotificacionesWeb.js` está vacío.
- **Almacenamiento local:** `BDCliente.js` sólo ofrece `JSON.stringify` y `JSON.parse` (`DataCodifica`, `DataDecodifica`) y un lector de archivos de texto; no usa IndexedDB. Cinco agendas guardan datos en `localStorage` para modo sin conexión y los purgan al cambiar el día (`VerificaDataOffLine`); el familiograma guarda su árbol en `localStorage`. No se guardan credenciales.
- **Auxiliares compartidos:** `General1.5.js` envuelve grillas y controles de Ext (`Grid*`, `Control*`, `Combo*`); `GeneralP.js` bloquea F5 y la tecla de retroceso fuera de campos de texto, limita textareas y clasifica el IMC según la OMS (`calcularPesoEtiqueta`); `filtro.js` da filtros locales de grilla (texto, fecha, número, booleano). Casi todos los filtros y listados se calculan en el navegador sobre lo ya cargado. `md.js` define MD5 en cliente, pero ninguna pantalla lo invoca.
- **Convenciones de llamada al servidor:** Ext.NET DirectMethods (`SRV.Metodo(...)`) en las pantallas Ext; PageMethods JSON con jQuery o `fetch` (`Pagina.aspx/Metodo`) en Empresas y Credenciales SISPRO. Nombres heredados engañosos (`GetCurrentTime` para guardar empresa, `CargarInformacionCita` para cargar empresa, `TIPODISCAPACIDAD` para el tipo de exoneración).
- **Hosts externos (sin direcciones):** Tickets embebe por HTTP, sin TLS, una aplicación de tickets externa y elige la vista administrativa si el rol activo tiene id 12; el diseñador de consentimientos inserta el logo desde un dominio externo del cliente; el concentrador SignalR del turnero se conecta a una URL que entrega el servidor (JSONP); Punto de venta es otro dominio y Punto local apunta a localhost.
- **Dispositivo de firma:** ocho pantallas (Activación de cita, Inicio historia, turnos de procedimientos, rayos X, urgencias, y citas de demanda inducida) usan el SDK de Wacom STU (`WacomGSS.STU`) contra el servicio local SigCaptX para capturar firma en tableta, con reintentos hasta 20 veces. Requiere el servicio instalado en el equipo del usuario.
- **Editores:** el diseñador de consentimientos usa el editor HTML nativo de Ext con botones propios y comodines numéricos entre corchetes ([1] nombre, [4] firma, [5] huella, [11] fecha, etc.); no usa Ace. El editor JSON (JSONEditor, que empaqueta Ace) se usa en Configuración General para editar la descripción de cada configuración.
- **Seguridad observada en cliente:**
  - Las credenciales SISPRO regresan al navegador y se cargan en el formulario al editar.
  - La vista administrativa de Tickets depende de un id de rol evaluado en el navegador.
  - Los permisos "Propios/Todos" se guardan por persona y módulo indirecto.
  - El paciente se registra con auditoría previa de la acción ("REGISTRAR PACIENTE").
  - El responsable del paciente se guarda como una sola cadena separada por guiones.
- **Sede:** se elige en el shell (`ComboSede`) y las pantallas operativas la envían como parámetro `SEDE`.

## Preguntas

Con pantallas, código JavaScript y norma colombiana se respondieron 68 preguntas; cada módulo las lista en "Respondidas", con su fuente. Lo que no se puede sacar del sistema (servidor, paciente real, decisiones del negocio) está agrupado por área en [preguntas-para-prored.md](preguntas-para-prored.md).
