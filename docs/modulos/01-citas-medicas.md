# Citas médicas

Módulo que gestiona la programación de agendas médicas (por profesional, jornada/turno y sede), la asignación de citas y turnos a pacientes (consulta, procedimientos externos, urgencias, demanda inducida, laboratorio/rayos X), la recepción y visado de autorizaciones, y la bitácora de llamadas de contacto. Incluye canales de agendamiento por BOT App/Web y notificaciones por WhatsApp.
Actores inferidos: administrador/programador de agenda, auxiliar de admisiones/citas, personal de autorizaciones, gestor de demanda inducida, médico/auxiliar asignado a agenda, paciente (vía BOT App/Web).
Entidades principales: Agenda (programación), Franja/Turno, Cita, Paciente, Autorización/Orden, Procedimiento (CUPS), Diagnóstico (CIE10), Empresa/Contrato (EPS), Adjunto, Llamada de bitácora, Campaña WhatsApp, Malla de reumatología.

Todas las pantallas comparten (confirmado en código: `SelecCIE10`, `AsignaAcudiente`, `AsignaResponsable`, `PrepararInstitucion`, repetidas en Recepción, Laboratorio y pantallas OLD) un bloque común: búsqueda de paciente por documento/nombre, creación/edición de paciente, datos de responsable/acudiente/acompañante, foto/firma/huella digital, adjuntos físicos y digitales, CIE10, procedimientos, datos laborales (medicina laboral), "Firmar ingreso", "Recibo de pago" y "Enviar Copago a Dian". Se documentan una vez en "Bloques comunes" al final de las entidades.

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
  - Cada franja tiene estado (valores no listados) y canal: normal, BOT App/Web, BOT App, Demanda Inducida; una franja se "activa" para un canal y puede bloquearse (confirmado en código: `renderDescripcionAgenda`, `prepareCommandsBot`; ver Hallazgos).
  - Bloquear exige tipo (por IPS o por médico) y causa.
  - La eliminación de programación es lógica (existe filtro para mostrar eliminadas) (confirmado en código: `LAM`/`LAMTELEMEDICINA` reciben el flag `ELIMINADOS`).
  - Existen versiones "BOT App/Web" y "BOT App" de las mismas ventanas; no dependen de la sede sino del tipo de bloqueo de la agenda: `AGME_ESTADO` 2 = "Bloqueda para BOT App/Web" y 3 = "Bloqueda para BOT App" (corregido según código: `renderDescripcionAgenda`).


**Hallazgos del código**
- Guardar (`GuardarAgenda`, `ValidarAgenda`): "Es obligatorio definir la hora final (Hora fin) para guardar la programación de la agenda.", "Es obligatorio seleccionar el tipo de atención para guardar la programación de la agenda.", "La duración de la cita debe ser múltiplo de 5 minutos." La validación de que el intervalo sea divisible exactamente por la duración está comentada (no se aplica).
- Requeridos con aviso: "Seleccione los dias de la programación", "Ingrese una observación de la agenda para continuar.", "No se ha definido la hora final de la agenda", "Es necesario seleccionar una jornada para continuar.", "Es necesario seleccionar una unidad funcional.", "Es necesario seleccionar un grupo servicio.", "Es necesario seleccionar un servicio.", "Es necesario seleccionar una sede valida." Guardar/Cancelar quedan deshabilitados hasta completar todo (`ValidarEstadoBotones`); se exige médico seleccionado salvo cuando Tipo de atención = 2 (agenda por especialidad, sin médico; `GANEspecialidad`, `CAMESPE`, `LAMTELEMEDICINA`).
- Confirmaciones: "Realmente desea guardar la agenda del médico?", "Realmente desea modificar la agenda del médico?", "Realmente desea activar la programación de la agenda?".
- Métodos de servidor: `GAN` (guardar por médico), `GANEspecialidad`, `CAM`/`CAMESPE` (consultar calendario), `LAM`/`LAMTELEMEDICINA` (listar programaciones), `MAM` (modificar), `AOA` (activar), `EAM` (eliminar), `ObtenerResumenTurnosAgenda`. Combos en cascada: Modalidad -> `CategoriaModalidadAtencion` -> `CargarTipoProgramaEspecial` -> `CargarEquipoAtencion`.
- Estado BOT: `AGME_ESTADO` 2 = "(Bloqueda para BOT App/Web)", 3 = "(Bloqueda para BOT App)" (sic). Cada franja tiene `ACTIVADA` 1/0 (alterna Activar/Desactivar) y `CITABLOQUEADA` 1/0 (alterna Habilitar/Deshabilitar). Los menús de bloqueo/gestión BOT sólo se ofrecen si la agenda no es de un día pasado; si lo es, se muestra el resumen de turnos.
- Al crear agendas busca citas con visado pendiente y abre "Citas con Visado Pendientes - N encontradas" (ordenadas por mes futuro de revisión); "Debe seleccionar al menos una cita para importar." y `ProcesarCitasConVisado` las asigna a las agendas nuevas (así se vincula el visado de Recepción con la agenda).

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
  - Estados de cita (parcialmente confirmado en código: `VolverEstadoAsignado` -> `VAA` revierte a asignado; `CargarTurnosA` usa TIAG 1 = "Cambio de turno" y 2 = "Asigna turno activo"): asignado, activado, atendido, cancelado/eliminado, "volver a asignado" revierte estado; transferir y "asignar cita de transferencia" son un par (origen/destino) (inferido).
  - Eliminar cita exige Motivo y Observación.
  - Cambio de turno: elegir jornada y turno disponible de la misma agenda.
  - Cita de laboratorio tiene ciclo asignación, toma, entrega.
  - Las citas se limitan a 1-4 por asignación.
  - Medicina laboral requiere datos laborales; reumatología requiere flag de primera vez y malla.
  - Atajos de teclado: M, Supr, C, T, P.
  - Envío de WhatsApp excluye a pacientes sin celular válido (la UI los lista aparte).
  - El flujo "Demanda inducida" busca contactar al paciente para agendar; "No realizó consulta" y "Atendido en otra institución" cierran el seguimiento (inferido).


