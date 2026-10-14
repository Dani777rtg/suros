# Citas médicas

Módulo que gestiona la programación de agendas médicas (por profesional, jornada/turno y sede), la asignación de citas y turnos a pacientes (consulta, procedimientos externos, urgencias, demanda inducida, laboratorio/rayos X), la recepción y visado de autorizaciones, y la bitácora de llamadas de contacto. Incluye canales de agendamiento por BOT App/Web y notificaciones por WhatsApp.
Actores inferidos: administrador/programador de agenda, auxiliar de admisiones/citas, personal de autorizaciones, gestor de demanda inducida, médico/auxiliar asignado a agenda, paciente (vía BOT App/Web).
Entidades principales: Agenda (programación), Franja/Turno, Cita, Paciente, Autorización/Orden, Procedimiento (CUPS), Diagnóstico (CIE10), Empresa/Contrato (EPS), Adjunto, Llamada de bitácora, Campaña WhatsApp, Malla de reumatología.

Todas las pantallas comparten (inferido) un bloque común: búsqueda de paciente por documento/nombre, creación/edición de paciente, datos de responsable/acudiente/acompañante, foto/firma/huella digital, adjuntos físicos y digitales, CIE10, procedimientos, datos laborales (medicina laboral), "Firmar ingreso", "Recibo de pago" y "Enviar Copago a Dian". Se documentan una vez en "Bloques comunes" al final de las entidades.

---

## Programar agenda médica (/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaMedica.aspx)
- **Propósito**: crear y administrar la programación de agendas por profesional/jornada y gestionar la disponibilidad de sus franjas (bloqueo, canal BOT, demanda inducida).
- **Funcionalidades**:
  - El usuario puede generar la agenda (botón Generar) en modo intervalo (hora inicial/final + minutos por turno) o por número de pacientes (opciones 1 y 2 del radio).
  - Puede elegir mes y año, actualizar el calendario y guardar la programación.
  - Puede ver programaciones eliminadas (checkbox "Mostrar programación eliminada").
  - Puede asignar médico a la agenda, asignar médico o auxiliar acompañante y agregar convenio a la agenda.
  - Puede bloquear franjas seleccionadas indicando tipo de bloqueo (Por IPS / Por Médico) y causa; puede desbloquear.
  - Puede bloquear/desbloquear franjas para agendamiento por BOT App/Web y por BOT App.
  - Puede activar franjas para BOT App/Web, BOT App o Demanda Inducida con tipo de activación (Por Defecto, Prioritaria; Demanda Inducida solo Por Defecto), individualmente o "Activar seleccionadas".
  - Puede ver resumen de turnos.
  - Puede refrescar, cerrar y filtrar la lista de médicos por especialidad.
  - Puede consultar campañas de mensajes WhatsApp asociadas, envíos por paciente e historial de mensajes.
- **Datos**:
  - Filtros/menú: Prestador de servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}; Jornada de atención (multi) {TURNO 1..TURNO 10}; Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}; Categorías; Ejecución/Nivel de complejidad; Equipo de atención; Zona de atención; Unidad funcional {AMBULATORIO}; Grupo de servicio {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}; Servicios.
  - Datos generales: consultorio (numérico), Externo (checkbox) + consultorio externo, observación, tipo de intervalo (radio), hora inicial/final, minutos por turno, número de pacientes (dos variantes: con intervalo y con rango horario).
  - Datos específicos: Especialidad, médico principal; Mes {ENERO..DICIEMBRE}, Año.
  - Bloqueo: Tipo de bloqueo {Por IPS, Por Médico}, Causa (texto, requerida por el diseño de la ventana).
  - Activación: Tipo de activación {Por Defecto, Prioritaria} (Demanda Inducida: {Por Defecto}).
  - Convenio (combo), Médico (combo), Médico o auxiliar (combo).
- **Listados**:
  - Lista de médicos.
  - Calendario: DOM–SAB.
  - Programación: ID | Fecha | Hora inicial | Hora final | Descripción | Profesional principal | Profesional auxiliar | Tiempo atención | Turnos creados | Turnos asignados | Jornada | Programada por.
  - Franjas: Turno | Hora | Estado | Acciones. Variantes: Franjas BOT App/Web, Franjas BOT App, Franjas Demanda Inducida (mismas columnas).
  - Campañas: Campaña | Plantilla | Fecha | Total | OK | Fallidos | Estado.
  - Envíos por paciente: Paciente | Teléfono | Fecha envío | Estado | WhatsApp ID.
- **Flujos y reglas inferidas**:
  - Una agenda se crea por fecha(s) del calendario + jornada(s) + profesional + consultorio; genera N turnos (franjas) con hora; "Turnos creados" vs "Turnos asignados" mide ocupación (inferido).
  - Cada franja tiene estado (valores no listados) y canal: normal, BOT App/Web, BOT App, Demanda Inducida; una franja se "activa" para un canal y puede bloquearse (inferido).
  - Bloquear exige tipo (por IPS o por médico) y causa.
  - La eliminación de programación es lógica (existe filtro para mostrar eliminadas) (inferido).
  - Existen versiones "BOT App/Web" y "BOT App" de las mismas ventanas, probablemente por parámetro de sede/prestador (inferido).

