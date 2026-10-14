# Informes y catálogo principal

Resumen: este documento cubre (a) el módulo INFORMES (3 pantallas: panel de informes configurables, reporte de remisiones, reporte de citas médicas) y (b) las pantallas del menú CATALOGO PRINCIPAL: catálogos de medicamentos y plantillas (módulo Facturación), agendas del turnero y de enfermería, tickets de soporte y accesos a sub-aplicaciones (Almacén, Historia Clínica, Página Web, Punto de Venta, Punto Local). Almacén, Historia Clínica y Página Web son sub-aplicaciones con menú propio (documentadas aparte); aquí solo se describe su pantalla de inicio. Punto de Venta (otro dominio, `puntoventa.suros.co`) y Punto Local (`localhost`) no se pudieron extraer.

Convención: "(inferido)" marca suposiciones no observadas directamente en la UI. Se omiten ruido global (mensajes, OK/Sí/No/Cancelar, sesión finalizada, cambio de contraseña, notificación médica, paginación, ordenar/columnas).

---

## INFORMES > INFORMES (/SUROSHistoriaClinica/Vistas/Privado/Informes/InicioInformes.aspx)
- **Propósito**: hub de informes con árbol "LISTA DE INFORMES" y panel "CONFIGURACIÓN GENERAL"; también permite administrar (crear/editar) informes y carpetas. Título de la página: "Inicio Historia clinica".
- **Funcionalidades**: El usuario puede:
  - elegir especialidad (combo) y ver el árbol de informes disponible para ella (el árbol no cargó en la exploración: "no fue posible determinar la especialidad"; los informes dependen de la especialidad del usuario);
  - filtrar por médicos, especialidades, entidades (empresa/régimen) y estado de cita mediante popups de selección múltiple con botones "limpiar" y "seleccionar";
  - definir periodo por MES (año + mes) o RANGO DE FECHAS, **Consultar** y **Exportar a Excel**;
  - crear carpeta, crear/editar módulo, crear nuevo reporte, crear nuevo reporte por especialidad, crear informe de resolución 256, crear nuevo dominio, editar reporte (con editor HTML).
- **Datos**: Opción de fecha {MES, RANGO DE FECHAS}; Año; Mes {ENERO…DICIEMBRE}; Fecha inicial/final; Estado de cita (multi) {CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}; Médicos, Especialidades, Entidades (texto con selección).
  - Ventana "Crear informe de resolucion 256": proceso, fecha inicio/fin, número, indicador (INDICA), combos.
  - Ventana "Nuevo reporte": fecha inicio/fin de empresa, estándar (número), selector de opción.
  - Ventana "Nuevo reporte por especialidad": fecha inicio/fin, estándar numérico, especialidades (multi).
  - Ventana "Editar reporte": fechas, estándar, unidad {DIAS, MENSUAL, TRIMESTRE, SEMESTRE, ANUAL, %, MINUTOS} (la segunda lista sin "%"), prestador {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}.
  - Ventana "CREAR NUEVO DOMINIO": nombre de dominio. Ventana "Editar modulo": proceso/carpeta, fechas, valor estándar.
- **Listados**: popups de selección: MEDICO; ESPECIALIDAD; EMPRESA | REGIMEN.
- **Flujos y reglas inferidas**:
  - Cada informe tiene fechas de vigencia, un valor "estándar" (meta) y una unidad de medida (inferido: indicadores de calidad/cumplimiento con meta, p. ej. oportunidad en días o minutos).
  - Informes se organizan en carpetas/módulos por proceso (inferido).
  - La visibilidad del árbol depende de la especialidad del usuario (confirmado por el mensaje de error) (inferido el mecanismo).
  - El informe "resolución 256" apunta a indicadores de calidad normativos colombianos (inferido).

## INFORMES > REPORTE REMISIONES (/SUROSHistoriaClinica/Vistas/Privado/Informes/ReporteRemisiones.aspx)
- **Propósito**: consultar remisiones (derivaciones) generadas en un periodo.
- **Funcionalidades**: El usuario puede elegir tipo de consulta, fechas o año/mes, **Consultar**, **Exportar**, paginar y actualizar.
- **Datos**: Tipo de Consulta {Rango De Fechas, Mes}; Inicial; Final; Año; Mes {ENERO…DICIEMBRE}.
- **Listados**: "Reporte Remisiones": Documento | Paciente | Departamento | Teléfono | Fecha Soli | Cantidad | Código | Descripción | Observación | Especialidad Remite | Empresa | CIE10 | CIE Descripción | Persona Remite | Edad | Género.
- **Flujos y reglas inferidas**: una fila por servicio/código remitido con su diagnóstico CIE10 (inferido). Contiene datos personales de pacientes: requiere control de acceso (inferido).