**Hallazgos del código** (Cita unificada)
- Servidor: `ValidarCopagoPaciente`, `ConsultarProcedimientosCita`, `RegistrarPeriodicidad`, `ObtenerFirmaPaciente`, `ObtenerFirmaAcudienteConcentimiento`, `TraerResponsable`, `CargarProcedimientosIngreso`, `BusProceidmienstosOrden`, `AgrgarAlStoreProcedimiento`, `FacturaElectronica`.
- Mensajes: "El diagnostico con codigo CIE10 X ya esta en la lista.", "Esta seguro de eliminar el procedimiento?", "Está seguro de agregar estos procedimientos?", "Está seguro de activar la cita?", "Es necesario que escriba un parametro de busqueda.".
- WhatsApp masivo: "Seleccione al menos un paciente con celular válido para continuar.", "Seleccione una plantilla para continuar.", "Seleccione al menos un paciente para enviar.", "Seleccione una plantilla para enviar.", "No se identificó la agenda del médico. Vuelva a abrir el asistente desde "Registrar citas"."; el paso final muestra enviados, fallidos y detalles (`EnviarMasivoWhatsAppAgenda`, `CargarAsistenteWhatsAppMasivo`, `CargarHistorialWhatsAppMasivo`). Al guardar una cita con plantilla configurada el envío es automático y SIN confirmación (`enviarWhatsAppCitaDemandaInducida` -> `EnviarWhatsAppPlantillaApi`; los errores sólo van a consola). El envío manual abre wa.me con prefijo 57; sin teléfono: "El contacto no tiene número de teléfono registrado para WhatsApp."
- Signos vitales y laboratorios previos a la consulta (`CalcIMC`, `GuardarLaboratoriosPreConsulta`): IMC = peso / talla^2 x 10000 (talla en cm); "M2" = peso x 4 + 7 (sólo el numerador de la fórmula de superficie corporal); clasificación: <16 Delgadez severa, 16-16,99 moderada, 17-18,49 aceptable, 18,5-24,9 Normal, 25-29,9 Preobeso, 30-34,9 Obeso I, 35-39,9 Obeso II, >=40 Obeso III. Al guardar, la saturación de oxígeno se envía fija en 95.
- El JS de esta pantalla no contiene `RegCita`: las validaciones de guardado de la cita no están en el cliente (están en servidor o código compartido).

## Activación de cita (/SUROSHistoriaClinica/Vistas/Privado/ActivacionCita/ActivacionCita.aspx)
- **Propósito**: activar (confirmar la llegada/pago) las citas pendientes de un paciente y emitir el recibo de caja.
- **Funcionalidades**:
  - El usuario puede buscar paciente por documento/nombre y ver su identificación, género, nombre, fecha de nacimiento, empresa, régimen, zona y municipio de residencia.
  - Puede mostrar todas las citas o actualizar pendientes.
  - Puede agregar copago autorizado (credenciales de usuario/contraseña; confirmado en código: `VP` exige ambas y valida con `HE`; que sea autorización de supervisor sigue siendo inferido) y agregar recibo de pago.
  - Puede imprimir recibo de pago y convertirlo a electrónico (facturación electrónica).
  - Puede enviar copago a la DIAN con resolución.
  - Puede firmar el ingreso (firma por teléfono, obtener firma/link, subir archivo, huella), tomar datos biométricos, generar consentimiento.
  - Puede editar datos del paciente, asignar responsable/acudiente/acompañante, adjuntar soportes, agregar diagnóstico CIE10 y procedimientos, agregar médico externo e institución.
  - Puede guardar y cerrar, imprimir.
- **Datos**: mismo bloque de cita que Cita unificada (agenda, fechas, vía de ingreso, tipo de cita, tipo de asignación, empresa, contrato, autorización, orden médica, datos laborales). Recibo de caja: concepto, valores, información de caja. Ingreso de credenciales: nombre de usuario, contraseña.
- **Listados**: Citas pendientes (ID | Código | Procedimiento/Profesional ×2); Recibo de caja (Concepto | Valores | Información caja); Diagnóstico; Procedimientos; Adjuntos físicos y digitales.
- **Flujos y reglas inferidas**:
  - Activar en esta pantalla = seleccionar la cita pendiente: `selectionChanged` llama a `CambiarEstadoCitaFacturada` y abre el módulo Facturador (corregido según código: `selectionChanged`; la activación está ligada a la facturación de la cita, no a un cambio de estado manual tras firma).
  - El copago requiere autorización con credenciales (confirmado en código: `VP`/`HE`).
  - El recibo puede convertirse a factura electrónica y reportarse a la DIAN.