## Cita médica unificada (/SUROSHistoriaClinica/Vistas/Privado/Agenda/CitaDemandaInducidaUnificada.aspx)
- **Propósito**: pantalla principal de asignación y gestión de citas sobre la agenda (consulta, procedimientos, laboratorio, demanda inducida), unificando varios tipos de cita.
- **Funcionalidades**:
  - El usuario puede buscar paciente (documento/nombre) o crear paciente nuevo y ver su información, historial de citas médicas (paginado) y de citas de laboratorio.
  - Puede seleccionar jornada(s), mes/año y día en el calendario de la agenda de un profesional/especialidad y ver otras agendas y % de agenda por profesional.
  - Puede asignar cita, modificar (M), eliminar (Supr), cambiar de turno (C), transferir cita (T), asignar cita de transferencia, imprimir (P), asignar turno, eliminar cita opcional, ver nota de inasistencia, activar cita, volver a "asignado", ver trazabilidad, firmar ingreso, agregar cita grupal.
  - Puede cambiar la fecha de la agenda, transferir toda la agenda o una jornada a otro médico, activar toda la agenda, agregar turnos al final, eliminar últimos turnos.
  - Puede exportar la agenda, actualizar, ver opciones.
  - Puede marcar al paciente como "No realizó consulta" o "Atendido en otra institución" (institución, fecha de atención, observación).
  - Puede registrar laboratorio y procedimiento externo; subir laboratorios (PC) por tipo de historia {CONSULTA HIGIENE ORAL, ESPECIALES (CRONICOS), REUMATOLOGIA} con grilla Examen/Valor.
  - Puede registrar signos vitales previos a la consulta.
  - Puede generar consentimiento informado (editor HTML con vista previa), buscar procedimiento, traer datos biométricos del ingreso, obtener firma (dispositivos), aplicar datos al formato.
  - Puede tomar foto del paciente, subir firma digital y huella (obtener huella/link).
  - Puede notificar por WhatsApp a pacientes de la agenda en asistente de 3 pasos (Atrás/Siguiente/Enviar notificaciones): lista de pacientes con celular válido vs sin celular válido, plantilla de mensaje y vista previa; y ver historial de envíos masivos con detalle y línea de tiempo.
  - Puede habilitar programas especiales, configurar la malla de reumatología y periodicidad por especialidad.
  - Puede agregar médico externo e institución (con departamento/municipio), ver adjuntos, ver/descargar imagen (PNG/JPG, zoom, rotar), enviar copago a la DIAN, adicionar procedimientos a la orden (búsqueda de CUPS con selección múltiple) y fórmula desde ingresos del paciente.
  - Puede enviar mensaje de confirmación al guardar la cita (checkbox).
- **Datos**:
  - Agenda: Prestador de servicios, Jornada, Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}, Categorías {JORNADA DE SALUD, VISITA DOMICILIARIA, UNIDAD MOVIL, TELEMEDICINA INTERACTIVA, TELEMEDICINA NO INTERACTIVA, TELEXPERTICIA, TELEMONITOREIO, INTRAMURAL}, Ejecución/Nivel de complejidad, Equipo de atención, Zona de atención, Tipo usuario, Tipo paciente.
  - Cita: Fecha solicitud, Fecha que quería el paciente, Fecha asignación, Número de citas {1,2,3,4}, Gestante {SI, NO}, Vía de ingreso {DEMANDA ESPONTANEA, DERIVADO DE CONSULTA EXTERNA, DERIVADO DE URGENCIAS, DERIVADO DE HOSPITALZACION, DERIVADO DE SALA DE CIRUGIA, DERIVADO DE SALA DE PARTOS, RECIEN NACIDO EN LA INSTITUCION, RECIEN NACIDO EN OTRA INSTITUCION, DERIVADO O REFERIDO DE HOSPITALIZACION DOMICILIARIA, DERIVADO DE ATENCION DOMICILIARIA, DERIVADO DE TELEMEDICINA, DERIVADO DE JORNADA DE SALUD, REFERIDO DE OTRA INSTITUCION, CONTRAREFERIDO DE OTRA INSTITUCION}, Limitación escalera {NO APLICA, SI, NO}, Tipo consulta/modalidad, Tipo de cita (ver Entidades), Subsidio RPMS, Tipo procedimiento gastro, Acompañante aplica {SI, NO}, Responsable, Acudiente/acompañante, Tipo de asignación {PRESENCIAL, TELEFONICA}, No. autorización, Empresa (ver catálogo), Contrato, Observación.
  - Orden médica: institución que remite, médico que remite, fecha orden, "Orden remitida desde Surós" {SI, NO} + Referenciar orden, "Primera vez del tratamiento de reumatología" (checkbox).
  - Diagnóstico: CIE10 (código/nombre), Tipo diagnóstico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}, prioridad.
  - Signos vitales: tensión sistólica/diastólica, frecuencia cardiaca, frecuencia respiratoria, glucometría, temperatura, peso, talla, IMC, superficie corporal (M2), riesgo.
  - Adjuntos: Categoría {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}, Tipo soporte digital, Relación con el paciente, descripción, archivo.
  - Eliminar cita: Motivo (combo), Observación. Cambio de turno: Jornada, Turnos disponibles. Adicionar citas: Número de citas. Datos laborales: fecha ingreso a la empresa, tipo de examen médico, empresa contratante, empresa en misión, cargo.
  - Notificación WhatsApp: plantilla, vista previa, detalle; filtro de estado de mensajes {Todos, En cola, Enviado, Entregado, Leído, Fallido}.
  - Copago DIAN: Resolución (combo), id copago, agenda.
- **Listados**:
  - Citas de la agenda: Jornada | Hora | Hora fin | Turno | Documento | Nombre paciente | Procedimiento | Tipo cita | No. Autorización | Empresa | Contrato | Régimen | Medio solicitud | Lugar de residencia | Fecha asignación | Registrado por | Estado | Sede | Nota | Celular.
  - Citas médicas del paciente: Descripción | CUPS | Fecha | Hora | Tipo de cita | Registrado por | Médico | Tipo de consulta | Estado | Factura | Info.
  - Citas laboratorio: ID | Procedimiento | CUPS | Tipo cita | Fecha asignación | Fecha toma | Fecha entrega | Registrado por | Estado.
  - Programa Res. 3280: Programa | Profesional que puede realizar | Ver sólo actividades pendientes | Programadas | Inasistencia | Ejecutadas | Fecha/especialidad última ejecutada | Programada | Fecha/especialidad última programada.
  - Malla: Especialidad | Periodicidad | ENE..DIC. Profesional de la salud: Profesional | % de agenda. Otras agendas.
  - Procedimientos: Código | Descripción | Cantidad | Observación (y variante ID | Cantidad ejecutada). Procedimientos CUPS: Código | Descripción | Tipo manual. Diagnóstico: Código | Descripción | Prioridad.
  - Adjuntos: Datos de adjunto | administrativo | archivo; Soportes digitales: Categoría | No Autorización | Tipo de soporte | Fecha creación | Registrado por | PDF | Modificar | Eliminar.
  - WhatsApp: Campañas (Campaña | Plantilla | Fecha | Estado | Total | Env. | Ent. | Leíd. | Fall.); Mensajes (Paciente | Teléfono | Estado | Fecha envío | Mensaje).
  - Ingresos del paciente.