## INFORMES > REPORTE CITAS MEDICAS (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Reportes/ReporteCitasMedicas.aspx)
- **Propósito**: reporte detallado de citas/servicios agendados con filtros múltiples.
- **Funcionalidades**: El usuario puede filtrar por especialidad, estado, médicos, entidades, contratos, diagnósticos CIE10 y CUPS (con búsqueda por código/nombre en popups "Diagnosticos" y "CUPS"), prioridad del diagnóstico, jornada y prestador; elegir formato GENERAL o RESUMIDO; **Consultar**, **Exportar a Excel**; botones "Reporte de Citas Demdicas" (sic) e "Info. Mensaje Masivos" (sin detalle observable).
- **Datos**: Opción de fecha {MES, RANGO DE FECHAS}; Año; Mes; FechaI/FechaF; Prestador de servicio {TODOS, PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}; Tipo de consulta (multi) {CITAS MEDICAS, CIRUGIAS, PROCEDIMIENTOS, RAYOS X, LABORATORIOS, URGENCIAS, QUIMIOTERAPIA}; Estado de la cita (multi) {CIRUGIA, CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}; Prioridad (multi) {PRINCIPAL, SECUNDARIO}; Jornada (multi) {TURNO 1…TURNO 10}; Campos {GENERAL, RESUMIDO}; Estado del médico/filtro {TODOS, ACTIVOS, INACTIVOS}; Diagnóstico; CUPS; Contrato.
- **Listados**: popups MEDICO; ESPECIALIDAD; EMPRESA | REGIMEN; CONTRATO; Código | Descripción (CIE10/CUPS). Grilla principal: Fecha asignación | Fecha atención | Turno | Tipo solicitud | Tipo consulta | Tipo cita | Estado cita | Estado ingreso | Jornada | Hora | Tipo doc | Documento | Nombre paciente | Fecha nacim | Etnia | Género | Prestador servicio | Empresa | Contrato | Régimen | Cód. diagnóstico | Descripción diagnóstico | Prioridad diagnóstico | Código CUPS | Procedimientos | Doc. médico | Nombre médico | Especialidad | Tipo historia | Observación.
- **Flujos y reglas inferidas**: una cita puede repetirse por cada diagnóstico/CUPS (inferido por columnas de prioridad y código). "Jornada" es el turno de agenda del prestador. "Asignada por BOT" indica canal automatizado de asignación (inferido). Fecha de nacimiento, etnia y género sugieren uso para reportes normativos (inferido).

---

## ALMACEN (/SUROSAlmacen/Vistas/InicioAlmacen.aspx)
- **Propósito**: página de inicio de la sub-aplicación Almacenes (título "SoftProject|Almacenes"). Menú propio (documentado aparte).
- **Funcionalidades**: árbol de opciones `TreeMenuOpciones` y panel "Inicio" vacío. Solo componentes globales (cambio de contraseña, notificación médica).
- **Datos / Listados**: ninguno propio.
- **Flujos y reglas inferidas**: sub-aplicación con sesión propia ("Sesión finalizada") (inferido).

## HISTORIA CLINICA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/InicioHistoria.aspx)
- **Propósito**: home de la Historia Clínica y buscador/consolidador de ingresos del paciente; punto de acceso a impresión, epicrisis, RDA y despacho de suministros. Menú propio documentado aparte.
- **Funcionalidades**: El usuario puede:
  - buscar paciente por Documento/Nombre y ver su información (documento, nombre, género, fecha nac., edad; botón "Información paciente"; ventana "Coincidencia con el parámetro ingresado" cuando hay varios);
  - filtrar ingresos por estado {EN ATENCIÓN, PREFACTURADO, FACTURADO, ATENDIDO, EN TRATAMIENTO}, fecha entrada/salida, especialidad o médico;
  - generar consolidados: de ingresos, ayudas DX, laboratorios, recomendaciones, remisiones y procedimientos; ver "Lista de Anexos";
  - **Generar ingreso sin cita** (fecha/hora de ingreso y salida);
  - sobre un ingreso: Asignar empresa (empresa, contrato, motivo), Configurar estados del ingreso (estado, fecha/hora de salida, destino médico, destino enfermera), Eliminar ingreso, Firmar ingreso, Ver folios anulados, Familiograma;
  - sobre los procedimientos del ingreso (grilla Impr | Id | Tipo Procedimiento | Estado | Fecha de registro | Opciones): Imprimir (ventana "Imprimir formatos" y "Ver formatos": un solo documento, carta/tirilla, encabezado), Trazabilidad, Epicrisis y reporte de epicrisis, informe de larga instancia, informes de ingreso, Formulación, Registros de actividades;
  - **Enviar RDA** (Registro de Atención) de PACIENTE, CONSULTA EXTERNA, URGENCIAS, HOSPITALIZACIÓN (inferido: interoperabilidad normativa; requiere "Credenciales" CONECTAR/VALIDAR y ventana "Ingresar credenciales" usuario/contraseña);
  - imprimir procedimientos médicos por mes/rango o trimestral/mensual, con opción ZIP y "Generar PDF"; informe de corte de larga instancia; "Impresión para Facturación"; anular factura (motivo de anulación); ver soportes de factura y soportes de actas de entrega (ID, número de acta, ciudad de entrega, fecha de entrega);
  - **Despacho de suministros desde enfermería** (ver abajo) y ver **Tratamiento anterior**; descargar consolidado.