**Hallazgos del código** (Activación de cita)
- Búsqueda de paciente: "Es necesario que escriba un parámetro de búsqueda." (`CP`; CIE10 con `CONS`).
- Doble clic en una cita abre `WinOPcionesCopago`; clic simple lista recibos de la cita (`ListarReciboPagoPorCita`). `GuardarRecibo(PENDIENTEPAGO)` envía caja, concepto, cantidad, valor, total a pagar, forma y medio de pago, total pagado, saldo, categoría de afiliación y el flag `COBRAR`, es decir permite guardar el recibo como pendiente de pago (`GuardarReciboPago`).
- Seleccionar una cita pendiente abre la pestaña FACTURADOR según `TIPOAGENDA` ("LABORATORIO CLINICO", "AGENDACITA", "PRO EXTERNO", "RAYOS X") y marca la cita como facturada (`CambiarEstadoCitaFacturada`). Si ya está abierto: "El módulo de Facturador esta abierto. Es necesario cerrarlo para facturar nuevamente".
- Credenciales de copago: "Ingrese usuario." / "Ingrese contraseña." y validación en servidor (`HE`).
- DIAN: `CargarDianCopago` abre la ventana de envío; `ConvertirDian` llama a `FacturaElectronica` (copago, tipo de agenda, id de agenda, parámetro de factura). La opción de menú "cambiar tipo de factura" sólo aparece si `ENVIARCOPAGODIAN == 1`. La anulación de recibo ("Realmente desea cancelar el copago?", `CancelarReciboPago`) está comentada.
- Firma: la página incluye el SDK de tableta Wacom (`tabletDemo`, `disconnect`, etc.).

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
  - Ciclo de recepción (confirmado en código: `abrirVentanaEstadoRecepcion`, `guardarEstadoRecepcionAutorizacion`): llega orden, se revisa y se marca {Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta} (por defecto "En Verificación"); opcionalmente se notifica al paciente por WhatsApp con ese estado. El mismo campo admite además "Prioritaria" y "Control" (`marcarEstadoPrioritario`, `marcarEstadoControl`).
  - Visado: autorización validada con fecha de futura revisión y tipo de cita; luego se asigna/reasigna cita.
  - Estado de asignación: pendiente vs asignado; reasignar/reprogramar exige razón; eliminar exige motivo.
  - Se puede marcar prioridad o convertir a control; la clasificación CUPS se corrige con justificación obligatoria (confirmado en código: `guardarCambiosClasificacionCUPS`).
  - Origen del registro incluye canal (app Surós/BOT, manual) (confirmado en código: `generarMensajeCancelacionCita` habla de "cita médica solicitada a través de la app Surós" y usa `OTPA_CODE`; WhatsApp como origen no se ve en el JS).


**Hallazgos del código**
- Consulta: "Seleccione un rango de fechas (inicio y fin) para consultar.", "La fecha fin no puede ser menor que la fecha inicio.", "El rango máximo permitido es de N meses. Ajuste la fecha de inicio o de fin." (N = `AUT_MAX_MESES_RANGO`, definido fuera del JS). Atajos Hoy/Este mes/Esta semana; se carga una base (`CargarBaseAutorizaciones`) y el filtro Pendientes/Asignados se hace en memoria (`FiltrarAutorizacionesEnMemoria`); interruptores "Ver eliminados" y "Ver todos los estados".
- Agregar orden (`validarCamposRequeridosRecepcion`): "Campos obligatorios faltantes:" Prestador de servicio, Especialidad, Empresa, Contrato, "Diagnóstico (al menos uno)". Además: "Por favor Seleccione el tipo de cita!", "Por favor Seleccione el tipo de asignación!", "Por favor Ingrese un procedimiento!", "Diligencie los campos obligatorios resaltados en rojo por favor.", "Ingrese el registro médico para continuar", "Ingrese la especialidad médica para continuar". Confirma "Está seguro de crear un nuevo registro?" / "Está seguro de modificar el registro?" y "Está seguro de limpiar el formulario?"; guarda con `GuardarAutorizacion`.
- Estado de recepción: sin selección "Debe seleccionar un estado"; `ActualizarEstadoRecepcionAutorizacion(cita, estado, enviarWhatsApp, mensaje, contacto)`; si se marca enviar, abre WhatsApp con enlace wa.me (`abrirChatWhatsApp`, prefijo 57) con una plantilla por estado (`plantillaMensajeEstado`: Aceptada = solicitud incluida en lista de espera para asignación; Rechazada = no cumple requisitos de validación; En verificación; Archivo dañado; Foto incompleta) o el texto por defecto "Información de su autorización: estado de recepción "X".".
- Prioritaria/Control: "¿Está seguro de marcar esta cita como PRIORITARIA?" / "¿Está seguro de marcar esta cita como CONTROL?" -> "Estado cambiado a PRIORITARIA." / "Estado cambiado a CONTROL." (mismo método de estado de recepción).
- Visado (`GuardarVisado`): guarda fecha futura de revisión (AAAA-MM-DD), tipo de cita y observación; `FiltrarMesesVisado` impide años y meses pasados; sin datos: "No hay información de visado para este registro."
- Asignar cita (`registrarCita`): "Ingrese un valor válido" si falta la cantidad de terapias; cantidad = valor opcional o terapias; abre la pestaña "ASIGNACION CITA MEDICA" (CitaDemandaInducidaUnificada.aspx) o, si la especialidad es "LABORATORIO CLINICO", "AGENDA LABORATORIOS" (TurnoInstanciaUrgencia.aspx). Terapias con fecha, hora final, número y médico: `RegistrarCitaAutorizacion`.
- Reasignar: nota obligatoria, se guarda en mayúsculas (`GuardarNotaReasignacionCita`); sin ella "Es necesario llenar los campos requeridos en el formulario para continuar."
- Eliminar: el servidor decide si es válido (`ValidarEliminacionCita(fecha, hora)`); si no, "Aviso" con el mensaje devuelto. Tras eliminar, notifica por WhatsApp sólo si la sección `WhatsApp_Encendido_EliminarCitaRecepcion` está habilitada (`ValidarConfigWhatsAppAccion`); avisos "La seccion de eliminacion de cita no tiene una plantilla configurada." y "El paciente no tiene numero de telefono para WhatsApp."
- Mensajes a pacientes del BOT: la cancelación dice que la cita "solicitada a través de la app Surós" fue cancelada porque al validar no registra servicios activos, incluye sede, médico, especialidad, fecha, hora y "Código OTP" (para trazabilidad) y recomienda verificar la afiliación con la EPS; la confirmación usa la plantilla `CONFIRMACION_AGENDAMIENTO_RECEPCION` (`GenerarMensajeWhatsAppPlantilla`).
- Clasificación CUPS (`guardarCambiosClasificacionCUPS` -> `ActualizarClasificacionCUPSBatch`): "No hay procedimientos cargados para actualizar", "Debe seleccionar la clasificación general para el código: X", "Debe seleccionar la clasificación específica para el código: X", "Debe ingresar la justificación del cambio para el código: X", "No se detectaron cambios para guardar".
- Otros servidores: `GenerarExcel` (exportar), `CargarDatosBusquedaAvanzada`, `BuscarRPMS`/`CargarProgramasSeleccionados` (programas), `RevisarRefrescoDesdeLaboratorios` (refresco cuando laboratorio cambia).