- **Flujos y reglas inferidas**:
  - Estados de cita (inferido de botones): asignado, activado, atendido, cancelado/eliminado, "volver a asignado" revierte estado; transferir y "asignar cita de transferencia" son un par (origen/destino) (inferido).
  - Eliminar cita exige Motivo y Observación.
  - Cambio de turno: elegir jornada y turno disponible de la misma agenda.
  - Cita de laboratorio tiene ciclo asignación, toma, entrega.
  - Las citas se limitan a 1-4 por asignación.
  - Medicina laboral requiere datos laborales; reumatología requiere flag de primera vez y malla.
  - Atajos de teclado: M, Supr, C, T, P.
  - Envío de WhatsApp excluye a pacientes sin celular válido (la UI los lista aparte).
  - El flujo "Demanda inducida" busca contactar al paciente para agendar; "No realizó consulta" y "Atendido en otra institución" cierran el seguimiento (inferido).

## Activación de cita (/SUROSHistoriaClinica/Vistas/Privado/ActivacionCita/ActivacionCita.aspx)
- **Propósito**: activar (confirmar la llegada/pago) las citas pendientes de un paciente y emitir el recibo de caja.
- **Funcionalidades**:
  - El usuario puede buscar paciente por documento/nombre y ver su identificación, género, nombre, fecha de nacimiento, empresa, régimen, zona y municipio de residencia.
  - Puede mostrar todas las citas o actualizar pendientes.
  - Puede agregar copago autorizado (credenciales de usuario/contraseña: autorización de supervisor, inferido) y agregar recibo de pago.
  - Puede imprimir recibo de pago y convertirlo a electrónico (facturación electrónica).
  - Puede enviar copago a la DIAN con resolución.
  - Puede firmar el ingreso (firma por teléfono, obtener firma/link, subir archivo, huella), tomar datos biométricos, generar consentimiento.
  - Puede editar datos del paciente, asignar responsable/acudiente/acompañante, adjuntar soportes, agregar diagnóstico CIE10 y procedimientos, agregar médico externo e institución.
  - Puede guardar y cerrar, imprimir.
- **Datos**: mismo bloque de cita que Cita unificada (agenda, fechas, vía de ingreso, tipo de cita, tipo de asignación, empresa, contrato, autorización, orden médica, datos laborales). Recibo de caja: concepto, valores, información de caja. Ingreso de credenciales: nombre de usuario, contraseña.
- **Listados**: Citas pendientes (ID | Código | Procedimiento/Profesional ×2); Recibo de caja (Concepto | Valores | Información caja); Diagnóstico; Procedimientos; Adjuntos físicos y digitales.
- **Flujos y reglas inferidas**:
  - Activar = pasar de ASIGNADO a ACTIVADO tras pago/copago y firma de ingreso (inferido por el catálogo de estados de Turno Procedimientos).
  - El copago requiere autorización con credenciales (inferido).
  - El recibo puede convertirse a factura electrónica y reportarse a la DIAN.

## Recepción autorizaciones (/SUROSHistoriaClinica/Vistas/Privado/Autorizaciones/RecepcionAutorizacion.aspx)
- **Propósito**: recibir, revisar (visar) y asignar cita a las autorizaciones/órdenes que llegan de pacientes, incluso por WhatsApp.
- **Funcionalidades**:
  - El usuario puede consultar por rango de fechas (Este mes, Esta semana, personalizado), filtrar Pendientes/Asignados, por empresa (multi) y contrato, y buscar en la agenda médica filtrada.
  - Puede hacer búsqueda avanzada (por estados de terapias, documento, id, rango), desbloquear campos y exportar.
  - Puede agregar una orden (nueva autorización) con paciente (buscar/crear/actualizar datos), prestador, tipo de consulta, tipo de programa especial, datos de cita, procedimientos, diagnóstico, adjuntos y médico/institución que remite.
  - Sobre cada registro puede: visualizar adjuntos, asignar cita, reasignar cita, ver información de eliminación, cambiar estado de recepción, contactar por WhatsApp, modificar registro (M), ver/agregar notas, visar y ver información de visado, eliminar (Supr), actualizar clasificación CUPS, marcar como prioritaria, marcar como control.
  - Puede agregar adjuntos (digitalizados/físicos), ver imagen, descargar PNG/JPG.
  - Puede cantidad de terapias (asignar N terapias con fecha, hora y médico) y ver citas pendientes.
