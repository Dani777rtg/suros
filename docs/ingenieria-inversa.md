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
- Todo lo marcado "(inferido)" en los módulos es deducción a partir de la interfaz y hay que confirmarlo.

## Preguntas abiertas prioritarias

1. **Estados y transiciones:** cita, franja, ingreso o atención, factura, orden de compra y pedido. Falta saber qué acción dispara cada cambio y qué rol puede hacerlo.
2. **Permisos:** qué significa cada permiso por rol (Todos/Propios, módulos indirectos), si hay restricción por sede, y quién aprueba bloqueos, traslados de agenda, anulaciones y notas.
3. **Reglas de asignación de citas:** autorización, contrato vigente, límite por día, primera vez frente a control, y copago o cuota moderadora.
4. **Facturación:** cómo agrupa el facturador automático, cómo se calcula cada modalidad de contrato (evento, paquete, PGP, capitación, incremento), y si glosas y radicación están en otro sistema.
5. **Historia clínica:** formularios por especialidad (odontología, terapias, especializada), órdenes, fórmulas, interconsultas y remisiones con su ciclo, epicrisis y firma del ingreso.
6. **Farmacia:** si el despacho de lotes es FEFO automático o manual, los umbrales del semáforo de vencimientos, y el control de medicamentos de control especial (INVIMA/CUM).
7. **Integraciones:** formato, credenciales y reintentos de DIAN, RIPS y RDA, BOT, WhatsApp y NEOSAGE.
8. **Alcance:** si las pantallas en "OLD" se siguen usando, y qué contienen punto de venta, tienda en línea y tickets.

Cada módulo trae su propia lista detallada de preguntas.