## Bitácora demanda inducida (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Bitacora/Bitacora.aspx)
- **Propósito**: registrar y consultar las llamadas de contacto a pacientes (demanda inducida, entrega de medicamentos, educación, ayudas diagnósticas).
- **Funcionalidades**:
  - El usuario puede buscar paciente (nombre/documento), seleccionar prestador y área que genera, y agregar/quitar teléfonos de contacto.
  - Puede registrar una llamada: contestó paciente u otra persona, hora, motivo, receptor, parentesco, nota y respuesta del usuario; guardar, actualizar o cancelar la actualización.
  - Puede usar plantillas de nota/observación: crear, editar, eliminar, guardar ítems en plantilla y cargar plantilla ("Mis plantillas").
  - Puede consultar historial de llamadas filtrando por Rango de fecha, Paciente o Todo, con prestadores múltiples; exportar a PDF y a Excel.
  - Puede imprimir formatos (carta o tirilla, selección por ítem), editar y eliminar registros.
- **Datos**: Prestador de servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}; paciente (nombre, documento, id persona); Área que genera; Teléfono; Contestó paciente / Otra persona (radio); Hora de llamada; Motivo de llamada {Demanda inducida, Entrega de medicamentos, Educacion, Revision de ayudas diagnosticas}; Receptor de la llamada; Parentesco {MAMÁ, PAPÁ, HIJO(A), TIO(A), ABUELO(A), PRIMO(A), SOBRINO(A), ESPOSO(A), OTRO, HERMANO(A)}; Nota; BILL_ID (identificador del registro de llamada/nota, no una factura; corregido según código: `GridCommand`, junto a `BILL_OBSERVACION`, `BILL_RECEPTORLLAMADA`); Filtros: Filtrar por, Fecha inicial/final.
- **Listados**: Teléfonos del paciente (Teléfonos | Quitar); Historial de llamadas (columnas no extraídas); Ítems de impresión (Descripción | Carta | Tirilla); Plantillas (Descripción).
- **Flujos y reglas inferidas**: cada llamada deja constancia de a quién se contactó (paciente u otra persona + parentesco). Las plantillas son personales ("Mis plantillas") (inferido). Imprimir formatos permite carta o tirilla.


**Hallazgos del código**
- Bitácora (`Bitacora.aspx`): obligatorios siempre paciente, hora de llamada, motivo y observación; si contestó otra persona también nombre del receptor y parentesco (`ComposObligatorioDinamicos`); sin formulario válido o sin teléfonos: "El formulario es incorrecto o la lista de contactos es vacia." Los teléfonos se guardan en la persona (`RegistrarTelefonos`); quitar pide "¿Esta seguro de eliminar este telefono?". Un registro es nota simple (sólo `BILL_OBSERVACION`) o llamada completa (con `BILL_RECEPTORLLAMADA`; parentesco informado = contestó otra persona). Eliminar registro NO pide confirmación (`EliminarRegistroBitacora`) y el botón se oculta si `puedeEliminar` es falso. Excel: "Por favor, primero haga la consulta". Imprimir (`COI`) abre pestañas Carta y Tirilla. Rango de fechas oculto para filtros Paciente y Todo. Se abre también desde la malla de reumatología (`BuscarPacienteMalla`).

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


**Hallazgos del código** (Turno procedimientos externos)
- El JS propio de la página es mínimo (`ActualizaLista`); el resto es servidor y clase base.