- **Datos**:
  - Orden: Prestador {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}; Tipo de consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}; Tipo programa especial {NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}; Tipo de afiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}; paciente (tipo/num. documento, nombre, nacimiento, género, cotizante, empresa, municipio, dirección, celular, teléfono).
  - Cita: fecha solicitud, fecha queria paciente, fecha asignación, número de citas {1-4}, gestante, limitación escalera {NO APLICA, SI, NO}, tipo de cita (ver catálogo), subsidio RPMS, tipo procedimiento gastro, acompañante aplica {SI, NO}, tipo de asignación {PRESENCIAL, TELEFONICA, INTERNET}, no. autorización, empresa, contrato, institución/médico que remite, fecha de la orden médica, observación.
  - Diagnóstico CIE10 con tipo {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}.
  - Estado recepción {Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta} + checkbox "Enviar mensaje por WhatsApp sobre este estado" + mensaje libre al paciente.
  - Visado: Mes/Día/Año de futura revisión, Tipo de cita {PRIMERA VEZ, CONTROL}, Observación.
  - Eliminar cita: Motivo + observación. Reprogramar: razón textual obligatoria ("explique la razón por la cuál se realiza la reprogramación").
  - Nota: texto, fecha, hora.
  - Filtro estados terapias {TODOS, ASIGNADO, PENDIENTE, ATENDIDO, CITA CANCELADA, CANCELADA SIN CITA}.
  - Terapias: cantidad, fecha cita, hora cita, número de terapias, médico.
  - Historial de citas del paciente: filtros por fecha, turno, hora, médico, registrador, motivo cambio de estado, tipo asignación, estado.
- **Listados**:
  - Recepción de autorizaciones: Id | Fecha | Documento | Nombre paciente | Teléfono | Institución que remite | Especialidad | Diagnóstico | Estado | Estado asignación | Origen | Servicio | Programa PYP | Estado recepción | WhatsApp | Visado | Médico que remite | Asignado por.
  - Historial de citas: Fecha | Turno | Hora | Médico | Registrado por | Nota | Tipo asignación | Estado.
  - Procedimientos: Código | Descripción | Cantidad | Observación. Procedimientos quirúrgicos/diagnóstico: Código | Descripción | Prioridad.
  - Actualizar clasificación CUPS: Código | Descripción | Clasificación actual | general | específica | Justificación del cambio.
  - Historial de notas; Adjuntos de la cita; Citas pendientes (Id | Hora | Fecha | Nombre paciente | Médico); Lista de médicos.
- **Flujos y reglas inferidas**:
  - Ciclo de recepción (inferido): llega orden, se revisa y se marca {Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta}; opcionalmente se notifica al paciente por WhatsApp con ese estado.
  - Visado: autorización validada con fecha de futura revisión y tipo de cita; luego se asigna/reasigna cita.
  - Estado de asignación: pendiente vs asignado; reasignar/reprogramar exige razón; eliminar exige motivo.
  - Se puede marcar prioridad o convertir a control; la clasificación CUPS se corrige con justificación obligatoria (inferido por columna).
  - Origen del registro incluye canal (WhatsApp, manual) (inferido).

## Bitácora demanda inducida (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Bitacora/Bitacora.aspx)
- **Propósito**: registrar y consultar las llamadas de contacto a pacientes (demanda inducida, entrega de medicamentos, educación, ayudas diagnósticas).
- **Funcionalidades**:
  - El usuario puede buscar paciente (nombre/documento), seleccionar prestador y área que genera, y agregar/quitar teléfonos de contacto.
  - Puede registrar una llamada: contestó paciente u otra persona, hora, motivo, receptor, parentesco, nota y respuesta del usuario; guardar, actualizar o cancelar la actualización.
  - Puede usar plantillas de nota/observación: crear, editar, eliminar, guardar ítems en plantilla y cargar plantilla ("Mis plantillas").
  - Puede consultar historial de llamadas filtrando por Rango de fecha, Paciente o Todo, con prestadores múltiples; exportar a PDF y a Excel.
  - Puede imprimir formatos (carta o tirilla, selección por ítem), editar y eliminar registros.
- **Datos**: Prestador de servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}; paciente (nombre, documento, id persona); Área que genera; Teléfono; Contestó paciente / Otra persona (radio); Hora de llamada; Motivo de llamada {Demanda inducida, Entrega de medicamentos, Educacion, Revision de ayudas diagnosticas}; Receptor de la llamada; Parentesco {MAMÁ, PAPÁ, HIJO(A), TIO(A), ABUELO(A), PRIMO(A), SOBRINO(A), ESPOSO(A), OTRO, HERMANO(A)}; Nota; BILL_ID (factura asociada, inferido); Filtros: Filtrar por, Fecha inicial/final.
- **Listados**: Teléfonos del paciente (Teléfonos | Quitar); Historial de llamadas (columnas no extraídas); Ítems de impresión (Descripción | Carta | Tirilla); Plantillas (Descripción).
- **Flujos y reglas inferidas**: cada llamada deja constancia de a quién se contactó (paciente u otra persona + parentesco). Las plantillas son personales ("Mis plantillas") (inferido). Imprimir formatos permite carta o tirilla.

## Turno procedimientos externos (/SUROSHistoriaClinica/Vistas/Privado/Agenda/TurnoProcedimientos.aspx)
- **Propósito**: asignar y gestionar turnos para procedimientos externos (citología, planificación, vacunación) sin agenda de médico fija.
- **Funcionalidades**:
  - El usuario puede crear nuevo ingreso/turno, buscar o crear paciente y editar sus datos.
  - Puede guardar, limpiar, cancelar, modificar turno (M), eliminar cita (Supr), ver trazabilidad, imprimir (P), activar cita.
  - Puede filtrar el listado por fecha y estado, y actualizar.
  - Puede asignar procedimientos (búsqueda CUPS) con cantidad y observación; quitar procedimientos.
  - Puede agregar diagnóstico CIE10, adjuntos físicos y digitales, foto, firma y huella, datos laborales, firmar ingreso, recibo de pago y copago DIAN.
  - Puede agregar médico externo e institución.
  - Puede cancelar turno con motivo y observación.