- **Datos**: Credenciales (combo); Almacén Stock (combo); Estado de ingreso, destinos; Tipo de procedimiento (trigger); Opción de fecha {MES, RANGO DE FECHAS} o {RANGO DE FECHAS}; casillas "Un solo documento", "Documentos individuales", Carta/Tirilla; motivo de anulación; empresa/contrato.
- **Listados**:
  - Despacho de suministros desde enfermería: TIPO | Código | Suministro | Solicitada | Entregada; y "Suministros en inventario": Cant. Entrega | Item | Presentación | Lote | Fecha Venc. | Cant. Actual | Cant. Descargada | Cant. Almacenada. Botón Finalizar.
  - Tratamiento anterior: ID | MECA ID | Fecha solicitud | Tipo de procedimiento | Solicitado por | Cantidad | Und/Med | Cada | Und/Med | Vía de administración | Tiempo | Und/Med | Modificado | Suspendido; detalle de medicamento: ID | Código | Nombre | Forma farmacéutica | Concentración | Presentación | Cant. dosis | Posología.
  - Ingresos: Id | Estado | Fecha ingreso | Fecha salida. Registros de actividades: ID | Fecha registro | Profesional que registra | Destino paciente | Opciones. Folios anulados: Identificador | Número | Modificado por | Opciones. Ver formatos: Descripción | Prev / Carta / Tirilla. Árbol "Modulos" del ingreso.
- **Flujos y reglas inferidas**: el ingreso es la unidad que agrupa procedimientos/folios (inferido). El despacho descuenta del inventario del almacén elegido por lote y fecha de vencimiento, y registra cantidad solicitada vs entregada (inferido). Firmar ingreso cierra la edición (inferido). Estados de ingreso listados arriba forman el ciclo EN ATENCIÓN → ATENDIDO/EN TRATAMIENTO → PREFACTURADO → FACTURADO (orden inferido).

---

## CATALOGO PRINCIPAL > PLANTILLA MEDICAMENTOS (/SUROSFacturacion/Vistas/Privado/Plantillas/PlantillaMedicamentos.aspx)
- **Propósito**: administrar plantillas (listas predefinidas) de medicamentos.
- **Funcionalidades**: El usuario puede crear una plantilla nueva, editarla, agregar (Add) o quitar medicamentos mediante buscador por código/nombre ("Coincidencia encontrada"), guardar / aceptar y guardar / salir, refrescar y paginar el listado.
- **Datos**: Nombre de la plantilla; Observación.
- **Listados**: plantillas: Fecha creación | Nombre de plantilla | Activo | Observación. Medicamentos de la plantilla: Código | Nombre genérico | Nombre comercial | Forma farmacéutica | Concentración | Valor para EPS. Búsqueda: Código | Nombre genérico | Nombre comercial | Forma | Concentración.
- **Flujos y reglas inferidas**: "Valor para EPS" es un precio pactado por entidad (inferido). Las plantillas se usan para prescribir/facturar en bloque (inferido).

## CATALOGO PRINCIPAL > PLANTILLA INSUMOS (/SUROSFacturacion/Vistas/Privado/Plantillas/PlantillaInsumos.aspx)
- **Propósito**: igual que la anterior para insumos (la etiqueta de la UI sigue diciendo "Lista de medicamentos"/"Plantilla de medicamentos", copia de la pantalla anterior).
- **Funcionalidades**: crear/editar plantilla, agregar/quitar insumos con búsqueda, guardar, paginar.
- **Datos**: Nombre de la plantilla; Observación.
- **Listados**: plantillas: Fecha creación | Nombre | Activo | Observación. Insumos: Descripción | Unidad de medida | Valor para EPS. Búsqueda: Código | Nombre | Nombre.
- **Flujos y reglas inferidas**: mismo flujo que medicamentos (inferido).