## Turno Rayos X (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaRayosx.aspx)
- **Propósito**: asignar y gestionar turnos para toma de rayos X e imágenes diagnósticas por jornada. Reutiliza casi por completo la pantalla "Turnos laboratorio" (abajo); sólo se documentan las diferencias. El título de la ventana sigue siendo "Turno Urgencia" (plantilla compartida; confirmado en código: usa `UpdateCancelarTurnoUrgencia`).
- **Diferencias frente a Turnos laboratorio**:
  - Tipo de cita {RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS}.
  - No tiene: filtro "Estado del estudio", botón "Nuevo Estudio", Gestante, hora de turno, subtipo RPMS, ventana "Ingresos del paciente" / "Agregar fórmula" / "Relacionar ingreso", visor y descarga de imagen, ni el generador de consentimiento informado con datos biométricos (sólo aparece una ventana "Concentimiento" sin extraer).
  - Sí tiene: botón Trazabilidad y ventana "Eliminar cita" con Motivo; botones "Nuevo Médico" y "Nueva IPS" junto a Médico remite / IPS que emite; ventana "Imagen adjunta"; sección "Nuevo soporte" en soportes digitales.
  - Grilla "Programación de turnos para toma de rayos x": Turno | Jornada | Turno | Documento | Paciente | Empresa | Régimen | Fecha asignación | Registrado por | Estado (sin Hora ni Médico/Entidad solicita).
  - Se mantiene Fecha + Agregar Jornada {TURNO 1..10} (nombre y número de pacientes), "Adicionar citas a la agenda" (número de citas), Recibo de pago, Enviar Copago a Dian (Resolución) y Gestión del paciente.
- **Flujos y reglas inferidas**: igual que laboratorio, sin ciclo de estados del estudio (toma/resultado); el estado es el del turno (inferido).


**Hallazgos del código** (Turno Rayos X)
- Reutiliza la clase de laboratorio/urgencias: `UpdateCancelarTurnoUrgencia`, `GuardarJornada`, `EliminarJornada`, `AddCita`, `EC` (eliminar cita), `ValidarCopagoPaciente`, `FacturaElectronica`.
- Mensajes: "Realmente desea eliminar esta jornada?", "Ingrese un numero de citas valido para continuar.", "El rango de eliminación es mayor al numero de citas de la agenda, no puede continuar.", "Es necesario tener un paciente seleccionado para cargar el adjunto."

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
  - Un turno pertenece a una jornada (TURNO 1..10) de una fecha (confirmado en código: `PrepararJornada` envía JORNID, FECHA, NOMBREJORNADA y NUMEROPACIENTES a `GuardarJornada`).
  - Cancelar y eliminar exigen motivo (confirmado en código: `EliminaCita` valida el formulario con motivo antes de `EC`); el pago pasa por recibo y copago DIAN (inferido).


**Hallazgos del código** (Turnos laboratorio)
- Jornada: `PrepararJornada` -> `GuardarJornada` {jornada, fecha, nombre en mayúsculas, número de pacientes}; "Realmente desea eliminar esta jornada?" -> `EliminarJornada`. Comandos de grupo: agregar cita opcional, agregar turnos (ADD), eliminar turnos (DEL), eliminar jornada, transferir turno.
- Cancelar turno: "Realmente desea Cancelar el Turno seleccionado?" -> `UpdateCancelarTurnoUrgencia` (reutiliza la clase de urgencias).
- Mensajes: "Seleccione el formato, por favor." (consentimiento), "Es necesario tener un paciente seleccionado para cargar el adjunto.", "Ingrese un numero de citas valido para continuar.", "El rango de eliminación es mayor al numero de citas de la agenda, no puede continuar.", "Está seguro de agregar estos procedimientos?".
- Servidor: `ConsultaIngresos`, `CargarProcedimientosIngreso`, `BusProceidmienstosOrden` (procedimientos de la orden según contrato y empresa), `AgregarConsentimiento`, `GetPDF`, `ValidarCopagoPaciente`, `FacturaElectronica`.

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


**Hallazgos del código** (Urología OLD)
- Mensajes propios de `RegCita`: "Seleccione la empresa de ingreso.", "La cita es de tipo cirugia programada, es nesesario que registre los procedimientos.", "Por favor, seleccione el medico que remite.", "Por favor, seleccione la IPS que remite.", "Por favor, seleccione el tipo de diagnostico.", "Por favor, seleccione el tipo de examen médico.", "No es posible ingresar más de un diagnóstico", "Ingrese una persona para continuar." Servidor: `RC` (registrar cita), `RT`, `RD`, `CHD`, `ListaUrgencia`, `CargarAsignarCitaAutorizacion`, `GuardarInstitucion`.

## OLD > Asignación cita médica (/SUROSHistoriaClinica/Vistas/Privado/Agenda/AsignacionCitaMedica.aspx)
- **Propósito**: asignación de cita médica sobre agenda de profesional (versión antigua de la cita unificada).
- **Funcionalidades**: El usuario puede buscar/crear/modificar paciente, asignar/modificar/eliminar cita, cambiar de turno, transferir cita y asignar cita de transferencia, imprimir, asignar turno, eliminar cita opcional, ver nota de inasistencia, activar cita, volver a asignado, ver Escala de Caídas (abre la pestaña "ESCALA DE CAIDAS", `EscalaMorse`), cambiar fecha de la agenda, transferir agenda a otro médico, activar toda la agenda, adicionar citas a la agenda; seleccionar especialidad, médico y mes/año; tomar foto, firmar, huella, CIE10, procedimientos, adjuntos, médico externo e institución, recibo de pago.
- **Datos**: igual a Cita unificada en versión reducida: Prestador, Tipo de consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}, paciente (edad, nacimiento, género, afiliado, cotizante, empresa, municipio, dirección, celular), Tipo de cita (catálogo completo), Subsidio RPMS, Responsable, Gestante (checkbox), Número de citas, Tipo de asignación, Autorización, Empresa, Contrato, Institución/Médico que remite, Observación, datos laborales; Eliminar: Motivo + Observación; Cambio de turno: Jornada + Turnos disponibles.
- **Listados**: Citas programadas: AGCI ID | Jornada | Hora | Turno | Documento | Nombre paciente | Tipo cita | Empresa | Régimen | Medio solicitud | Fecha asignación | Registrado por | Estado. Lista de médicos; Turnos; Historial de citas médicas.
- **Flujos y reglas inferidas**: igual a Cita unificada; incluye "Escala de Caídas" (valoración de riesgo; confirmado en código: `EscalaMorse` pide "Esta seguro de realizar la escala de caidas?" y `RedireccionEscalaCaidas` abre EscalaCaidas.aspx).