- **Datos**: Tipo afiliado ingreso (catálogo de afiliados); Modalidad; Prestador; Categorías; Tipo programa especial {NO APLICA}; Equipo de atención; Tipo paciente; Unidad funcional {AMBULATORIO}; Grupo de servicio; Servicios; Fecha solicitud, hora turno, fecha que quería el paciente, fecha asignación; Gestante {SI, NO}; Vía de ingreso (catálogo); Tipo de cita {PROCEDIMIENTO EXTERNO, CITOLOGIA, PLANIFICACIÓN, VACUNACION}; Categoría de procedimiento; Responsable; Tipo de asignación {PRESENCIAL, TELEFONICA}; No. autorización; Empresa; Contrato; Atiende (combo de profesionales); institución/médico que remite; observación; Primera vez reumatología; Cancelar turno: Motivo + Observación.
- **Listados**: Turnos procedimientos: Turno | Sede atención | Fecha asignación | TD | Documento | Nombre | Empresa | Acudiente | Tipo procedimiento | Procedimientos | Médico atiende | Contrato. Procedimientos (Código | Descripción | Cantidad | Observación); Diagnóstico; Historial (Fecha | Turno | Hora | Médico | Registrado por | Nota | Tipo asignación | Estado); Adjuntos digitales.
- **Flujos y reglas inferidas**:
  - Estados del turno {CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}.
  - Cancelar exige motivo; "Cancelado reprogramación" distingue cancelación por reprogramación; "Asignada por BOT" indica canal BOT.
  - Activar y facturar siguen al pago/recibo (inferido).

## Turno Rayos X (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaRayosx.aspx)
- **Propósito**: asignar y gestionar turnos para toma de rayos X e imágenes diagnósticas por jornada. Reutiliza casi por completo la pantalla "Turnos laboratorio" (abajo); sólo se documentan las diferencias. El título de la ventana sigue siendo "Turno Urgencia" (plantilla compartida, inferido).
- **Diferencias frente a Turnos laboratorio**:
  - Tipo de cita {RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS}.
  - No tiene: filtro "Estado del estudio", botón "Nuevo Estudio", Gestante, hora de turno, subtipo RPMS, ventana "Ingresos del paciente" / "Agregar fórmula" / "Relacionar ingreso", visor y descarga de imagen, ni el generador de consentimiento informado con datos biométricos (sólo aparece una ventana "Concentimiento" sin extraer).
  - Sí tiene: botón Trazabilidad y ventana "Eliminar cita" con Motivo; botones "Nuevo Médico" y "Nueva IPS" junto a Médico remite / IPS que emite; ventana "Imagen adjunta"; sección "Nuevo soporte" en soportes digitales.
  - Grilla "Programación de turnos para toma de rayos x": Turno | Jornada | Turno | Documento | Paciente | Empresa | Régimen | Fecha asignación | Registrado por | Estado (sin Hora ni Médico/Entidad solicita).
  - Se mantiene Fecha + Agregar Jornada {TURNO 1..10} (nombre y número de pacientes), "Adicionar citas a la agenda" (número de citas), Recibo de pago, Enviar Copago a Dian (Resolución) y Gestión del paciente.
- **Flujos y reglas inferidas**: igual que laboratorio, sin ciclo de estados del estudio (toma/resultado); el estado es el del turno (inferido).

## Turnos laboratorio (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaUrgencia.aspx)
- **Propósito**: asignar y gestionar turnos de estudios de laboratorio por jornada. La página es la clase de urgencias reutilizada: la ventana se titula "Turno Urgencia" y conserva textos como "Eliminar Turno de Urgencia". Es muy parecida a "Turno procedimientos externos" (mismo bloque de paciente, ingreso, agenda, procedimientos, diagnóstico, adjuntos, historial).
- **Funcionalidades**:
  - El usuario puede buscar paciente (tipo y número de documento, nombre) o crear/editar paciente, y guardar, limpiar, cancelar.
  - Puede filtrar la grilla de programación por Fecha y por Estado del estudio {ASIGNADO, TOMA DE MUESTRA REALIZADA, TOMA DE MUESTRA PARCIAL, REGISTRO DE RESULTADO REALIZADO, REGISTRO DE RESULTADO PARCIAL, CON RESULTADOS COMPLETOS, RESULTADOS ENTREGADOS, ANULADO, RECHAZADO}; crear "Nuevo Estudio" y "Agregar Jornada" (Jornada {TURNO 1..10}, nombre, número de pacientes); ordenar y elegir columnas.
  - Sobre un turno: modificar cita (M), eliminar cita (Supr), ver nota de inasistencia, trazabilidad, imprimir cita, cancelar turno con Motivo + Observación; "Adicionar citas a la agenda" (número de citas).
  - Puede asignar procedimientos (búsqueda de CUPS con ventana "Cups encontrados") con cantidad y observación, "Agregar Procedimientos"/"Quitar de la lista"; agregar diagnóstico CIE10 (código/nombre, tipo {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}, prioridad).
  - Puede firmar ingreso (grilla Código | Descripción | Tipo manual), consultar los ingresos del paciente por rango de fechas y relacionar uno al turno ("Relacionar Ingreso", "Agregar Formula").
  - Puede asignar acudiente/acompañante y responsable (ventanas con documento, nombre, celular, teléfono, parentesco; "Traer datos responsable"), agregar médico externo (nombres, registro profesional, especialidad) e institución (NIT, nombre, estado {ACTIVO, INACTIVO}, departamento/municipio), y registrar datos laborales (fecha ingreso, tipo de examen médico, empresa contratante, empresa en misión, cargo).
  - Puede capturar foto, firma digital y huella (subir archivo / "Obtener firma"), traer datos biométricos del ingreso y generar el consentimiento informado (procedimiento, editor HTML, datos de paciente y de testigo/responsable con relación).
  - Puede gestionar adjuntos físicos (Administrativo, Clínico, Diligenciamiento de archivos; con descripción y archivo; visor con zoom, rotar, restablecer; descargar imagen en PNG o JPG) y adjuntos digitales (Categoría {ADMINISTRATIVO}, tipo de soporte, relación con el paciente).
  - Puede ver recibo de pago y enviar el copago a la DIAN (Resolución).