## CATALOGO PRINCIPAL > MEDICAMENTO (/SUROSFacturacion/Vistas/Privado/Medicamentos/Medamento.aspx)
- **Propósito**: catálogo de nombres de medicamento (principios activos / nombres base).
- **Funcionalidades**: El usuario puede agregar, editar y eliminar nombres de medicamento, con filtros de búsqueda y paginación.
- **Datos**: Nombre medicamento; Es principio activo {SI, NO}; Código DCI; Clave; Activo {SI, NO}.
- **Listados**: Nombre | Principio activo.
- **Flujos y reglas inferidas**: este catálogo alimenta el "Nombre genérico" de la pantalla siguiente (inferido). DCI = Denominación Común Internacional (inferido).

## CATALOGO PRINCIPAL > ADMINISTRACIÓN CATALOGO MEDICAMENTOS (/SUROSFacturacion/Vistas/Privado/Medicamentos/AdministracionMedicamentos.aspx)
- **Propósito**: administrar el catálogo principal de presentaciones de medicamentos.
- **Funcionalidades**: El usuario puede agregar al catálogo (ventana "Agregar al catálogo principal"), editar, eliminar, buscar y paginar.
- **Datos**: Código; Nombre genérico (combo); Nombre comercial (combo); Forma farmacéutica (combo); Concentración (combo).
- **Listados**: Fecha creación | Código | Nombre genérico | Nombre comercial | Forma farmacéutica | Concentración | Estado.
- **Flujos y reglas inferidas**: un ítem de catálogo es la combinación genérico + comercial + forma + concentración con código propio (inferido). Es la fuente de los medicamentos de las plantillas y de la formulación (inferido).

## CATALOGO PRINCIPAL > PAGINA WEB (/SUROSPaginaWeb/Vistas/InicioPaginaWeb.aspx)
- **Propósito**: inicio de la sub-aplicación CMS ("SoftProject | CMS"); menú propio documentado aparte.
- **Funcionalidades**: solo árbol `TreeMenuOpciones`.
- **Datos / Listados**: ninguno propio.

## CATALOGO PRINCIPAL > AGENDA CONSULTAS TERMINADAS (/SUROSTurnero/Vistas/Privado/Agenda/AgendaConsultasTerminadas.aspx)
- **Propósito**: tablero del turnero de consulta externa: gestión de turnos de pacientes que terminaron consulta, atendido por un asesor desde un puesto.
- **Funcionalidades**: El usuario puede:
  - seleccionar asesor y **establecer** su puesto, o **crear nuevo** puesto (ventana "CREAR PUESTO": nombre y sede) y **cerrar puesto**;
  - filtrar por consultorio (multi), especialidad y fecha; **Consultar**, **Mostrar toda la agenda**, actualizar lista de turnos;
  - sobre un turno: **Activar**, **Imprimir órdenes** (ventanas "Ver formatos"/"Imprimir formatos", carta/tirilla), **Realizar nuevamente el llamado**, marcar **Atendido**, **No atendió llamado**, **Activar nuevamente el turno**.
- **Datos**: Asesor; Puesto (Nombre, Sede); Consultorio; Especialidad; Fecha.
- **Listados**: ID | Paciente | Documento | Consultorio | Procedimiento médico | Médico | Fecha.
- **Flujos y reglas inferidas**: los turnos se llaman por puesto; si el paciente no responde se marca "no atendió llamado" y puede reactivarse (inferido). Al terminar, se imprimen las órdenes (inferido).

## CATALOGO PRINCIPAL > AGENDA HOSPITALIZACIÓN (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaFacturacionHospitalizacion.aspx)
- **Propósito**: agenda de enfermería: pacientes hospitalizados por cama, con reportes de facturación/instancia.
- **Funcionalidades**: El usuario puede ver ayuda de colores, mostrar solo salidas del médico, filtrar por mes o rango, empresa y tipo de archivo, **Generar reporte** (PDF o Excel), **Reporte instancia** y actualizar la agenda.
- **Datos**: Opción {MES, RANGO DE FECHAS}; Año; Mes; Fec. inicial/final; Empresa {TODAS más entidades del tenant observado}; Tipo {PDF, EXCEL}.
- **Listados**: Fecha ingreso | Cama | Tipo doc | Documento | Nombre paciente | EPS | Nota de ingreso | Observación de ingreso | Caso especial.
- **Flujos y reglas inferidas**: los colores codifican estado de la cama/paciente (inferido; leyenda no extraída). "Caso especial" marca pacientes con condición particular (inferido).