**Hallazgos del código** (Asignación cita médica OLD; `RegCita` y funciones afines, con validaciones iguales en Urología OLD y Recepción)
- Si la configuración `TIPOAF = 1`: "Por favor Seleccione el tipo de afiliación!", "Por favor Seleccione el tipo de consulta!", "Por favor Seleccione el prestador de servicio!", "Por favor Seleccione el tipo de cita!"; si el tipo de afiliado vale 2 y falta el cotizante: "Registre el cotizante para continuar".
- Siempre: "Seleccione el paciente para continuar.", "Seleccione el tipo de cita por favor.", "Seleccione la fecha solicitud del paciente.", "Ingrese el contrato por favor". Para documento RC sin responsable: "Debido a Las condiciones del paciente es necesario que  registre los datos del responsable" (la exigencia de acompañante está comentada). Con autorización global (`AUTORIZACIONGLOBAL = 1`) y sin procedimientos: "Es nesesario que registre los procedimientos."
- Si el ingreso está "EN TRATAMIENTO" (`CONF.CONTROL = 1`) no se permite tipo PRIMERA VEZ: "No puede seleccionar el tipo de cita X debido a que existe un ingreso en estado EN TRATAMIENTO...". Para tipo de cita 7 (cirugía programada) exige "Seleccione el tipo de examen médico, por favor."
- Comentado (no se aplica): bloqueo por paciente ya con cita en la misma agenda ("El paciente seleccionado ya tiene una cita asignada en esta agenda, no puede contrinuar.") y el bloque de exigencias de autorización (institución/médico que remite, cantidad ordenada, tipo y diagnóstico).
- El recibo de pago se captura embebido (`PanelReciboPago`) y viaja con la cita.
- Operaciones: eliminar (`EliminaCita`: formulario con motivo y observación -> `EC`; `ECO` -> `ELC` eliminar opcional), cambio de turno ("Seleccione el turno al que desea cambiar" -> `CT`), adicionar/eliminar citas (`AddDelCita` -> `AddCita`), cambiar fecha ("Esta seguro de cambiar la fecha de la agenda?" -> `CFA`), transferir agenda o jornada ("Esta seguro de transferir la agenda al medico X ?" / "Esta seguro de transferir la jornada X al medico Y ?" -> `TAM`), activar toda la agenda ("Esta seguro de ACTIVAR la agenda?"), volver a asignado ("Esta seguro de Asignar de nuevo a la agenda?" -> `VAA`). "No hay médicos disponibles para la especialidad requerida".

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


**Hallazgos del código** (Gestiona turno urgencia)
- El JS propio sólo inicializa el servicio de firma de tableta Wacom STU (`checkForSigCaptX`: hasta 20 reintentos, 1 s entre ellos; si falla, "Unable to establish connection to SigCaptX" en consola). La captura de firma depende de ese servicio local.

## OLD > Cita demanda inducida (/SUROSHistoriaClinica/Vistas/Privado/Agenda/CitaDemandaInducida.aspx)
- **Propósito**: versión antigua de la cita unificada para demanda inducida.
- **Funcionalidades**: igual a Cita médica unificada, sin notificación masiva WhatsApp, sin historial de laboratorio ni envíos: guardar, limpiar, cancelar; no realizó consulta; atendido en otra institución (institución, fecha, observación); registrar laboratorio y procedimiento externo; cambiar fecha de agenda, transferir agenda, activar toda la agenda; asignar/modificar/eliminar/cambiar turno/transferir/imprimir cita; activación, volver a asignado, trazabilidad, firmar ingreso; subir laboratorios; signos vitales; consentimiento informado; foto, firma, huella; CIE10; adjuntos.
- **Datos**: Mismos que Cita unificada; adicional "EPS afiliado" en datos del responsable/acompañante; selección de jornadas {TURNO 1..10}; Programa Res. 3280.
- **Listados**: Citas de la agenda: Jornada | Hora | Turno | Documento | Nombre paciente | Tipo cita | Empresa | Régimen | Medio solicitud | Lugar de residencia | Fecha asignación | Registrado por | Estado. Citas médicas del paciente: Descripción | CUPS | Fecha | Hora | Tipo cita | Registrado por | Médico | Tipo consulta | Estado | Factura.
- **Flujos y reglas inferidas**: igual a unificada; "Eliminar cita" exige motivo y observación.


**Hallazgos del código** (Cita demanda inducida OLD)
- El JS propio sólo contiene la captura de signos vitales y laboratorios previos a la consulta (`GuardarLaboratoriosPreConsulta`, `EXAMI.CargaExamenesLaboratorioPorHistoria`); la asignación es lógica de servidor.