- **Datos**: Tipo afiliado ingreso (catálogo de afiliados); Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}; Prestador de servicio {PRORED ×4 sedes}; Categorías; Tipo programa especial {NO APLICA}; Equipo de atención; Tipo paciente; Unidad funcional {AMBULATORIO}; Grupo de servicio {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}; Servicios. Datos de la agenda: fecha que quería el paciente, fecha de solicitud, fecha de asignación, hora, número de citas {1..4}, Gestante {SI, NO}, Vía de ingreso (catálogo), Tipo de cita {LABORATORIO RPMS, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS} con subtipo RPMS, Tipo de asignación {PRESENCIAL, TELEFONICA}, Empresa (catálogo de empresas), Contrato, No. autorización, Observación.
- **Listados**: Programación de turnos para estudios de laboratorio: Turno | Hora | Documento | Paciente | Empresa | Régimen | Médico/Entidad solicita | Fecha asignación | Registrado por | Estado (hay una segunda grilla con Jornada en lugar de Hora, para la vista por jornada). Procedimientos (Código | Descripción | Cantidad | Observación); Diagnóstico (Código | Descripción | Prioridad); Historial (Fecha | Turno | Hora | Médico | Registrado por | Nota | Tipo asignación | Estado; con filtros por columna); Soportes digitales (Categoría | No. autorización | Tipo de soporte | Fecha de creación | Registrado por | PDF | Modificar | Eliminar).
- **Flujos y reglas inferidas**:
  - El ciclo del estudio (asignado, toma de muestra total/parcial, registro de resultado total/parcial, resultados completos, entregados; anulado o rechazado) se gestiona sobre el turno (inferido).
  - Un turno pertenece a una jornada (TURNO 1..10) de una fecha (inferido).
  - Cancelar y eliminar exigen motivo; el pago pasa por recibo y copago DIAN (inferido).

## OLD > Agenda Urología (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaUrologia.aspx)
- **Propósito**: agenda/turnos de consulta de urología (versión antigua; título interno "Turno Urgencia").
- **Funcionalidades**:
  - El usuario puede crear Nueva Cita, buscar paciente, crear paciente nuevo, actualizar datos del paciente.
  - Puede modificar turno, cancelar turno (motivo + observación en "Eliminar Turno de Urgencia"), guardar, actualizar.
  - Puede asignar acudiente, responsable, acompañante; agregar médico que remite y IPS que emite (nuevos); agregar procedimientos, diagnóstico CIE10; foto, firma y huella; datos laborales (medicina laboral).
  - Puede filtrar por fecha, hora y estado.
- **Datos**: Empresa/Prestador {PRORED ×4}; Tipo de cita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS}; Número de citas {1-4}; Tipo de asignación {PRESENCIAL, TELEFONICA}; Tipo afiliado (catálogo); Tipo de examen médico {PRE-INGRESO, PERIÓDICO, EGRESO, TRABAJO EN ALTURAS, MANIPULACIÓN DE ALIMENTOS, POST-INCAPACIDAD, CAMBIO DE OCUPACIÓN}; Estado de la cita {EN ESPERA, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO}; autorización, observación; institución (NIT, nombre, estado {ACTIVO, INACTIVO}, departamento/municipio); médico externo (nombres, registro profesional, especialidad).
- **Listados**: Programación de citas UROLOGÍA: Turno | Hora | Documento | Paciente | Empresa | Régimen | Médico/Entidad solicita | Fecha asignación | Registrado por | Estado. Historial de citas médicas (Fecha | Turno | Hora | Médico | Registrado por | Nota | Tipo asignación | Estado). Médico/Especialidad. Procedimientos; Diagnóstico.
- **Flujos y reglas inferidas**: flujo de sala de espera: EN ESPERA, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO o CANCELADO. Cancelar exige motivo. Pantalla "OLD" (inferido: reemplazada por la unificada).

## OLD > Asignación cita médica (/SUROSHistoriaClinica/Vistas/Privado/Agenda/AsignacionCitaMedica.aspx)
- **Propósito**: asignación de cita médica sobre agenda de profesional (versión antigua de la cita unificada).
- **Funcionalidades**: El usuario puede buscar/crear/modificar paciente, asignar/modificar/eliminar cita, cambiar de turno, transferir cita y asignar cita de transferencia, imprimir, asignar turno, eliminar cita opcional, ver nota de inasistencia, activar cita, volver a asignado, ver Escala de Caídas, cambiar fecha de la agenda, transferir agenda a otro médico, activar toda la agenda, adicionar citas a la agenda; seleccionar especialidad, médico y mes/año; tomar foto, firmar, huella, CIE10, procedimientos, adjuntos, médico externo e institución, recibo de pago.
- **Datos**: igual a Cita unificada en versión reducida: Prestador, Tipo de consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}, paciente (edad, nacimiento, género, afiliado, cotizante, empresa, municipio, dirección, celular), Tipo de cita (catálogo completo), Subsidio RPMS, Responsable, Gestante (checkbox), Número de citas, Tipo de asignación, Autorización, Empresa, Contrato, Institución/Médico que remite, Observación, datos laborales; Eliminar: Motivo + Observación; Cambio de turno: Jornada + Turnos disponibles.
- **Listados**: Citas programadas: AGCI ID | Jornada | Hora | Turno | Documento | Nombre paciente | Tipo cita | Empresa | Régimen | Medio solicitud | Fecha asignación | Registrado por | Estado. Lista de médicos; Turnos; Historial de citas médicas.
- **Flujos y reglas inferidas**: igual a Cita unificada; incluye "Escala de Caídas" (valoración de riesgo, contenido no visible).