## CATALOGO PRINCIPAL > TICKETS (/SurosTickets/Vistas/Ticket.aspx)
- **Propósito**: soporte de ayuda ("Soporte de Ayuda SoftProject"). Solo un panel; no se extrajeron campos (probablemente contenido embebido/externo) (inferido).

## CATALOGO PRINCIPAL > ATENCIÓN AL USUARIO (/SUROSTurnero/Vistas/Privado/Agenda/AgendaServicios.aspx)
- **Propósito**: turnero de atención al usuario (servicios), con asesor y puesto.
- **Funcionalidades**: El usuario puede seleccionar asesor y establecer puesto, filtrar por puesto y fecha, consultar, mostrar toda la agenda, actualizar turnos, cerrar puesto, ordenar/agrupar.
- **Datos**: Asesor; Puesto (multi); Fecha.
- **Listados**: ID | Instancia | Sigla | Turno | Hora | Asistió | No atendió el llamado | Método | Puesto.
- **Flujos y reglas inferidas**: "Sigla" es el prefijo del turno por servicio y "Método" el canal de generación del turno (inferido).

## CATALOGO PRINCIPAL > PUNTO DE VENTA (http://puntoventa.suros.co/Vista/Privado/Inicio.aspx)
- **Propósito**: aplicación externa (otro dominio). No extraída: el acceso al marco desde `prored.suros.co` fue bloqueado por política de origen cruzado.

## CATALOGO PRINCIPAL > PUNTO LOCAL (http://localhost:61167/Vista/Privado/Inicio.aspx)
- **Propósito**: apunta a un servidor local (puerto 61167), probablemente una instalación local del punto de venta (inferido). No extraída.

---

## Entidades y estados
- **Informe/Reporte**: carpeta, módulo, nombre, fechas de vigencia, estándar (meta), unidad {DIAS, MENSUAL, TRIMESTRE, SEMESTRE, ANUAL, %, MINUTOS}, prestador, especialidad; dominio.
- **Prestador de servicio** (sedes PRORED): FLORENCIA-CAQUETÁ, CAUCA, PASTO-NARIÑO, RISARALDA.
- **Cita**: tipos {CITAS MEDICAS, CIRUGIAS, PROCEDIMIENTOS, RAYOS X, LABORATORIOS, URGENCIAS, QUIMIOTERAPIA}; jornada TURNO 1-10; diagnóstico (CIE10, prioridad PRINCIPAL/SECUNDARIO); CUPS; contrato/empresa/régimen.
- **Estado de cita**: CIRUGIA, CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT.
- **Estado de ingreso**: EN ATENCIÓN, PREFACTURADO, FACTURADO, ATENDIDO, EN TRATAMIENTO.
- **Ingreso**: fechas entrada/salida, empresa/contrato, destino médico/enfermera, procedimientos/folios (con anulados), actas de entrega, factura y soportes.
- **Catálogo de medicamentos**: Medicamento (nombre, principio activo, DCI, clave, activo) y Catálogo (código, genérico, comercial, forma, concentración, estado); Plantilla de medicamentos / de insumos (nombre, activo, observación, ítems con valor para EPS).
- **Suministro/inventario**: almacén, lote, fecha de vencimiento, cantidades actual/descargada/almacenada, solicitada/entregada.
- **Turnero**: asesor, puesto (nombre, sede), turno (sigla, hora, asistió, no atendió), consultorio.
- **Cama/hospitalización**: cama, ingreso, nota, caso especial.

## Preguntas abiertas
1. Qué informes contiene realmente la LISTA DE INFORMES y cómo se asocian a especialidades/perfiles (el árbol no cargó); cómo se calculan los indicadores con estándar y unidad.
2. Qué hacen exactamente "Info. Mensaje Masivos", "Reporte de Citas Demdicas" e "Informe de larga instancia"/"Reporte Instancia"; qué es "instancia".
3. Cómo funcionan el envío de RDA (formato, destino, credenciales) y la firma del ingreso (cierra edición, valida qué).
4. Reglas de estados del ingreso y de la cita: transiciones permitidas, quién las dispara, y cómo se anulan facturas y folios.
5. Contenido de Tickets, Punto de Venta y Punto Local (no extraídos), y significado de la leyenda de colores de Agenda Hospitalización y de "Caso especial".