## OLD > Malla Reumatología (/SUROSHistoriaClinica/Vistas/Privado/Agenda/MallaReumatologia.aspx)
- **Propósito**: construir y agendar la malla (plan periódico) de atenciones multidisciplinarias de pacientes de reumatología.
- **Funcionalidades**:
  - El usuario puede consultar pacientes por rango de fechas, especialidades (multi) y empresas (multi).
  - Puede crear nueva malla, agregar paciente a la malla (buscar), guardar, terminar y guardar, descartar malla.
  - Puede ver historial de mallas creadas y abrirlas en el visor.
  - Puede registrar cita médica desde la malla con fecha de agendación de citas.
- **Datos**: Fecha inicial, Fecha final, Fecha agendación de citas; Especialidades {PSICOLOGÍA, NUTRICIÓN, FISIOTERAPIA, TERAPIA OCUPACIONAL, REUMATOLOGIA, MEDICAMENTOS, ENFERMERÍA}; Empresas {TODOS, PIJAOS SALUD E.P.S.I (SUBSIDIADO), PARTICULAR (OTRO), ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA (OTRO), ASMET SALUD EPS SAS (SUBSIDIADO), ASMET SALUD EPS SAS (CONTRIBUTIVO)}.
- **Listados**: Listado de pacientes reumatología: # Paciente | Fecha de atención reumatología | Empresa | Documento | Nombre | Apellido | Residencia | Departamento. Historial de mallas: # | Usuario registra | Fecha de creación | Estado | Acciones.
- **Flujos y reglas inferidas**: la malla pasa por borrador (Guardar) y finalizada ("Terminar y Guardar"), o descartada (confirmado en código: `GuardarMalla`, `TerminarMalla`, `DescartarMalla`). Al finalizar NO se agendan citas automáticamente: el agendamiento se hace paciente por paciente y especialidad por especialidad desde la malla (`asignarCitaClick` -> `CargarParametrosLoader`, `RecibirDatos` -> `ActualizarMaya`) (corregido según código); la periodicidad se configura aparte (`RegistrarPeriodicidad`, ver Cita unificada).

**Hallazgos del código** (Malla Reumatología)
- Buscar paciente: "Es necesario que ingrese un parametro de busqueda."; agregar: "Este paciente ya se encuentra en la malla." (`AgregarPaciMalla` -> `AgregarPaciente`).
- Guardar/Terminar: "No se puede guardar la malla si se esta ejecutando algun filtro" (el filtro de residencia debe estar vacío); `GuardarMalla`, `TerminarMalla`.
- Descartar: "Está seguro de DESCARTAR la MALLA?" y "Una vez guardada no podrá realizar ninguna modificación." (`DescartarMalla`).
- Cada celda por especialidad se actualiza al agendar (`RecibirDatos` -> `ActualizarMaya`) o al registrar bitácora (`RecibirDatosBitacora` -> `ActualizarMayaBitacora`) y se persiste con `GuardarMallaActualizada` (el nombre `ActualizarMayaMongo` sugiere almacén documental). Historial: ver (`verMalla`), descargar XML (`verMallaXml`), editar (`TraermallaVistual`); la acción de edición se oculta si el estado de la malla (`MRVE_ID`) no es 1.

## Agendas del día y reportes (pantallas no documentadas arriba)

**Hallazgos del código**
- Agendas de consulta (AgendaConsultaExterna, AgendaConsultaExternaPyP): cargan por fecha y sede (`AL`); "Está seguro de activar la cita?" -> `AC`. Abren el módulo de historia según tipo de cita (`TICI_ID` 8 = Historia nota básica de programas especiales, 16 = Historia reumatología, 18 = Historia citología); sin módulo: "No se ha asignado el modulo de historia para la especialidad del medico."; si ya hay una historia abierta: "Se encontro una historia clinica abierta desea cerrarla? Se perdera la informacion si no se guardo" y luego "Vuelva a seleccionar el paciente.".
- Agenda de procedimientos externos: "Es necesario activar la cita para continuar con la atención"; enruta por tipo de procedimiento (`TIPE_ID`) a actividades de procedimientos externos o procedimientos oftalmológicos (este último sólo con estado de cita 6 o 3).
- Agenda de urgencias: "El paciente X ya esta siendo atendido por Y" si el estado de agenda es 2 o 4 y el médico es otro (bloqueo de atención simultánea); estado 4 se pinta verde y 6 rojo; `CE` cambia el estado.
- Reporte de citas médicas: filtros por médico, especialidad, entidad, contrato y prestador, con período por Año+Mes (opción 1) o rango de fechas (opción 2); `GC`, `CONS`, `CONSCUPS`. Reporte de citas por paciente: el JS sólo copia documento y nombre de la coincidencia (`AsignaN`).

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