## OLD > Gestiona turno urgencia (/SUROSHistoriaClinica/Vistas/Privado/Agenda/TurnoUrgencias.aspx)
- **Propósito**: registrar el ingreso/turno de urgencias, con triage, signos vitales, remisión y eventos de accidente.
- **Funcionalidades**:
  - El usuario puede buscar paciente y crearlo/actualizarlo, nuevo ingreso, guardar, limpiar, cancelar.
  - Puede marcar "Sin contrato", seleccionar modo de ingreso, asignar acudiente, agregar procedimientos (búsqueda por código/nombre), observación, gestante y labor de parto.
  - Puede registrar datos del prestador que remite (lugar y código de remisión), crear empresa (NIT, dirección, email, teléfono, código entidad, régimen, plan único de cuentas, departamento/municipio).
  - Puede registrar accidente de tránsito, trabajo informal u otro accidente (ventanas "Datos de accidente" y "Datos de otros accidentes laborales informales").
  - Puede agregar signos vitales, firmar cita, adjuntar archivos, foto, firma y huella.
  - Puede cancelar turno (motivo + observación) y modificar turno; ver trazabilidad; buscar por paciente y fecha.
  - Puede definir destino de enfermería {HOSPITALIZACIÓN} (unidad funcional).
- **Datos**:
  - Ingreso: Prestador {PRORED ×4}; Empresa (catálogo), Contrato, Tipo afiliado (catálogo), cotizante; Modo de ingreso {URGENCIAS, CONSULTA EXTERNA O PROGRAMADA, REMITIDO, NACIDO EN LA INSITUCIÓN}; Gestante; Labor de parto {SI, NO}; observación urgencia.
  - Accidente (tránsito/evento): condición del accidentado, naturaleza del evento, tipo de evento, fecha, hora, dirección, zona {RURAL, URBANO}, características.
  - Otros accidentes laborales: ocupación habitual, jornada de trabajo habitual, desplazado {SI, NO}, fecha/hora accidente, ¿realizaba labor habitual? {SI, NO}, tipo de accidente, tipo de lesión, sitio donde ocurrió, descripción de lesión, objeto de la lesión, parte del cuerpo afectada.
  - Signos vitales: tensión (sist/diast), frecuencia cardiaca, frecuencia respiratoria, saturación de oxígeno, glucometría, perímetro encefálico, fetocardia, temperatura, peso, talla, IMC, M2.
  - Cancelación: Motivo + Observación.
  - Filtros: Lista de estados {EN ESPERA, ATENCIÓN TRIAGE, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO, NO ASISTIO}.
- **Listados**: Turnos Urgencia: Turno | Fecha asignación | TD | Documento | Nombre | Celular | Empresa | Acudiente | Observación | Código | Contrato | Anexo. Procedimientos (Código | Procedimiento). Lista de adjuntos.
- **Flujos y reglas inferidas**: EN ESPERA, ATENCIÓN TRIAGE, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO; salidas CANCELADO y NO ASISTIO. Cancelar exige motivo. Los eventos de accidente (tránsito/trabajo informal) generan datos para reportes de aseguramiento (inferido, SOAT/ARL por catálogo de afiliados).

## OLD > Cita demanda inducida (/SUROSHistoriaClinica/Vistas/Privado/Agenda/CitaDemandaInducida.aspx)
- **Propósito**: versión antigua de la cita unificada para demanda inducida.
- **Funcionalidades**: igual a Cita médica unificada, sin notificación masiva WhatsApp, sin historial de laboratorio ni envíos: guardar, limpiar, cancelar; no realizó consulta; atendido en otra institución (institución, fecha, observación); registrar laboratorio y procedimiento externo; cambiar fecha de agenda, transferir agenda, activar toda la agenda; asignar/modificar/eliminar/cambiar turno/transferir/imprimir cita; activación, volver a asignado, trazabilidad, firmar ingreso; subir laboratorios; signos vitales; consentimiento informado; foto, firma, huella; CIE10; adjuntos.
- **Datos**: Mismos que Cita unificada; adicional "EPS afiliado" en datos del responsable/acompañante; selección de jornadas {TURNO 1..10}; Programa Res. 3280.
- **Listados**: Citas de la agenda: Jornada | Hora | Turno | Documento | Nombre paciente | Tipo cita | Empresa | Régimen | Medio solicitud | Lugar de residencia | Fecha asignación | Registrado por | Estado. Citas médicas del paciente: Descripción | CUPS | Fecha | Hora | Tipo cita | Registrado por | Médico | Tipo consulta | Estado | Factura.
- **Flujos y reglas inferidas**: igual a unificada; "Eliminar cita" exige motivo y observación.

## OLD > Malla Reumatología (/SUROSHistoriaClinica/Vistas/Privado/Agenda/MallaReumatologia.aspx)
- **Propósito**: construir y agendar la malla (plan periódico) de atenciones multidisciplinarias de pacientes de reumatología.
- **Funcionalidades**:
  - El usuario puede consultar pacientes por rango de fechas, especialidades (multi) y empresas (multi).
  - Puede crear nueva malla, agregar paciente a la malla (buscar), guardar, terminar y guardar, descartar malla.
  - Puede ver historial de mallas creadas y abrirlas en el visor.
  - Puede registrar cita médica desde la malla con fecha de agendación de citas.
- **Datos**: Fecha inicial, Fecha final, Fecha agendación de citas; Especialidades {PSICOLOGÍA, NUTRICIÓN, FISIOTERAPIA, TERAPIA OCUPACIONAL, REUMATOLOGIA, MEDICAMENTOS, ENFERMERÍA}; Empresas {TODOS, PIJAOS SALUD E.P.S.I (SUBSIDIADO), PARTICULAR (OTRO), ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA (OTRO), ASMET SALUD EPS SAS (SUBSIDIADO), ASMET SALUD EPS SAS (CONTRIBUTIVO)}.
- **Listados**: Listado de pacientes reumatología: # Paciente | Fecha de atención reumatología | Empresa | Documento | Nombre | Apellido | Residencia | Departamento. Historial de mallas: # | Usuario registra | Fecha de creación | Estado | Acciones.
- **Flujos y reglas inferidas**: la malla pasa por borrador (Guardar) y finalizada ("Terminar y Guardar"), o descartada (inferido); al finalizar se agendan citas por especialidad según periodicidad (ver "Configuración malla reumatología" en Cita unificada).