### Respondidas
- ¿Qué estados tiene una agenda/franja frente a los canales BOT? Agenda: `AGME_ESTADO` 2 = bloqueada para BOT App/Web, 3 = bloqueada para BOT App; franja: `ACTIVADA` 1/0 y `CITABLOQUEADA` 1/0. Fuente: código: `renderDescripcionAgenda`, `prepareCommandsBot`.
- ¿Qué estados de recepción de una autorización existen? Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta, más Prioritaria y Control; por defecto "En Verificación". Fuente: código: `guardarEstadoRecepcionAutorizacion`, `marcarEstadoPrioritario`, `marcarEstadoControl`.
- ¿Cuándo aplica PRIMERA VEZ vs CONTROL? No se permite PRIMERA VEZ si existe un ingreso en estado EN TRATAMIENTO; el visado define si la cita futura es PRIMERA VEZ o CONTROL. Fuente: código: `RegCita`, `GuardarVisado`.
- ¿Qué se exige para guardar una orden en Recepción? Prestador, especialidad, empresa, contrato y al menos un diagnóstico; para asignar, cantidad de terapias. Fuente: código: `validarCamposRequeridosRecepcion`, `registrarCita`.
- ¿Qué se valida al asignar una cita en las pantallas OLD? Paciente, tipo de cita, fecha de solicitud, contrato, responsable si el documento es RC, tipo de examen si es cirugía programada, procedimientos si hay autorización global. Fuente: código: `RegCita` (Asignación cita médica OLD).
- ¿Hay tope de citas por asignación? El cliente ofrece 1 a 4 y valida el número en `AddDelCita`; el tope diario de servidor se lista abajo. Fuente: código: `AddDelCita`.
- ¿Qué relación hay entre visado y agenda? Al crear agendas el sistema lista las citas con visado pendiente y permite importarlas a las agendas nuevas. Fuente: código: `mostrarCitasConVisado`, `ProcesarCitasConVisado`.
- ¿Cómo se envía WhatsApp? Por dos vías: API de plantillas del servidor (`EnviarWhatsAppPlantillaApi`, `EnviarMasivoWhatsAppAgenda`, plantilla `CONFIRMACION_AGENDAMIENTO_RECEPCION`) y enlace manual wa.me con prefijo 57 (`abrirChatWhatsApp`); los estados En cola/Enviado/Entregado/Leído/Fallido vienen del proveedor. Fuente: código: `enviarWhatsAppCitaDemandaInducida`, `abrirChatWhatsApp`.
- ¿Qué dispositivo usa la firma? Tableta Wacom STU mediante el servicio local SigCaptX. Fuente: código: `checkForSigCaptX`.
- ¿Cómo se reporta el copago a la DIAN? Con `FacturaElectronica` (copago, tipo y id de agenda, parámetro de factura), disponible si `ENVIARCOPAGODIAN = 1`; la facturación electrónica de venta se rige por la Resolución DIAN 000042 de 2020. Fuente: código: `ConvertirDian`, `CargarDianCopago`; norma: Resolución DIAN 000042 de 2020.
- ¿Qué son copago y cuota moderadora y cuándo aplican? Pagos del afiliado regulados para el régimen contributivo por el Acuerdo 260 de 2004 del CNSSS; el sistema los valida en servidor (`ValidarCopagoPaciente`). Fuente: norma: Acuerdo 260 de 2004.
- ¿Qué es "Programa Res. 3280" y qué son los RIPS? La Resolución 3280 de 2018 define las rutas integrales de atención (RPMS); los RIPS son los registros individuales de prestación de servicios de salud (Resolución 3374 de 2000). Fuente: norma: Resolución 3280 de 2018; Resolución 3374 de 2000.
- ¿Qué contiene el historial de llamadas de la bitácora? Paciente, observación, receptor, parentesco, área y prestador, con edición distinta según sea nota simple o llamada. Fuente: código: `GridCommand`.
- ¿Qué pantallas están vigentes? Recepción abre CitaDemandaInducidaUnificada.aspx (o TurnoInstanciaUrgencia.aspx para laboratorio clínico) y no abre Asignación cita médica ni Cita demanda inducida OLD; el resto de OLD se trata como legado. Fuente: código: `registrarCita`; supuesto estándar del sector para el resto.
- ¿Quién puede eliminar en la bitácora? Sólo quien tenga `puedeEliminar` verdadero. Fuente: código: `preparaBarraPR`.

### Sin respuesta por ingeniería inversa
- Transiciones exactas de estado de cita, franja y urgencias (valores numéricos de `AGME_ESTADO`, `ESAG_ID`, `TIAG`) y quién las ejecuta: lógica del servidor.
- Matriz de permisos por rol y sede (bloquear, activar para BOT/Demanda Inducida, transferir, eliminar, visar, convertir recibos): lógica del servidor.
- Reglas de servidor al asignar: vigencia de autorización/contrato, límite de citas por día, duplicado de paciente en la agenda (la validación del cliente está comentada), cuándo se exige copago: lógica del servidor.
- Algoritmo de reserva de franjas por el BOT y significado práctico de "Prioritaria" vs "Por Defecto": lógica del servidor.
- Proveedor de WhatsApp, plantillas aprobadas, webhooks y si se verifica la autorización de tratamiento de datos (Ley 1581 de 2012) antes de enviar: sin acceso.
- Dispositivos de huella y captura de foto: sin acceso.
- Contenido de la ventana "Concentimiento" de Turno Rayos X y sincronización del estado del estudio con laboratorio: requiere paciente real.
- Si el módulo genera RIPS o reportes de Res. 3280: lógica del servidor.
- Valores de `AUT_MAX_MESES_RANGO` y de `ENVIARCOPAGODIAN`: sin acceso (parametrización).
- Qué pantallas OLD siguen visibles en el menú por perfil: sin acceso.
- Intención de "M2 = peso x 4 + 7" y de la saturación fija en 95 al guardar laboratorios previos: decisión del negocio.
- Si eliminar en la bitácora (sin confirmación) es borrado lógico o físico: lógica del servidor.