---

## Entidades y estados del módulo

**Bloques comunes**: Paciente (tipo/num. documento, nombre, nacimiento, edad, género, tipo de afiliado, cotizante, empresa, municipio, dirección, celular, teléfono); Responsable/Acudiente/Acompañante (documento, nombre, teléfono, parentesco, EPS afiliado); Médico externo (nombres, apellidos, registro profesional, especialidad); Institución remitente (NIT, nombre, estado ACTIVO/INACTIVO, departamento, municipio); datos biométricos (foto, firma digital, huella); datos laborales (fecha ingreso, tipo de examen, empresa contratante, empresa en misión, cargo).

| Entidad | Atributos principales |
|---|---|
| Agenda (programación) | id, fecha, hora inicial/final, descripción, profesional principal, auxiliar, tiempo de atención, turnos creados/asignados, jornada, programada por, convenio, consultorio (interno/externo), prestador, modalidad, categoría, nivel de complejidad, equipo, zona, unidad funcional, grupo de servicio, servicio, eliminada (lógica) |
| Franja / Turno | turno, hora, estado, canal (normal, BOT App/Web, BOT App, Demanda Inducida), tipo de activación (Por Defecto, Prioritaria), bloqueo (tipo, causa) |
| Cita | id (AGCI), jornada, hora, turno, paciente, tipo de cita, tipo de asignación, medio de solicitud, empresa, contrato, régimen, no. autorización, fechas (solicitud, deseada, asignación), vía de ingreso, gestante, registrado por, estado, sede, nota, factura, CUPS |
| Autorización / Recepción | id, fecha, paciente, institución y médico que remite, especialidad, diagnóstico, estado, estado asignación, origen, servicio, programa PYP, estado recepción, WhatsApp, visado, asignado por, adjuntos, notas, clasificación CUPS |
| Turno procedimiento externo | turno, sede, fecha asignación, paciente, empresa, acudiente, tipo y procedimientos, médico que atiende, contrato |
| Turno urgencias | turno, paciente, empresa, acudiente, observación, código, contrato, anexo, modo de ingreso, remisión, signos vitales, datos de accidente |
| Llamada (bitácora) | prestador, paciente, teléfono, contestó (paciente/otra persona), hora, motivo, receptor, parentesco, nota, bill_id |
| Campaña WhatsApp / Mensaje | campaña, plantilla, fecha, total/enviados/entregados/leídos/fallidos; mensaje: paciente, teléfono, estado, fecha envío, WhatsApp ID |
| Malla reumatología | #, usuario registra, fecha creación, estado, pacientes, especialidades, periodicidad por mes |
| Adjunto | categoría, tipo de soporte, no. autorización, fecha creación, registrado por, archivo/PDF |
| Procedimiento (CUPS) | código, descripción, tipo manual, cantidad, cantidad ejecutada, observación, clasificación general/específica |
| Diagnóstico (CIE10) | código, descripción, tipo, prioridad |
| Nota | texto, fecha, hora |

**Catálogos y estados**:
- Prestador: PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA.
- Jornada: TURNO 1 a TURNO 10.
- Modalidad: INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN.
- Tipo de cita (consulta): PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA. Procedimientos externos: PROCEDIMIENTO EXTERNO, CITOLOGIA, PLANIFICACIÓN, VACUNACION.
- Tipo de asignación: PRESENCIAL, TELEFONICA (+ INTERNET en autorizaciones).
- Estados de turno de procedimientos: CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT.
- Estados de urgencias: EN ESPERA, ATENCIÓN TRIAGE, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO, NO ASISTIO.
- Estados de cita urología (old): EN ESPERA, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO.
- Estado de recepción de autorización: Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta.
- Estado de terapias: ASIGNADO, PENDIENTE, ATENDIDO, CITA CANCELADA, CANCELADA SIN CITA.
- Estado de mensaje WhatsApp: En cola, Enviado, Entregado, Leído, Fallido.
- Tipo de bloqueo: Por IPS, Por Médico. Tipo de activación: Por Defecto, Prioritaria.
- Tipo de diagnóstico: CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA.
- Tipo de afiliado: ver lista en Recepción autorizaciones (12 valores).
- Empresas (EPS/pagadores): PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO.
- Programa especial: NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD.
- Motivo de llamada: Demanda inducida, Entrega de medicamentos, Educacion, Revision de ayudas diagnosticas.
- Grupo de servicio: CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA.
- Tipo de examen médico (laboral): PRE-INGRESO, PERIÓDICO, EGRESO, TRABAJO EN ALTURAS, MANIPULACIÓN DE ALIMENTOS, POST-INCAPACIDAD, CAMBIO DE OCUPACIÓN.
- Categoría de adjunto: ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS.

## Preguntas abiertas
- Valores y transiciones exactos del estado de cita y de franja (la grilla muestra "Estado" sin catálogo) y quién puede ejecutar cada transición.
- Permisos por rol/perfil y por sede para bloquear, activar para BOT/Demanda Inducida, transferir agendas, eliminar, visar y convertir recibos a electrónicos.
- Reglas de negocio de asignación: validación de autorización/contrato/vigencia, límites de citas por día, tope de 4 citas, cuándo aplica PRIMERA VEZ vs CONTROL, copago/cuota moderadora y cuándo se exige.
- Integraciones: BOT App/Web (cómo reservan franjas, prioridad), proveedor de WhatsApp (plantillas, webhooks de entrega/lectura), DIAN (copagos y facturación electrónica), dispositivos de firma/huella/foto, y registros RIPS/Res. 3280.
- Contenido de la ventana "Concentimiento" de Turno Rayos X, cómo se relaciona el estado del estudio de laboratorio con el módulo de laboratorio, de la grilla de historial de llamadas de la bitácora, y relación real entre pantallas OLD y la unificada (qué sigue en uso).
