## CITAS MEDICAS > PROGRAMAR AGENDA MEDICA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaMedica.aspx)
TITLE Agenda Medica
BTN Refrescar
BTN Bloquear seleccionadas
BTN Cerrar
GRID Franjas: Turno | Hora | Estado | Acciones
WINDOW Gestionar franjas horarias de la agenda
FIELD[combobox] Tipo de bloqueo {Por IPS, Por Médico}
FIELD[textareafield] Causa
BTN Confirmar
BTN Cancelar
WINDOW Bloquear franjas seleccionadas
WINDOW Gestionar franjas horarias de la agenda (BOT App)
WINDOW Bloquear franjas seleccionadas (BOT App)
GRID Franjas BOT App/Web: Turno | Hora | Estado | Acciones
WINDOW Activar franjas para Agendamiento por BOT App/Web
FIELD[combobox] Tipo de activación {Por Defecto, Prioritaria}
WINDOW Activar franjas seleccionadas para BOT
BTN Activar seleccionadas
GRID Franjas BOT App: Turno | Hora | Estado | Acciones
WINDOW Activar franjas para Agendamiento por BOT App
WINDOW Activar franjas seleccionadas para BOT App
GRID Franjas Demanda Inducida: Turno | Hora | Estado | Acciones
WINDOW Activar franjas para Agendamiento por Demanda Inducida
FIELD[combobox] Tipo de activación {Por Defecto}
WINDOW Activar franjas seleccionadas para Demanda Inducida
BTN Bloquear franjas para agendamiento por BOT App/Web
BTN Bloquear franjas para Agendamiento por BOT App
BTN Bloquear/Desbloquear para agendamiento por BOT App/Web
BTN Bloquear/Desbloquear para agendamiento por BOT App
BTN Activar franjas para Agendamiento por BOT App/Web
BTN Activar franjas para Agendamiento por BOT App
BTN Ver resumen de turnos
WINDOW Menu de opciones
FIELD[combobox] Prestador de servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[netmulticombo] Jornada de atención {TURNO 1, TURNO 2, TURNO 3, TURNO 4, TURNO 5, TURNO 6, TURNO 7, TURNO 8, TURNO 9, TURNO 10}
FIELD[combobox] Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[combobox] Categorias
FIELD[combobox] Ejecucion/Nivel de complejidad
FIELD[combobox] Equipo de atención
FIELD[combobox] Zona Atención
FIELD[combobox] Unidad funcional {AMBULATORIO}
FIELD[combobox] Grupo de servicio {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}
FIELD[combobox] Servicios
FORM Datos generales
FIELD[displayfield] DisplayField1
FIELD[numberfield] TextConsultorio
FIELD[checkboxfield] Externo
FIELD[textfield] ConsultorioExterno
FIELD[textfield] TextObservacion
FIELD[radiofield] Opcion 1
FIELD[radiofield] Opcion 2
FIELD[radiogroup] Opcion intervalo
FIELD[timefield] HoraInicial1
FIELD[numberfield] TextMinutos
FIELD[timefield] HoraFinal22
FIELD[numberfield] TextNumPacientes
FIELD[timefield] HoraInicial
FIELD[timefield] HoraFinal
FIELD[numberfield] TextNumPacientes2
BTN Generar
FORM Datos específicos
FIELD[displayfield] ctl252
FIELD[textfield] textfield-1092
FIELD[combobox] Especialidad
GRID : LISTA DE MEDICOS
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[numberfield] TextAno
BTN Actualizar
GRID Calendario: DOM | LUN | MAR | MIE | JUE | VIE | SAB
BTN Guardar
FIELD[checkboxfield] Mostrar programación eliminada
GRID : ID | FECHA | HORA INICIAL | HORA FINAL | DESCRIPCION | PROFESIONAL PRINCIPAL | PROFESIONAL AUXILIAR | TIEMPOATENCIÓN | TURNOSCREADOS | TURNOSASIGNADOS | JORNADA | PROGRAMADA POR
BTN Asignar medico
BTN Medico o auxiliar acompañante
BTN Agregar convenio
TOOLTIP Actualizar
BTN Sort Ascending
BTN Sort Descending
BTN Columns
BTN Group by this field
FIELD[textfield] textfield-1233
FIELD[combobox] Convenio
WINDOW Agregar Convenio
FIELD[combobox] Medico
WINDOW Asignar medico a la agenda
FIELD[combobox] Medico o auxiliar
WINDOW Medico o auxiliar acompañante
GRID : CAMPAÑA | PLANTILLA | FECHA | TOTAL | OK | FALLIDOS | ESTADO
PANEL Campañas
GRID : PACIENTE | TELÉFONO | FECHA ENVÍO | ESTADO | WHATSAPP ID
PANEL Envíos por paciente
WINDOW Historial de mensajes

## CITAS MEDICAS > CITA MEDICA UNIFICADA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/CitaDemandaInducidaUnificada.aspx)
TITLE Cita Demanda Inducida
WINDOW Registrar Laboratorio
WINDOW Registrar Procedimiento Externo
BTN No Realizo Consulta
BTN Atendido en Otra Institucion
WINDOW Menu de opciones
FIELD[textfield] Institucion
FIELD[datefield] Fecha Atencion
FIELD[textareafield] Observacion
BTN Guardar
BTN Cancelar
WINDOW Registrar Datos
GRID : Descripción
BTN Aceptar
WINDOW Dispositivos
BTN Cambiar fecha de la agenda
BTN Transferir la agenda a otro medico
BTN Activar toda la agenda
BTN Opciones
BTN Exportar
FIELD[displayfield] TextPacientTR
BTN Transferir jornada a otro medico
BTN Notificar WhatsApp
BTN Historial de envíos
BTN Eliminar ultimos turnos
BTN Agregar turnos al final
BTN Actualizar
GRID : JORNADA | HORA | HORA FIN | TURNO | DOCUMENTO | NOMBRE PACIENTE | PROCEDIMIENTO | TIPO CITA | No. Autorización | EMPRESA | CONTRATO | REGIMEN | MEDIO SOLICITUD | LUGAR DE RESIDENCIA | FECHA ASIGNACIÓN | REGISTRADO POR | ESTADO | SEDE | NOTA | CELULAR
WINDOW Registrar Citas
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
WINDOW Detalle datos del paciente
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
GRID : Codigo | Descripción
BTN Salir
WINDOW Coincidencias encontradas en el CIE10
BTN Asignar cita
BTN Modificar cita (M)
BTN Eliminar cita (Supr)
BTN Cambiar de turno (C)
BTN Transferir cita (T)
BTN Asigna cita de transferencia (T)
BTN imprimir (P)
BTN Asignar turno
BTN Eliminar cita opcional
BTN Ver nota inasistencia
BTN Activación de cita
BTN Volver a asignado
BTN Trazabilidad
BTN Firmar ingreso
BTN Agregar cita grupal
BTN Subir Laboratorios Pc
FIELD[combobox] EXAMI_ComboTipohistoriaLaboratorios {CONSULTA HIGIENE ORAL, ESPECIALES (CRONICOS), REUMATOLOGIA}
GRID : EXAMEN | VALOR
FIELD[numberfield] Sist
FIELD[displayfield] EXAMI_DisplayField7
FIELD[numberfield] Dias
FIELD[displayfield] EXAMI_DisplayField1
FIELD[numberfield] EXAMI_TextFrecuenciaCardiaca
FIELD[displayfield] EXAMI_DisplayField2
FIELD[numberfield] EXAMI_TextFrecuenciaRespiratoria
FIELD[displayfield] EXAMI_DisplayField3
FIELD[numberfield] EXAMI_TextGlucometria
FIELD[displayfield] EXAMI_DisplayField5
FIELD[numberfield] EXAMI_TextTemperatura
FIELD[displayfield] EXAMI_DisplayField6
FIELD[numberfield] EXAMI_TextPesoo
FIELD[displayfield] EXAMI_DisplayField8
FIELD[numberfield] EXAMI_TextTallaa
FIELD[displayfield] EXAMI_DisplayField9
FIELD[numberfield] EXAMI_TextIMCC
FIELD[numberfield] EXAMI_TextM2
FIELD[displayfield] Peso
FIELD[displayfield] Riesgo
FORM SIGNOS VITALES
PANEL Laboratorios
WINDOW Laboratorios Pre Consulta
BTN Buscar Procedimiento
BTN Traer datos Biometricos del Ingreso
BTN Obtener firma
BTN Aplicar datos al formato
FIELDSET Datos del paciente
PANEL Datos Biometricos paciente
FIELD[textfield] Documento de identidad:
FIELD[textfield] Nombre del testigo o responsable del paciente:
FIELD[textfield] Relaciòn con el paciente:
FIELDSET Datos del testigo o responsable del paciente
PANEL Datos Biometricos Acompanante
FIELD[textfield] TxtProcedimientoConsentimiento
BTN Buscar
PANEL Procedimientos
FIELD[htmleditor] HtmlEditorPanelPrev
WINDOW GENERAR CONSENTIMIENTO INFORMADO
FIELD[textfield] TextDocumentoP
BTN Editar Datos Paciente
FIELD[combobox] Tipo Usuario:
FIELD[combobox] Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[textfield] Prestador de servicios
FIELD[textfield] Jornada
FIELD[combobox] Categorias {JORNADA DE SALUD, VISITA DOMICILIARIA, UNIDAD MOVIL, TELEMEDICINA INTERACTIVA, TELEMEDICINA NO INTERACTIVA, TELEXPERTICIA, TELEMONITOREIO, INTRAMURAL}
FIELD[combobox] Ejecucion/Nivel de complejidad
FIELD[combobox] Equipo de atención
FIELD[combobox] Zona Atención
FIELD[textfield] TextTipoPaciente
BTN Habilitar Programa especiales
PANEL DATOS DE LA AGENDA
FIELD[datefield] FechaSolicitudCita
FIELD[datefield] FechaQueriaPaciente
FIELD[datefield] FechaAsignacion
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[combobox] Gestante {SI, NO}
FIELD[combobox] ViaIngreso {DEMANDA ESPONTANEA, DERIVADO DE CONSULTA EXTERNA, DERIVADO DE URGENCIAS, DERIVADO DE HOSPITALZACION, DERIVADO DE SALA DE CIRUGIA, DERIVADO DE SALA DE PARTOS, RECIEN NACIDO EN LA INSTITUCION, RECIEN NACIDO EN OTRA INSTITUCION, DERIVADO O REFERIDO DE HOSPITALIZACION DOMICILIARIA, DERIVADO DE ATENCION DOMICILIARIA, DERIVADO DE TELEMEDICINA, DERIVADO DE JORNADA DE SALUD, REFERIDO DE OTRA INSTITUCION, CONTRAREFERIDO DE OTRA INSTITUCION}
FIELD[combobox] LimitacionEscalera {NO APLICA, SI, NO}
FIELD[combobox] TipoConsultaModalidad
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA}
FIELD[combobox] ComboBoxSubsRPMS
FIELD[combobox] ComboBoxTipoProcedimientoGastro
FIELD[combobox] AcompananteAplica {SI, NO}
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[textfield] TextAcudiente
BTN Asignar datos del Acompanante
BTN Borrar Acompanante
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboContrato
FIELD[textareafield] TextObservacion
PANEL Información de la cita
BTN Tomar Foto
PANEL Fotografia
FIELD[filefield] SubirArchivo
BTN Obtener Link
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
BTN Obtener Huella
PANEL Huella Digital
PANEL Datos Biometricos
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[datefield] FechaOrdenMedica
FIELD[combobox] Orden remitida desde Surós: {SI, NO}
BTN Referenciar Orden
FIELD[checkboxfield] Primera vez del tratamiento de reumatología:
BTN Eliminar
GRID : Código | Descripción | Cantidad | Observación
BTN Agregar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Adjuntos Fisicos
FIELD[combobox] Categoria: {ADMINISTRATIVO}
FIELD[combobox] Tipo soporte digital:
FIELD[combobox] Relaciòn con el paciente:
GRID Listado de soportes digitales: Categoria | No Autorización | Tipo de soporte | Fecha de creacion | Registrado por | PDF | Modificar | Eliminar
PANEL Adjunto Digitales
FIELD[textfield] DiagnosticoIdCita
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Codigo | Descripción | Prioridad
PANEL Diagnostico
GRID : Datos de adjunto
BTN Descargar
BTN Zoom +
BTN Zoom -
BTN Rotar ?
BTN Restablecer
PANEL Vista previa
BTN Imprimir
FIELD[checkboxfield] Enviar mensaje confirmación
BTN Guardar y cerrar
WINDOW Asignar cita
GRID : Paciente | Celular
PANEL Pacientes con celular válido (recibirán la notificación)
GRID : Paciente | Celular | Teléfono
PANEL Pacientes sin celular válido — no recibirán notificación
FIELD[combobox] Plantilla de mensaje
FIELD[textareafield] TxtWhatsAppVistaPrevia
PANEL Vista previa del mensaje
FIELD[textareafield] TxtWhatsAppResDetalles
BTN Atrás
BTN Siguiente
BTN Enviar notificaciones
WINDOW Enviar notificaciones WhatsApp
GRID : Campaña | Plantilla | Fecha | Estado | Total | Env. | Ent. | Leíd. | Fall.
PANEL Campañas
GRID : Paciente | Teléfono | Estado | Fecha envío | Mensaje
FIELD[combobox] Estado {Todos, En cola, Enviado, Entregado, Leído, Fallido}
PANEL Mensajes de la campaña
WINDOW Historial de envíos masivos
PANEL Línea de tiempo
FIELD[textareafield] TxtWhatsAppHistDetContenido
PANEL Contenido del mensaje
WINDOW Detalle del mensaje
FIELD[filefield] FileUploadField1
FIELD[filefield] FileUploadField2
BTN GUARDAR
BTN CANCELAR
WINDOW FIRMAR INGRESO
BTN Limpiar
FIELD[combobox] Seleccione
FIELD[textfield] textfield-1283
GRID : ESPECIALIDAD | PERIOSIDAD
WINDOW CONFIGURACION MALLA REUMATOLOGIA
GRID :
WINDOW PERIODICIDAD
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
BTN Tomar Fotografia
BTN Guardar Fotografia
BTN Volver a tomar
WINDOW Tomando Foto del Paciente
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
BTN Traer datos responsable
WINDOW Datos del acudiente
WINDOW Datos del Acompanante
WINDOW Registrar nuevo paciente
FIELD[combobox] Motivo
FIELD[textareafield] Observación
WINDOW Eliminar cita
FIELD[combobox] Jornada
FIELD[combobox] Turnos disponibles
WINDOW Cambio de turno
FIELD[numberfield] Numero citas
WINDOW Adicionar citas a la agenda
WINDOW Seleccione la nueva fecha
BTN Octubre 2026
BTN Hoy
FIELD[displayfield] ctl953
FIELD[textfield] textfield-1327
GRID : MEDICO
WINDOW Medicos disponible para transferir
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
BTN Crear nuevo paciente
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombre
FIELD[textfield] TextGenero
FIELD[textfield] TextFNacimiento
FIELD[textfield] TextEdad
BTN Información paciente
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
GRID : Descripcion | Cups | Fecha | Hora | Tipo de Cita | Registrado Por | Medico | Tipo de Consulta | Estado | Factura | Info
PANEL CITAS MEDICAS
GRID : ID | PROCEDIMIENTO | CUPS | TIPO CITA | FECHA ASIGNACION | FECHA TOMA | FECHA ENTREGA | REGISTRADO POR | ESTADO
PANEL CITAS LABORATORIO
FIELD[textfield] textfield-1379
FIELD[displayfield] ctl1039
FIELD[displayfield] ctl1043
FIELD[displayfield] ctl1047
FIELD[displayfield] ctl1051
FIELD[displayfield] ctl1055
FIELD[displayfield] ctl1059
FIELD[displayfield] ctl1063
FIELD[displayfield] ctl1067
GRID : PROGRAMA RES. 3280 | PROFESIONAL QUE PUEDE REALIZAR | Ver sólo actividades pendientes | Programadas | Inasistencia | Ejecutadas | Fecha ultima ejecutada | Especialidad ultima ejecucion | Programada | Fecha ultima programada | Especialidad ultima programada
BTN Configurar
GRID : ESPECIALIDAD | PERIOSIDAD | ENE | FEB | MAR | ABR | MAY | JUN | JUL | AGO | SEP | OCT | NOV | DIC
FIELD[combobox] Especialidad
GRID OTRAS AGENDAS:
FIELD[textfield] TextNombreFilter
GRID PROFESIONAL DE LA SALUD: PROFESIONAL | PROFESIONAL | % de Agenda
FIELD[netmulticombo] JornadaDescripcion {TURNO 1, TURNO 2, TURNO 3, TURNO 4, TURNO 5, TURNO 6, TURNO 7, TURNO 8, TURNO 9, TURNO 10}
PANEL Jornada
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[numberfield] TextAno
GRID Agenda: DOM | LUN | MAR | MIE | JUE | VIE | SAB
TOOLTIP Actualizar
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjuntos
WINDOW Imagen Adjunta
WINDOW Recibo de pago
WINDOW Gestion del paciente
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
WINDOW Agregar Médico Externo
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
FIELD[combobox] Departamento
FIELD[combobox] Municipio
WINDOW Municipio
BTN Agregar Procedimientos
BTN Quitar de la lista
GRID : ID | Código | Descripción | Cantidad | Cantidadejecutada | Observación
WINDOW Adicionar procedimiento
GRID : CODIGO | CODIGO
WINDOW COINCIDENCIA
FIELD[datefield] Fecha inicio:
FIELD[datefield] Fecha fin:
BTN Consultar
GRID : ID | FECHA | HORA INICIAL | HORA FINAL | DESCRIPCION | ESPECIALIDAD | MEDICO ASIGNADO | MEDICO AUXILIAR | CONVENIO | ESTADO | TURNOSCREADOS | TURNOSASIGNADOS | PROGRAMADA POR
BTN Asignar medico
BTN Medico o auxiliar Acompanante
BTN Agregar convenio
WINDOW Agenda Telemedicina
FIELD[combobox] Convenio
BTN Confirmar
WINDOW Agregar Convenio
FIELD[combobox] Medico
WINDOW Agregar medico a la agenda
FIELD[combobox] Medico o auxiliar
WINDOW Medico o auxiliar Acompanante
FIELD[textfield] txtCopaId
FIELD[textfield] txtAgenda
FIELD[textfield] txtAgendaId
FIELD[combobox] Resolución
BTN Enviar
WINDOW Enviar Copago a Dian
GRID : Ingreso
BTN Agregar Formula
WINDOW Ingresos del Paciente
FIELD[checkboxfield] chkSelectAll
BTN AGREGAR
WINDOW Cups Encontrados
FIELD[textfield] Nombre del archivo
FIELD[combobox] Formato {PNG, JPG}
WINDOW Descargar Imagen

## CITAS MEDICAS > ACTIVACIÓN DE CITA (/SUROSHistoriaClinica/Vistas/Privado/ActivacionCita/ActivacionCita.aspx)
TITLE 
BTN Agregar Copago autorizado
WINDOW Opciones
FIELD[filefield] SubirArchivo
BTN Obtener firma
BTN Obtener Link
BTN Cancelar
BTN Guardar
PANEL Firma Digital
WINDOW Firmas por telefono
GRID : Descripción
BTN Aceptar
WINDOW Dispositivos
FIELD[textfield] txtCopaId
FIELD[textfield] txtAgenda
FIELD[textfield] txtAgendaId
FIELD[combobox] Resolución
BTN Enviar
WINDOW Enviar Copago a Dian
FIELD[textfield] Nombre usuario
FIELD[textfield] Contraseña
BTN Continuar
WINDOW Ingresar credenciales
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
BTN Agregar
WINDOW Recibo de pago
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
FIELD[textfield] Identificación
FIELD[textfield] Género
FIELD[textfield] Nombre Completo:
FIELD[textfield] Nombre1:
FIELD[textfield] Fecha de nacimiento
FIELD[textfield] Empresa:
FIELD[textfield] Régimen:
FIELD[textfield] Zona residencial:
FIELD[textfield] Municipio residencia:
BTN Mostrar todo
BTN Actualizar pendientes
GRID : ID | Código | Procedimiento/Profesional | Procedimiento/Profesional
GRID Recibo de caja: Concepto | Valores | Información caja
BTN Imprimir el recibo de pago
BTN Convertir a Electronica
PANEL Activación Citas - Recibo Caja
BTN Limpiar
WINDOW FIRMAR INGRESO
FIELD[textfield] TextDocumentoP
BTN Editar Datos del paciente
FIELD[combobox] Tipo Usuario:
FIELD[combobox] Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[textfield] Prestador de servicios
FIELD[textfield] Jornada
FIELD[textfield] Categorias
FIELD[textfield] Ejecución/Nivel Complejidad
FIELD[textfield] Equipo de atención
FIELD[textfield] TextTipoPaciente
PANEL DATOS DE LA AGENDA
FIELD[datefield] FechaSolicitudCita
FIELD[datefield] FechaQueriaPaciente
FIELD[datefield] FechaAsignacion
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[combobox] Gestante {SI, NO}
FIELD[combobox] ViaIngreso {DEMANDA ESPONTANEA, DERIVADO DE CONSULTA EXTERNA, DERIVADO DE URGENCIAS, DERIVADO DE HOSPITALZACION, DERIVADO DE SALA DE CIRUGIA, DERIVADO DE SALA DE PARTOS, RECIEN NACIDO EN LA INSTITUCION, RECIEN NACIDO EN OTRA INSTITUCION, DERIVADO O REFERIDO DE HOSPITALIZACION DOMICILIARIA, DERIVADO DE ATENCION DOMICILIARIA, DERIVADO DE TELEMEDICINA, DERIVADO DE JORNADA DE SALUD, REFERIDO DE OTRA INSTITUCION, CONTRAREFERIDO DE OTRA INSTITUCION}
FIELD[combobox] LimitacionEscalera {NO APLICA, SI, NO}
FIELD[combobox] TipoConsultaModalidad
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA}
FIELD[combobox] ComboBoxSubsRPMS
FIELD[combobox] ComboBoxTipoProcedimientoGastro
FIELD[combobox] AcompañanteAplica {SI, NO}
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[textfield] TextAcudiente
BTN Asignar datos del acompañante
BTN Borrar acompañante
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboContrato
FIELD[textareafield] TextObservacion
PANEL Información de la cita
BTN Tomar Foto
PANEL Fotografia
FIELD[filefield] FileUploadField1
FIELD[filefield] SubirHuellaDactilar
BTN Obtener Huella
PANEL Huella Digital
PANEL Datos Biometricos
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[datefield] FechaOrdenMedica
FIELD[combobox] Orden remitida desde Surós: {SI, NO}
BTN Referenciar Orden
FIELD[checkboxfield] Primera vez del tratamiento de reumatología:
BTN Eliminar
GRID : Código | Descripción | Cantidad | Observación
PANEL Procedimientos
BTN Actualizar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Adjuntos Fisicos
FIELD[combobox] Categoria: {ADMINISTRATIVO}
FIELD[combobox] Tipo soporte digital:
FIELD[combobox] Relaciòn con el paciente:
GRID Listado de soportes digitales: Categoria | No Autorización | Tipo de soporte | Fecha de creacion | Registrado por | PDF | Modificar | Eliminar
PANEL Adjunto Digitales
FIELD[textfield] DiagnosticoIdCita
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Codigo | Descripción | Prioridad
PANEL Diagnostico
GRID : Datos de adjunto
BTN Descargar
BTN Zoom +
BTN Zoom -
BTN Rotar ↻
BTN Rotar ↺
BTN Restablecer
PANEL Vista previa
BTN Imprimir
BTN Guardar y cerrar
WINDOW Asignar cita
WINDOW Concentimiento
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
GRID : Codigo | Descripción
BTN Salir
WINDOW Coincidencias encontradas en el CIE10
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjuntos
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
BTN Traer datos responsable
WINDOW Datos del acudiente
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
FIELD[combobox] Especialidad
WINDOW Agregar Médico Externo
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
WINDOW Gestion del paciente

## CITAS MEDICAS > RECEPCIÓN AUTORIZACIONES (/SUROSHistoriaClinica/Vistas/Privado/Autorizaciones/RecepcionAutorizacion.aspx)
TITLE RECEPCIÓN AUTORIZACIÓN
GRID : Código | Descripción | Tipo manual
BTN Aceptar
BTN Cancelar
WINDOW Coincidencias encontradas
BTN Tomar Fotografia
BTN Guardar Fotografia
BTN Salir
WINDOW Tomando Foto del Paciente
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
WINDOW Datos del responsable
WINDOW Datos del acompañante
FIELD[combobox] Departamento
FIELD[combobox] Municipio
WINDOW Municipio
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
FIELD[combobox] Especialidad
WINDOW Agregar Médico Externo
WINDOW Registrar nuevo paciente
GRID : Codigo | Descripción
WINDOW Coincidencias encontradas en el CIE10
FIELD[combobox] Prestador Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Tipo de Consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[combobox] Tipo programa especial: {NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}
FIELD[textfield] Buscar
BTN Buscar Paciente
BTN Crear Paciente
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombreP
FIELD[textfield] TextFechaNacimiento
FIELD[textfield] TextGenero
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[textfield] TextEmpresa
FIELD[textfield] TextMunicipio
FIELD[textfield] TextDireccion
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
BTN Actualizar Paciente
BTN Guardar Cambios
FIELDSET Datos personales del paciente
FIELD[textfield] TextFechaFilter
FIELD[textfield] TextTurnoFilter
FIELD[textfield] TextHoraFilter
FIELD[textfield] TextMedicoFilter
FIELD[textfield] TextRegistraCitaFilter
FIELD[textfield] TextMotivoCambioEstadoFilter
FIELD[textfield] TextTipoAsignacionFilter
FIELD[textfield] TextEstadoFilter
GRID : Fecha | Turno | Hora | Medico | Registrado por | Nota | Tipo asignación | Estado
PANEL Historial de Citas Autorizaciones
FIELD[datefield] FechaSolicitudCita
FIELD[datefield] FechaQueriaPaciente
FIELD[datefield] FechaAsignacion
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[checkboxfield] Gestante
FIELD[combobox] LimitacionEscalera {NO APLICA, SI, NO}
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA}
FIELD[combobox] ComboBoxSubsRPMS
FIELD[combobox] ComboBoxTipoProcedimientoGastro
FIELD[combobox] AcompañanteAplica {SI, NO}
FIELD[textfield] TextResponsable
BTN Asignar datos del acompañante
BTN Borrar acompañante
FIELD[combobox] cbxTipoAsignacion {PRESENCIAL, TELEFONICA, INTERNET}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa
FIELD[combobox] ComboContrato
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[datefield] FechaOrdenMedica
FIELD[textareafield] TextObservacion
PANEL Autorizaciones
GRID : Código | Descripción | Cantidad | Observación
BTN Eliminar
PANEL Procedimientos
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID Procedimientos Quirurgicos: Codigo | Descripción | Prioridad
PANEL Diagnóstico
BTN Guardar
WINDOW Asignar cita
BTN Visualizar adjuntos
BTN Asignar Cita
BTN Reasignar Cita
BTN Información de eliminación
BTN Estado de recepción
BTN Contacto WhatsApp
BTN Modificar Registro (M)
BTN Notas
BTN Visado
BTN Información de visado
BTN Eliminar cita (Supr)
BTN Actualizar Clasificación CUPS
BTN Marcar como Prioritaria
BTN Marcar como Control
WINDOW Menu de opciones
BTN Agregar
BTN Actualizar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
WINDOW Adjuntos de la cita
BTN Descargar
BTN Zoom +
BTN Zoom -
BTN Rotar ↻
BTN Rotar ↺
BTN Restablecer
BTN Cerrar
WINDOW Visualizador de imagen
FIELD[textfield] Nombre del archivo
FIELD[combobox] Formato {PNG, JPG}
WINDOW Descargar Imagen
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisicoRA
FIELD[filefield] AddAdjuntoFisicoRA
WINDOW Adjuntos
BTN Actualizar Lista
GRID Historial de notas: ID
FIELD[textareafield] TextNota
FIELD[datefield] Fecha:
FIELD[timefield] Hora
FORM Nota
BTN Editar
PANEL Notas
FIELD[combobox] Mes futura revisión {Enero, Febrero, Marzo, Abril, Mayo, Junio, Julio, Agosto, Septiembre, Octubre, Noviembre, Diciembre}
FIELD[numberfield] Día
FIELD[numberfield] Año
FIELD[combobox] Tipo de cita {PRIMERA VEZ, CONTROL}
FIELD[textareafield] Observación
WINDOW Visado
FIELD[combobox] Motivo
WINDOW Eliminar cita
FIELD[textareafield] Por favor, explique la razón por la cuál se realiza la reprogramación de la cita:
WINDOW Reprogramar cita
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Lista de Médicos
WINDOW Coincidencia encontrada
FIELD[combobox] Jornada
FIELD[combobox] Turnos disponibles
WINDOW Cambio de turno
FIELD[numberfield] Numero citas
WINDOW Adicionar citas a la agenda
WINDOW Seleccione la nueva fecha
BTN Octubre 2026
BTN Hoy
FIELD[numberfield] TextTerapiasAsignacionCita
WINDOW Cantidad de terapias
FIELD[datefield] dtFechaCita
FIELD[timefield] TimeHoraCita
FIELD[numberfield] TextNumeroTerapias
FIELD[combobox] ComboMedico
WINDOW Registra Cita
FIELD[datefield] _Desde
FIELD[datefield] _Hasta
FIELD[combobox] _ESTADOTERAPIAS {TODOS, ASIGNADO, PENDIENTE, ATENDIDO, CITA CANCELADA, CANCELADA SIN CITA}
FIELD[textfield] _DOCUMENTO
FIELD[combobox] _ID
BTN Borrar
WINDOW Búsqueda avanzada
GRID : Id | Hora | Fecha | Nombre paciente | Medico
WINDOW Citas Pendientes
FIELD[textfield] ctl655
FIELD[textfield] textfield-1190
FIELD[textfield] textfield-1192
FIELD[textfield] textfield-1194
FIELD[textfield] textfield-1196
FIELD[textfield] textfield-1198
FIELD[textfield] textfield-1200
FIELD[textfield] textfield-1202
FIELD[textfield] textfield-1204
FIELD[textfield] textfield-1206
FIELD[textfield] textfield-1208
FIELD[textfield] textfield-1210
FIELD[textfield] textfield-1212
FIELD[textfield] textfield-1214
FIELD[textfield] textfield-1216
FIELD[textfield] textfield-1218
FIELD[textfield] textfield-1220
FIELD[textfield] textfield-1222
FIELD[textfield] textfield-1224
FIELD[datefield] Fecha inicio:
FIELD[datefield] Fecha fin
BTN Este Mes
BTN Esta Semana
BTN Consultar
BTN Pendientes
BTN Asignados
BTN Agregar Orden
BTN Búsqueda avanzada
BTN Desbloquear campos
BTN Exportar
FIELD[triggerfield] Buscar en la agenda médica filtrada
FIELD[netmulticombo] Empresa
FIELD[combobox] Contrato
BTN Refrescar
GRID Recepción de Autorizaciones: Id | FECHA | DOCUMENTO | NOMBRE PACIENTE | TELEFONO | INSTITUCION QUE REMITE | ESPECIALIDAD | DIAGNOSTICO | ESTADO | ESTADO ASIGNACIÓN | ORIGEN | SERVICIO | PROGRAMA PYP | ESTADO RECEPCIÓN | WHATSAPP | VISADO | MEDICO QUE REMITE | ASIGNADO POR
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field
GRID : Código | Descripción | Clasificación Actual | Clasificación General | Clasificación Específica | Justificación del Cambio
WINDOW Actualizar Clasificación CUPS
FIELD[combobox] Estado {Aceptada, Rechazada, En Verificación, Archivo Dañado, Foto Incompleta}
FIELD[checkboxfield] Enviar mensaje por WhatsApp sobre este estado
FIELD[textareafield] Escriba un mensaje para el paciente...
WINDOW Estado recepción autorización

## CITAS MEDICAS > BITÁCORA DEMANDA INDUCIDA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Bitacora/Bitacora.aspx)
TITLE Bitacora de llamadas
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
FIELD[textareafield] OBSERVACION
WINDOW Observación
BTN Nueva plantilla
BTN Editar plantilla
BTN Eliminar plantilla
GRID : Descripcion
BTN Guardar Items en la Plantilla
BTN Cargar plantilla
BTN Cancelar
WINDOW Mis plantillas
FIELD[textfield] TextNPlantilla
BTN Aceptar
WINDOW Nombre Plantilla
FIELD[combobox] Prestador de Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[textfield] Nombre
FIELD[textfield] Documento
FIELD[textfield] PERS_ID
FIELD[combobox] Area que genera
FORM Busqueda
FIELD[textfield] Teléfono
BTN Agregar
PANEL Telefonos de contacto
GRID Teléfonos del paciente: TELEFONOS | QUITAR
FIELD[radiofield] Contestó paciente
FIELD[radiofield] Otra persona
FIELD[timefield] Hora llamada
FIELD[combobox] Motivo de llamada {Demanda inducida, Entrega de medicamentos, Educacion, Revision de ayudas diagnosticas}
FIELD[textfield] Receptor de la llamada
FIELD[combobox] Parentesco {MAMÁ, PAPÁ, HIJO(A), TIO(A), ABUELO(A), PRIMO(A), SOBRINO(A), ESPOSO(A), OTRO, HERMANO(A)}
FIELD[textareafield] Nota
FIELD[textfield] BILL_ID
FORM Respuesta del usuario
PANEL Información Completa
PANEL Nota
BTN Guardar
BTN Actualizar
BTN Cancelar actualizacion
PANEL Bitacora de contacto
FIELD[combobox] Filtrar por: {Rango de fecha, Paciente, Todo}
FIELD[datefield] Fecha inicial:
FIELD[datefield] Fecha final:
FIELD[netmulticombo] Prestador de Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
BTN Exportar a PDF
BTN Exportar a excel
BTN First Page
BTN Previous Page
BTN Next Page
BTN Last Page
BTN Refresh
GRID :
PANEL Historial de llamadas
TOOLTIP Plantillas
FIELD[checkboxfield] CheckTodoCarta
FIELD[checkboxfield] CheckTodoTirilla
GRID Ítems de impresión: Descripción | Carta | Tirilla
WINDOW Imprimir formatos
BTN Editar
BTN Imprimir
BTN Eliminar

## CITAS MEDICAS > TURNO PROCEDIMIENTOS EXTERNOS (/SUROSHistoriaClinica/Vistas/Privado/Agenda/TurnoProcedimientos.aspx)
TITLE Turno Procedimientos
BTN Guardar
BTN Limpiar
BTN Cancelar
WINDOW FIRMAR INGRESO
BTN Agregar
WINDOW Recibo de pago
GRID : Código | Descripción | Tipo manual
BTN Aceptar
WINDOW Coincidencias encontradas
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
BTN Traer datos responsable
WINDOW Datos del responsable
FIELD[combobox] Motivo
FIELD[textareafield] Observación
WINDOW Cancelar turno
BTN Modificar turno (M)
BTN Eliminar cita (Supr)
BTN Trazabilidad
BTN Imprimir (P)
BTN Activación de cita
WINDOW Menu de opciones
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
FIELD[textfield] textfield-1033
FIELD[textfield] textfield-1035
FIELD[textfield] textfield-1037
FIELD[textfield] textfield-1039
FIELD[textfield] textfield-1041
FIELD[textfield] textfield-1043
FIELD[textfield] textfield-1045
FIELD[textfield] textfield-1047
FIELD[textfield] textfield-1049
FIELD[textfield] textfield-1052
FIELD[textfield] textfield-1055
FIELD[textfield] textfield-1057
FIELD[datefield] Fecha
FIELD[combobox] Listado de Estados {CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}
BTN Nuevo Ingreso
BTN Actualizar
GRID Turnos Procedimientos: TURNO | SEDE ATENCIÓN | FECHA ASIGNACIÓN | TD | DOCUMENTO | NOMBRE | EMPRESA | ACUDIENTE | TIPO PROCEDIMIENTO | PROCEDIMIENTOS | MEDICO ATIENDE | CONTRATO
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombreP
FIELD[textfield] Buscar
BTN Buscar Paciente
BTN Crear Paciente
BTN Editar Datos del paciente
FIELD[combobox] Tipo Afiliado ingreso: {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[combobox] Modalidad de atención {INTRAMURAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[combobox] Prestador de Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Categorias
FIELD[combobox] Tipo programa especial: {NO APLICA}
FIELD[combobox] Equipo de atención
FIELD[textfield] TextTipoPaciente
FIELD[combobox] Unidad funcional {AMBULATORIO}
FIELD[combobox] Grupo de servicio {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}
FIELD[combobox] Servicios
PANEL DATOS DE LA AGENDA
FIELD[datefield] FechaSolicitudCita
FIELD[timefield] HoraTurno
FIELD[datefield] FechaQueriaPaciente
FIELD[datefield] FechaAsignacion
FIELD[combobox] GESTANTECHECK {SI, NO}
FIELD[combobox] ViaIngreso {DEMANDA ESPONTANEA, DERIVADO DE CONSULTA EXTERNA, DERIVADO DE URGENCIAS, DERIVADO DE HOSPITALZACION, DERIVADO DE SALA DE CIRUGIA, DERIVADO DE SALA DE PARTOS, RECIEN NACIDO EN LA INSTITUCION, RECIEN NACIDO EN OTRA INSTITUCION, DERIVADO O REFERIDO DE HOSPITALIZACION DOMICILIARIA, DERIVADO DE ATENCION DOMICILIARIA, DERIVADO DE TELEMEDICINA, DERIVADO DE JORNADA DE SALUD, REFERIDO DE OTRA INSTITUCION, CONTRAREFERIDO DE OTRA INSTITUCION}
FIELD[combobox] ComboTipoCita {PROCEDIMIENTO EXTERNO, CITOLOGIA, PLANIFICACIÓN, VACUNACION}
FIELD[combobox] COMBOCATEGORIAPROCEDIMIENTO
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboContrato
FIELD[combobox] Atiende {<valores omitidos: nombres de personas y sedes>}
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[textareafield] TextObservacion
PANEL Información del procedimientos
PANEL Fotografia
FIELD[filefield] SubirArchivo
BTN Obtener firma
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
PANEL Huella Digital
PANEL Datos Biometricos
GRID : Código | Descripción | Cantidad | Observación
FIELD[checkboxfield] Primera vez del tratamiento de reumatología:
BTN Eliminar
PANEL Procedimientos
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Codigo | Descripción | Prioridad
PANEL Diagnóstico
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Adjuntos
FIELD[combobox] Categoria: {ADMINISTRATIVO}
FIELD[combobox] Tipo soporte digital:
FIELD[combobox] Relaciòn con el paciente:
GRID Listado de soportes digitales: Categoria | No Autorización | Tipo de soporte digital | Fecha de creacion | Registrado por | PDF | Modificar | Eliminar
PANEL Adjuntos Digitales
FIELD[textfield] TextFechaFilter
FIELD[textfield] TextTurnoFilter
FIELD[textfield] TextHoraFilter
FIELD[textfield] TextMedicoFilter
FIELD[textfield] TextRegistraCitaFilter
FIELD[textfield] TextMotivoCambioEstadoFilter
FIELD[textfield] TextTipoAsignacionFilter
FIELD[textfield] TextEstadoFilter
GRID : Fecha | Turno | Hora | Medico | Registrado por | Nota | Tipo asignación | Estado
PANEL Historial
GRID : Datos de adjunto
PANEL Adjuntos Fisicos
BTN Descargar
BTN Zoom +
BTN Zoom -
BTN Rotar ↻
BTN Rotar ↺
BTN Restablecer
PANEL Vista previa
BTN Imprimir
BTN Guardar y cerrar
BTN Salir
WINDOW Asignar Procedimientos
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
WINDOW Registrar nuevo paciente
WINDOW Gestion del paciente
GRID : Codigo | Descripción
WINDOW Coincidencias encontradas en el CIE10
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjunto fisico
BTN Cerrar
WINDOW Imagen Adjunta
FIELD[textfield] txtCopaId
FIELD[textfield] txtAgenda
FIELD[textfield] txtAgendaId
FIELD[combobox] Resolución
BTN Enviar
WINDOW Enviar Copago a Dian
FIELD[textfield] Nombre del archivo
FIELD[combobox] Formato {PNG, JPG}
WINDOW Descargar Imagen
WINDOW Concentimiento

## CITAS MEDICAS > TURNO RAYOS X (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaRayosx.aspx)
ERR c.getColumnManager is not a function

## CITAS MEDICAS > TURNOS LABORATORIO (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaUrgencia.aspx)
ERR c.getColumnManager is not a function

## CITAS MEDICAS > OLD > AGENDA UROLOGÍA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Instancias/TurnoInstanciaUrologia.aspx)
TITLE Turno Urgencia
GRID : Código | Descripción | Tipo manual
BTN Aceptar
BTN Cancelar
WINDOW Coincidencias encontradas
GRID : Codigo | Descripción
BTN Salir
WINDOW Coincidencias encontradas en el CIE10
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Celular
BTN Guardar
WINDOW Datos del Acudiente
GRID : DOCUMENTO | NOMBRE
WINDOW Coincidencias Encontradas
FIELD[combobox] Motivo:
FIELD[textareafield] Observación
WINDOW Eliminar Turno de Urgencia
BTN Cancelar Turno >>>
BTN Modificar Turno
WINDOW Menú de Opciones
WINDOW Registrar Nuevo Paciente
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
WINDOW Datos del responsable
WINDOW Datos del acompañante
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
FIELD[combobox] Especialidad
WINDOW Agregar Médico Externo
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico: {PRE-INGRESO, PERIÓDICO, EGRESO, TRABAJO EN ALTURAS, MANIPULACIÓN DE ALIMENTOS, POST-INCAPACIDAD, CAMBIO DE OCUPACIÓN}
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
FIELD[combobox] Departamento
FIELD[combobox] Municipio
WINDOW Municipio
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
FIELD[textfield] Buscar
BTN Buscar
BTN Crear Paciente
FIELD[combobox] Empresa {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombreP
FIELD[textfield] TextFechaNacimiento
FIELD[textfield] TextGenero
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[textfield] TextEmpresa
FIELD[textfield] TextMunicipio
FIELD[textfield] TextDireccion
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
BTN Actualizar Paciente
BTN Guardar Cambios
FIELDSET Datos personales del paciente
FIELD[textfield] TextFechaFilter
FIELD[textfield] TextTurnoFilter
FIELD[textfield] TextHoraFilter
FIELD[textfield] TextMedicoFilter
FIELD[textfield] TextRegistraCitaFilter
FIELD[textfield] TextMotivoCambioEstadoFilter
FIELD[textfield] TextTipoAsignacionFilter
FIELD[textfield] TextEstadoFilter
GRID : Fecha | Turno | Hora | Medico | Registrado por | Nota | Tipo asignación | Estado
PANEL Historial de Citas Medicas
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS}
FIELD[textfield] TextAcudiente
BTN Asignar datos del acompañante
BTN Borrar acompañante
FIELD[datefield] FechaSolicitudCita
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[textfield] TextNumeroAutorizacion
FIELD[textareafield] TextObservacion
PANEL Información de la cita
PANEL Fotografia
FIELD[filefield] SubirArchivo
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
PANEL Huella Digital
PANEL Datos Biometricos
GRID : Código | Descripción | Cantidad | Observación
FIELD[combobox] Médico remite:
BTN Nuevo Médico
FIELD[combobox] IPS que emite:
BTN Nueva IPS
BTN Eliminar
PANEL Procedimientos
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Codigo | Descripción | Prioridad
PANEL Diagnóstico
BTN Imprimir
BTN Guardar y cerrar
WINDOW Asignar cita
BTN Pasar al modo de edición de código fuente.
FIELD[htmleditor] AreaDescripcion
WINDOW HTML
GRID : Medico/Especialidad
FIELD[textfield] textfield-1135
FIELD[textfield] textfield-1138
FIELD[textfield] textfield-1140
FIELD[textfield] textfield-1142
FIELD[textfield] textfield-1144
FIELD[textfield] textfield-1146
FIELD[textfield] textfield-1148
FIELD[textfield] textfield-1150
FIELD[textfield] textfield-1152
FIELD[textfield] textfield-1154
FIELD[textfield] textfield-1156
FIELD[datefield] Fecha
FIELD[timefield] Hora
FIELD[combobox] Estado de la cita {EN ESPERA, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO}
BTN Nueva Cita
BTN Actualizar
GRID Programación de citas UROLOGÍA: Turno | Turno | Hora | Documento | Paciente | Empresa | Regimen | Medico/Entidad Solicita | Fecha asignación | Registrado por | Estado

## CITAS MEDICAS > OLD > ASIGNACIÓN CITA MEDICA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/AsignacionCitaMedica.aspx)
TITLE Asignacion cita Medica
GRID : Descripción
BTN Aceptar
BTN Cancelar
WINDOW Dispositivos
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
BTN Tomar Fotografia
BTN Guardar Fotografia
BTN Salir
WINDOW Tomando Foto del Paciente
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
WINDOW Datos del responsable
WINDOW Datos del acompañante
WINDOW Registrar nuevo paciente
FIELD[textfield] Buscar
BTN Buscar Paciente
BTN Crear Paciente
FIELD[combobox] Prestador de Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Tipo de Consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombreP
FIELD[textfield] TextEdad
FIELD[textfield] TextFechaNacimiento
FIELD[textfield] TextGenero
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[textfield] TextEmpresa
FIELD[textfield] TextMunicipio
FIELD[textfield] TextDireccion
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
BTN Modificar
BTN Actualizar Paciente
BTN Guardar Cambios
FIELDSET Datos personales del paciente
FIELD[textfield] TextFechaFilter
FIELD[textfield] TextTurnoFilter
FIELD[textfield] TextHoraFilter
FIELD[textfield] TextMedicoFilter
FIELD[textfield] TextRegistraCitaFilter
FIELD[textfield] TextMotivoCambioEstadoFilter
FIELD[textfield] TextTipoAsignacionFilter
FIELD[textfield] TextEstadoFilter
GRID : Fecha | Turno | Hora | Medico | Registrado por | Nota | Tipo asignación | Estado
PANEL Historial de Citas Medicas
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA}
FIELD[combobox] ComboBoxSubsRPMS
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[datefield] FechaSolicitudCita
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboContrato
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[checkboxfield] Gestante
FIELD[textareafield] TextObservacion
PANEL Información de la cita
PANEL Fotografia
FIELD[filefield] SubirArchivo
BTN Obtener firma
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
PANEL Huella Digital
PANEL Datos Biometricos
GRID : Código | Descripción | Cantidad | Observación
FIELD[checkboxfield] Primera vez del tratamiento de reumatología:
BTN Eliminar
PANEL Procedimientos
FIELD[textfield] Codigo/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Codigo | Descripción | Prioridad
PANEL Diagnóstico
BTN Agregar
BTN Actualizar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Adjuntos
BTN Imprimir
BTN Guardar y cerrar
BTN Guardar
WINDOW Asignar cita
BTN Asignar cita
BTN Modificar cita (M)
BTN Eliminar cita (Supr)
BTN Cambiar de turno (C)
BTN Transferir cita (T)
BTN Asigna cita de transferencia (T)
BTN Imprimir (P)
BTN Asignar turno
BTN Eliminar cita opcional
BTN Ver nota inasistencia
BTN Activación de cita
BTN Volver a asignado
BTN Escala de Caidas
WINDOW Menu de opciones
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
FIELD[combobox] Motivo
FIELD[textareafield] Observación
WINDOW Eliminar cita
FIELD[combobox] Jornada
FIELD[combobox] Turnos disponibles
WINDOW Cambio de turno
FIELD[numberfield] Numero citas
WINDOW Adicionar citas a la agenda
WINDOW Seleccione la nueva fecha
BTN Octubre 2026
BTN Hoy
FIELD[displayfield] ctl368
FIELD[textfield] textfield-1125
GRID : MEDICO
WINDOW Medicos disponible para transferir
GRID Turnos: 
FIELD[displayfield] ctl395
FIELD[textfield] textfield-1136
FIELD[combobox] Especialidad
GRID Lista de medicos: MEDICO
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[numberfield] TextAno
GRID Agenda: DOM | LUN | MAR | MIE | JUE | VIE | SAB
BTN Cambiar fecha de la agenda
BTN Transferir la agenda a otro medico
BTN Activar toda la agenda
BTN Opciones
FIELD[displayfield] TextPacientTR
GRID Citas programadas: AGCI ID | JORNADA | HORA | TURNO | DOCUMENTO | NOMBRE PACIENTE | TIPO CITA | EMPRESA | REGIMEN | MEDIO SOLICITUD | FECHA ASIGNACIÓN | REGISTRADO POR | ESTADO
TOOLTIP Actualizar
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
WINDOW Agregar Médico Externo
FIELD[combobox] Departamento
FIELD[combobox] Municipio
WINDOW Municipio
GRID : Codigo | Descripción
WINDOW Coincidencias encontradas en el CIE10
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjunto fisico
WINDOW Recibo de pago
WINDOW Gestion del paciente
BTN Cerrar
WINDOW Imagen Adjunta

## CITAS MEDICAS > OLD > GESTIONA TURNO URGENCIA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/TurnoUrgencias.aspx)
TITLE Turno Urgencia
BTN Guardar
BTN Limpiar
BTN Cancelar
WINDOW FIRMAR INGRESO
FIELD[textfield] NOMBRE
FIELD[textfield] NIT
FIELD[textfield] DIRECCION
FIELD[textfield] EMAIL
FIELD[textfield] TELEFONO
FIELD[textfield] CODIGO ENTIDAD
FIELD[combobox] REGIMEN
FIELD[combobox] Plan Unico de Cuenta:
BTN GUARDAR
BTN CANCELAR
WINDOW Crear Empresa
FIELD[combobox] DEPARTAMENTO
FIELD[combobox] MUNICIPIO
WINDOW Lugar de remisión
FIELD[textfield] CodigoEmpresaRemision
FIELD[textfield] DepartamentoMunicipio
BTN Lugar de remisión
BTN Cerrar
WINDOW Datos de remisión
GRID : Descripción
BTN Aceptar
WINDOW Dispositivos
FIELD[combobox] DestinoEnfermeria {HOSPITALIZACIÓN}
WINDOW Unidad Funcional
FIELD[combobox] CONDICIÓN DEL ACCIDENTADO
FIELD[combobox] NATURALEZA DEL EVENTO
FIELD[combobox] TIPO DE EVENTO
FIELD[datefield] FECHAEVENTOACCIDENTE
FIELD[timefield] HORAEVENTO
FIELD[textfield] DIRECCIONACCIDENTE
FIELD[radiofield] RURAL
FIELD[radiofield] URBANO
FIELD[radiogroup] ZONA
FIELD[textareafield] CARACTERISTICASACCIDENTE
WINDOW Datos de accidente
FIELD[textfield] TextBuscarPaciente
BTN Buscar Paciente
FIELD[checkboxfield] Sin Contrato
FIELD[combobox] Modo ingreso {URGENCIAS, CONSULTA EXTERNA O PROGRAMADA, REMITIDO, NACIDO EN LA INSITUCIÓN}
BTN Transito
BTN Trabajo Informal
BTN Accidente
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombre
FIELD[textfield] TextFechaNacimiento
FIELD[textfield] TextGenero
FIELD[textfield] textCelular
FIELD[textfield] TextTelefono
FIELD[textfield] TextDireccion
FIELD[textfield] Textmunicipio
FIELD[textfield] TextEmpresa
FIELD[textfield] TextAcudienteUrgencia
BTN Asignar datos del Acudiente
FIELD[combobox] ComboBoxIdPrestadorServicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] Contrato
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[textfield] txtbusquedaprocedimiento
FIELD[textfield] Nombre del procedimiento
BTN Modificar
FIELD[checkboxfield] PacienteGestante
FIELD[combobox] LaborParto {SI, NO}
FIELD[textareafield] TexAreaObservacionUrgencia
FIELD[textfield] NombreLugarRemision
FIELD[textfield] CodigoRemision
FIELD[textfield] LugarRemisionText
PANEL Datos del prestador de servicios de salud que remite
BTN Agregar
BTN Actualizar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Lista de adjuntos
PANEL Fotografia
FIELD[filefield] SubirArchivo
BTN Obtener firma
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
PANEL Huella Digital
PANEL Datos Biometricos
BTN Guardar y cerrar
WINDOW Datos Personales
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Celular
WINDOW Datos del Acudiente
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjunto fisico
GRID : DOCUMENTO | NOMBRE
WINDOW Coincidencias Encontradas
GRID : CODIGO | PROCEDIMIENTO
FIELD[combobox] Motivo:
FIELD[textareafield] Observación
WINDOW Eliminar Turno de Urgencia
BTN Cancelar Turno
BTN Modificar Turno
WINDOW Menú de Opciones
WINDOW Registrar Nuevo Paciente
GRID : Documento | Nombre paciente
WINDOW Coincidencia con el parámetro ingresado
FIELD[textfield] textfield-1106
FIELD[textfield] textfield-1108
FIELD[textfield] textfield-1110
FIELD[textfield] textfield-1112
FIELD[textfield] textfield-1114
FIELD[textfield] textfield-1116
FIELD[textfield] textfield-1118
FIELD[textfield] textfield-1120
FIELD[textfield] textfield-1122
FIELD[textfield] textfield-1124
FIELD[textfield] textfield-1126
FIELD[textfield] textfield-1129
FIELD[datefield] Fecha
FIELD[combobox] Lista de Estados {EN ESPERA, ATENCIÓN TRIAGE, ESPERA CONSULTA, ATENCIÓN CONSULTA, ATENDIDO, CANCELADO, NO ASISTIO}
BTN Nuevo Ingreso
FIELD[textfield] Paciente
BTN Buscar
BTN Trazabilidad
GRID Turnos Urgencia: TURNO | FECHA ASIGNACIÓN | TD | DOCUMENTO | NOMBRE | CELULAR | EMPRESA | ACUDIENTE | OBSERVACIÓN | CODIGO | CONTRATO | Anexo
BTN Agregar signos Vitales
BTN Firmar Cita
FIELD[filefield] FileUploadField1
BTN Obtener Link
FIELD[filefield] FileUploadField2
FIELD[numberfield] Sist
FIELD[displayfield] DisplayField7
FIELD[numberfield] Dias
FIELD[displayfield] DisplayField1
FIELD[numberfield] TextFrecuenciaCardiaca
FIELD[displayfield] DisplayField2
FIELD[numberfield] TextFrecuenciaRespiratoria
FIELD[displayfield] DisplayField3
FIELD[numberfield] TextSaturacionOxigeno
FIELD[displayfield] DisplayField4
FIELD[numberfield] TextGlucometria
FIELD[displayfield] DisplayField5
FIELD[numberfield] TextPerimetroEncefalico
FIELD[displayfield] DisplayField10
FIELD[numberfield] TextFetocardia
FIELD[displayfield] DisplayField11
FIELD[numberfield] TextTemperatura
FIELD[displayfield] DisplayField6
FIELD[numberfield] TextPesoo
FIELD[displayfield] DisplayField8
FIELD[numberfield] TextTallaa
FIELD[displayfield] DisplayField9
FIELD[numberfield] IMC
FIELD[numberfield] M2
WINDOW Ingresar Signos Vitales
WINDOW Imagen Adjunta
FIELD[textareafield] OCUPACIONHABITUALOTROSACCIDENTES
FIELDSET OCUPACIÓN HABITUAL
FIELD[combobox] JORNADA DE TRABAJO HABITUAL
FIELD[radiofield] SI
FIELD[radiofield] NO
FIELD[radiogroup] DESPLAZADO
PANEL IDENTIFICACION GENERAL PERSONA ACCIDENTADA
FIELD[datefield] FECHAACCIDENTEOTROSACCIDENTE
FIELD[timefield] HORAACCIDENTEOTROSACCIDENTE
FIELD[radiogroup] ESTABA REALIZANDO SU LABOR HABITUAL
FIELD[combobox] TIPO DE ACCIDENTE
FIELD[combobox] TIPO DE LESION
FIELD[textareafield] SITIOACCIDENTEOTROSACCIDENTE
FIELDSET SITIO DONDE OCURRIO EL ACCIENTE
FIELD[textareafield] DESCRIPCIONLESIONOTROSACCIDENTES
FIELDSET DESCRIPCIÓN DE LESION
FIELD[textfield] OBJETOLESIONOTROSACCIDENTE
FIELD[textfield] PARTECUERPOAFECTADAOTROSACCIDENTES
PANEL INFORMACIÓN SOBRE EL ACCIDENTE
WINDOW DATOS DE OTROS ACCIDENTES LABORALES INFORMALES
WINDOW Gestion del paciente

## CITAS MEDICAS > OLD > CITA DEMANDA INDUCIDA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/CitaDemandaInducida.aspx)
TITLE Cita Demanda Inducida
BTN Guardar
BTN Limpiar
BTN Cancelar
WINDOW FIRMAR INGRESO
WINDOW Registrar Laboratorio
WINDOW Registrar Procedimiento Esterno
BTN No Realizo Consulta
BTN Atendido en Otra Institucion
WINDOW Menu de opciones
FIELD[textfield] Institucion
FIELD[datefield] Fecha Atencion
FIELD[textareafield] Observacion
WINDOW Registrar Datos
GRID : Descripción
BTN Aceptar
WINDOW Dispositivos
BTN Cambiar fecha de la agenda
BTN Transferir la agenda a otro medico
BTN Activar toda la agenda
BTN Opciones
FIELD[displayfield] TextPacientTR
BTN Actualizar
GRID : JORNADA | HORA | TURNO | DOCUMENTO | NOMBRE PACIENTE | TIPO CITA | EMPRESA | REGIMEN | MEDIO SOLICITUD | LUGAR DE RESIDENCIA | FECHA ASIGNACIÓN | REGISTRADO POR | ESTADO
WINDOW Registrar Citas
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
WINDOW Detalle datos del paciente
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
BTN Asignar cita
BTN Modificar cita (M)
BTN Eliminar cita (Supr)
BTN Cambiar de turno (C)
BTN Transferir cita (T)
BTN Asigna cita de transferencia (T)
BTN imprimir (P)
BTN Asignar turno
BTN Eliminar cita opcional
BTN Ver nota inasistencia
BTN Activación de cita
BTN Volver a asignado
BTN Trazabilidad
BTN Firmar ingreso
BTN Subir Laboratorios Pc
FIELD[combobox] EXAMI_ComboTipohistoriaLaboratorios {CONSULTA HIGIENE ORAL, ESPECIALES (CRONICOS), REUMATOLOGIA}
GRID : EXAMEN | VALOR
FIELD[numberfield] Sist
FIELD[displayfield] EXAMI_DisplayField7
FIELD[numberfield] Dias
FIELD[displayfield] EXAMI_DisplayField1
FIELD[numberfield] EXAMI_TextFrecuenciaCardiaca
FIELD[displayfield] EXAMI_DisplayField2
FIELD[numberfield] EXAMI_TextFrecuenciaRespiratoria
FIELD[displayfield] EXAMI_DisplayField3
FIELD[numberfield] EXAMI_TextGlucometria
FIELD[displayfield] EXAMI_DisplayField5
FIELD[numberfield] EXAMI_TextTemperatura
FIELD[displayfield] EXAMI_DisplayField6
FIELD[numberfield] EXAMI_TextPesoo
FIELD[displayfield] EXAMI_DisplayField8
FIELD[numberfield] EXAMI_TextTallaa
FIELD[displayfield] EXAMI_DisplayField9
FIELD[numberfield] EXAMI_TextIMCC
FIELD[numberfield] EXAMI_TextM2
FIELD[displayfield] Peso
FIELD[displayfield] Riesgo
FORM SIGNOS VITALES
PANEL Laboratorios
WINDOW Laboratorios Pre Consulta
BTN Traer datos Biometricos del Ingreso
BTN Obtener firma
BTN Aplicar datos al formato
FIELDSET Datos del paciente
PANEL Datos Biometricos paciente
FIELD[textfield] Documento de identidad:
FIELD[textfield] Nombre del testigo o responsable del paciente:
FIELD[textfield] Relaciòn con el paciente:
FIELDSET Datos del testigo o responsable del paciente
PANEL Datos Biometricos acompañante
FIELD[htmleditor] HtmlEditorPanelPrev
WINDOW GENERAR CONSENTIMIENTO INFORMADO
FIELD[textfield] Buscar
BTN Buscar Paciente
BTN Crear Paciente
FIELD[combobox] Prestador de Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Tipo de Consulta {PRESENCIAL, TELEMEDICINA, EXTRAMURAL, TELEORIENTACIÓN}
FIELD[textfield] TextTipoDocumento
FIELD[textfield] TextDocumentoP
FIELD[textfield] TextNombreP
FIELD[textfield] TextFechaNacimiento
FIELD[textfield] TextGeneroP
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[textfield] TextEmpresa
FIELD[textfield] TextMunicipio
FIELD[textfield] TextDireccion
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
BTN Modificar
BTN Actualizar Paciente
BTN Guardar Cambios
FIELDSET Datos personales del paciente
FIELD[combobox] ComboTipoCita {PRIMERA VEZ, CONTROL, PRIORITARIA, PyP, CONTROL POP, CIRUGIA PROGRAMADA, MEDICINA LABORAL, AFINAMIENTO, PREINGRESO, TRANSCRIPCIÓN DOCUMENTO, SALUD PUBLICA, LABORATORIO CLÍNICO, RAYOS X, IMAGENES DIAGNOSTICAS, PROCEDIMIENTOS, PAQUETE P890260, VACUNACION, CITOLOGIA VPH, CIRUGIA URGENCIADA, MIPRES, PROCEDIMIENTOS GASTROENTEROLOGOS, SALUD PUBLICA ENFERMERIA}
FIELD[combobox] ComboBoxSubsRPMS
FIELD[textfield] TextResponsable
BTN Asignar datos del responsable
BTN Borrar responsable
FIELD[textfield] TextAcudiente
BTN Asignar datos del acompañante
BTN Borrar acompañante
FIELD[datefield] FechaSolicitudCita
FIELD[combobox] ComboNumeroCitas {1, 2, 3, 4}
FIELD[combobox] ComboTipoAsignacion {PRESENCIAL, TELEFONICA}
FIELD[textfield] TextNumeroAutorizacion
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboContrato
FIELD[combobox] cbxInstitucionRemite
FIELD[combobox] cbxMedico
BTN Agregar Nuevo Médico Externo
FIELD[checkboxfield] Gestante
FIELD[textareafield] TextObservacion
PANEL Información de la cita
PANEL Fotografia
FIELD[filefield] SubirArchivo
PANEL Firma Digital
FIELD[filefield] SubirHuellaDactilar
PANEL Huella Digital
PANEL Datos Biometricos
GRID : Código | Descripción | Cantidad | Observación
FIELD[checkboxfield] Primera vez del tratamiento de reumatología:
BTN Eliminar
PANEL Procedimientos
BTN Agregar
GRID : Datos de adjunto | Datos administrativo | Datos de archivo
PANEL Ajuntos Fisicos
FIELD[combobox] Categoria: {ADMINISTRATIVO}
FIELD[combobox] Tipo soporte digital:
FIELD[combobox] Relaciòn con el paciente:
FIELDSET Nuevo soporte
GRID Listado de soportes digitales: Categoria | No Autorización | Tipo de soporte digital | Fecha de creacion | Registrado por | PDF | Modificar | Eliminar
PANEL Ajuntos Digitales
BTN Imprimir
BTN Guardar y cerrar
WINDOW Asignar cita
FIELD[filefield] FileUploadField1
FIELD[filefield] FileUploadField2
BTN GUARDAR
BTN CANCELAR
FIELD[datefield] Fecha Ingreso a la empresa:
FIELD[combobox] Tipo de examen médico:
FIELD[textfield] Empresa Contratante:
FIELD[textfield] Empresa en Misión:
FIELD[textfield] Cargo:
PANEL Datos Laborales
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
BTN Tomar Fotografia
BTN Guardar Fotografia
BTN Salir
WINDOW Tomando Foto del Paciente
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
FIELD[textfield] EPS afiliado
WINDOW Datos del responsable
WINDOW Datos del acompañante
WINDOW Registrar nuevo paciente
FIELD[combobox] Motivo
FIELD[textareafield] Observación
WINDOW Eliminar cita
FIELD[combobox] Jornada
FIELD[combobox] Turnos disponibles
WINDOW Cambio de turno
FIELD[numberfield] Numero citas
WINDOW Adicionar citas a la agenda
WINDOW Seleccione la nueva fecha
BTN Octubre 2026
BTN Hoy
FIELD[displayfield] ctl585
FIELD[textfield] textfield-1314
GRID : MEDICO
WINDOW Medicos disponible para transferir
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
BTN Crear nuevo paciente
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombre
FIELD[textfield] TextGenero
FIELD[textfield] TextFNacimiento
FIELD[textfield] TextEdad
FIELD[netmulticombo] Jornadas {TURNO 1, TURNO 2, TURNO 3, TURNO 4, TURNO 5, TURNO 6, TURNO 7, TURNO 8, TURNO 9, TURNO 10}
BTN Información paciente
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
GRID : Descripcion | Cups | Fecha | Hora | Tipo de Cita | Registrado Por | Medico | Tipo de Consulta | Estado | Factura
FIELD[combobox] Seleccione
FIELD[textfield] textfield-1350
FIELD[displayfield] ctl666
FIELD[displayfield] ctl670
FIELD[displayfield] ctl674
FIELD[displayfield] ctl678
FIELD[displayfield] ctl682
FIELD[displayfield] ctl686
FIELD[displayfield] ctl690
FIELD[displayfield] ctl694
GRID : PROGRAMA RES. 3280 | PROFESIONAL QUE PUEDE REALIZAR | Ver sólo actividades pendientes | Programadas | Inasistencia | Ejecutadas | Fecha ultima ejecutada | Especialidad ultima ejecucion | Programada | Fecha ultima programada | Especialidad ultima programada
FIELD[textfield] TextNombreFilter
FIELD[combobox] Especialidad
GRID PROFESIONAL DE LA SALUD: PROFESIONAL | PROFESIONAL | % de Agenda
GRID OTRAS AGENDAS:
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[numberfield] TextAno
GRID Agenda: DOM | LUN | MAR | MIE | JUE | VIE | SAB
TOOLTIP Actualizar
FIELD[combobox] Title {ADMINISTRATIVO, CLINICO, DILIGENCIAMIENTO DE ARCHIVOS}
FIELD[combobox] Title
FIELD[textfield] DescripcionAdjuntoFisico
FIELD[filefield] AddAdjuntoFisico
WINDOW Adjuntos
WINDOW Imagen Adjunta
WINDOW Recibo de pago
WINDOW Gestion del paciente
FIELD[textfield] Primer Nombre:
FIELD[textfield] Segundo Nombre:
FIELD[textfield] Primer Apellido:
FIELD[textfield] Segundo Apellido:
FIELD[textfield] Registro Profesional:
WINDOW Agregar Médico Externo
FIELD[textfield] TxtMunicipioIps
BTN Buscar Municipio
FIELD[textfield] Nit:
FIELD[textfield] Nombre:
FIELD[combobox] ComboEstado {ACTIVO, INACTIVO}
WINDOW Agregar Institución
FIELD[combobox] Departamento
FIELD[combobox] Municipio
WINDOW Municipio

## CITAS MEDICAS > OLD > MALLA REUMATOLOGIA (/SUROSHistoriaClinica/Vistas/Privado/Agenda/MallaReumatologia.aspx)
TITLE Malla Reumatologia
WINDOW Registrar Cita Medica
FIELD[textfield] Buscar
BTN Buscar
BTN Agregar a Malla
GRID : # PACIENTE | FECHA DE ATENCION REUMATOLOGIA | EMPRESA | DOCUMENTO | NOMBRE | APELLIDO | RESIDENCIA | DEPARTAMENTO
WINDOW Agregar Paciente
GRID : # | USUARIO REGISTRA | FECHA DE CREACION | ESTADO | ACCIONES
WINDOW Historial de mallas Creadas
WINDOW Visor de mallas Creadas
FIELD[datefield] Fecha Inicial
FIELD[datefield] Fecha Final
FIELD[datefield] Fecha Agendacion Citas
FIELD[netmulticombo] Especialidades {PSICOLOGÍA, NUTRICIÓN, FISIOTERAPIA, TERAPIA OCUPACIONAL, REUMATOLOGIA, MEDICAMENTOS, ENFERMERÍA}
FIELD[netmulticombo] Empresas {TODOS, PIJAOS SALUD E.P.S.I(SUBSIDIADO), PARTICULAR(OTRO), ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA(OTRO), ASMET SALUD EPS SAS(SUBSIDIADO), ASMET SALUD EPS SAS(CONTRIBUTIVO)}
BTN Consultar
BTN Historial de Mallas
BTN Nueva Malla
BTN Descartar Malla
BTN Guardar
BTN Terminar y Guardar
BTN Agregar Paciente
PANEL LISTADO DE PACIENTES REUMATOLOGIA

## CONFIGURACION GENERAL > CONFIGURACIÓN GENERAL (/SUROS/Vistas/Privado/General/ConfiguracionGeneral.aspx)
TITLE Configuración General
GRID : Id | Configuración
BTN Guardar Configuracion
BTN Editar esta configuración

## CONFIGURACION GENERAL > FUNCIONARIO > GESTIONAR DATOS FUNCIONARIO (/SUROSHistoriaClinica/Vistas/Privado/Funcionario/FormularioFuncionario.aspx)
TITLE Formulario funcionario
GRID : PROGRAMA PYP
BTN GUARDAR CAMBIOS
BTN Cancelar
WINDOW Seleccionar los programas asociados
BTN Aceptar
WINDOW Seleccionar firma
FIELD[combobox] Pais
FIELD[combobox] Departamento
FIELD[combobox] Municipio
FIELD[checkboxfield] .
WINDOW Municipio
GRID : DOCUMENTO | NOMBRE FUNCIONARIO
WINDOW Coincidencia encontrada
FIELD[displayfield] ctl45
FIELD[textfield] textfield-1028
FIELD[textfield] textfield-1030
GRID : Descripcion
WINDOW Especialidad medica
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field
FIELD[displayfield] ctl64
FIELD[textfield] textfield-1093
GRID : Empresa
WINDOW Convenios
WINDOW Asignar firma
FIELD[combobox] ctl168 {ACTIVO, INACTIVO}
FIELD[combobox] ctl172 {SI, NO}
FIELD[combobox] ctl176 {SI, NO}
FIELD[combobox] ComboTipoDocumento {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}
FIELD[textfield] TextDocumento
FIELD[combobox] ComboGenero {MASCULINO, FEMENINO, INDETERMINADO O INTERSEXUAL}
FIELD[datefield] dd/mm/yyyy
FIELD[combobox] ComboOcupacion
FIELD[combobox] ComboCargo
FIELD[textfield] TextPNombre
FIELD[textfield] TextSNombre
FIELD[textfield] TextPApellido
FIELD[textfield] TextSApellido
FIELD[textfield] TextEmail
FIELD[combobox] ComboEmpresa
FIELD[textfield] TextMunicipioNac
BTN Buscar Municipio
FIELD[textfield] TextMunicipioRec
FIELD[combobox] ComboEtnia {OTRAS ETNIAS, INDIGENA, RAIZAL (ARCHIPIELAGO SAN ANDRÉS Y PROVIDENCIA), GITANO, PALENQUERO DE SAN BASILIO, NEGRO(A) O MULATO(A) O AFROCOLOMBIANO(A) O AFRODESCENDIENTE, AFROCOLOMBIANO}
FIELD[combobox] ComboEstadoCivil {ESTADO NO SUMINISTRADO, CASADO(A), DIVORCIADO(A), MENOR DE EDAD, SOLTERO(A), UNION LIBRE, VIUDO}
FIELD[combobox] ComboDiscapacidad {DISCAPACIDAD FÍSICA, DISCAPACIDAD VISUAL, DISCAPACIDAD AUDITIVA, DISCAPACIDAD INTELECTUAL, DISCAPACIDAD SICOSOCIAL, SORDOCEGUERA, DISCAPACIDAD MÚLTIPLE, SIN DISCAPACIDAD}
FIELD[combobox] ComboNivelEducativo {NO DEFINIDO, PRESCOLAR, BASICA PRIMARIA, BASICA SECUNDARIA, MEDIA ACADEMICA O CLASICA, MEDIA TECNICA, NORMALISTA, TECNICA PROFESIONAL, TECNOLOGICA, PROFESIONAL, ESPECIALIZACION, MAESTRIA, DOCTORADO}
FIELD[textfield] Calle/Carrera 22 # 4-5A Barrio
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
FIELD[combobox] Es medico
FIELD[combobox] Estado {ACTIVO, INACTIVO}
FIELD[textfield] Registro Profesional:
FIELD[textfield] Lic. salud ocupacional:
FIELDSET Información general del médico
GRID : Especialidad | Estado | Cirugia | PyP
BTN Adicionar especialidad
GRID : Convenio
BTN Adicionar convenio
FIELD[filefield] SubirArchivo
FIELD[textfield] Documento/Nombre
BTN Buscar funcionario
FIELD[combobox] ComboEstadoFuncionario
BTN LIMPIAR FORMULARIO
FORM Gestionar datos del funcionario

## CONFIGURACION GENERAL > FUNCIONARIO > USUARIO Y CONTRASEÑA (/SUROS/Vistas/Privado/Usuario/UsuarioCredenciales.aspx)
TITLE Usuario credenciales
FIELD[textfield] Usuario
FIELD[textfield] Contraseña
FIELD[textfield] Confirmar contraseña
BTN Aceptar
BTN cancelar
WINDOW Asignar contraseña a usuario
FIELD[combobox] ctl30 {ACTIVO, INACTIVO}
FIELD[triggerfield] Nombre persona
BTN Actualizar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
GRID Usuarios: Tipo Docum | Documento | Nombre persona | Nombre usuario | Estado usuario
BTN Asignar contraseña a usuario.
BTN Eliminar usuario
BTN Crear usuario

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN ROL A USUARIO (/SUROS/Vistas/Privado/Usuario/Roles/RolUsuario.aspx)
TITLE Rol Usuario
GRID : Descripción | Permiso
FIELD[combobox] ComboModulosIndirectos {ACTIVACION DE CITA, ACTIVIDADES DE ENFERMERIA, AGENDA MEDICA, CARGAR INVENTARIOS, CATALOGOMEDICAMENTO.ASPX, CONSULTA EXTERNA, HISTORIA CRONICOS, HISTORIA URGENCIA, INICIO, INICIO HISTORIA, PEDIDOS INTERNOS, REPORTE CITAS MEDICAS}
BTN Actualizar lista de permisos
BTN Aceptar
BTN Cancelar
WINDOW Gestionar permisos a modulos indirectos
FIELD[textfield] Buscar especialidad:
FIELD[checkboxfield] VerTodos
FIELD[checkboxfield] VerPropios
FIELD[checkboxfield] ImprimirTodos
FIELD[checkboxfield] ImprimirPropios
GRID : Descripción | Todos | Propios | Todos | Propios
FIELD[combobox] ComboOtrosPermisos {INICIO HISTORIA}
WINDOW Gestionar otros permisos
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
FIELD[triggerfield] Nombre persona
GRID Usuarios: Documento | Nombre persona | Nombre usuario | Estado usuario
BTN Otros Permisos
GRID Rol asignado: Rol
BTN Elimina el rol del usuario seleccionado
BTN Asigna rol a usuario seleccionado
FIELD[displayfield] ctl264
FIELD[textfield] textfield-1146
GRID Rol disponible: Rol

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN INFORMES USUARIO (/SUROS/Vistas/Privado/Usuario/AsignacionInformeUsuario.aspx)
TITLE Rol Usuario
FIELD[triggerfield] Nombre persona
GRID FUNCIONARIOS: Documento | Nombre persona | Nombre usuario | Estado usuario
FIELD[triggerfield] TriggerField1
BTN Agregar Nuevo Reporte
TREE INFORMES DISPONIBLES
BTN Asigna informe a usuario seleccionado
BTN Elimina el informe del usuario seleccionado
GRID INFORMES ASIGNADOS: ID | CODIGO | INDICADOR | DOMINIO | RESOLUCION
FIELD[textfield] NombreP
FIELD[textfield] TextNombreP
FIELD[textfield] TextUrl
GRID : Nombre | Nombre pagina | Url pagina
BTN Actualiza lista de paginas
BTN Aceptar
BTN Cancelar
WINDOW Paginas disponibles
FIELD[textfield] Nombre Grupo
FIELD[textfield] Nombre Carpeta
FIELD[textfield] Nombre Reporte
FIELD[textfield] Pagina
BTN Mostrar lista de paginas disponibles
BTN Guardar
BTN Salir
WINDOW Agregar Reporte
LABEL 200
LABEL OK
FIELD[htmleditor] htmleditor-1063
WINDOW Request Failure

## CONFIGURACION GENERAL > CONFIGURACION ENTIDAD HOSPITALARIA (/SUROS/Vistas/Privado/General/InformacionEntidad.aspx)
TITLE Informacion entidad
BTN Si
MESSAGEBOX Notificación
FIELD[combobox] ComboValor
FIELD[textfield] TextNombre
FIELD[textfield] TextNit
FIELD[textfield] TextCorreo
FIELD[textfield] TextDireccion
FIELD[textfield] TextTelefono
FIELD[textfield] TextCiudad
FIELD[numberfield] TextNivell
FORM Información general
GRID Configuración general: Item | Nombre | Descripción | Valor
BTN Guardar
BTN Sort Ascending
BTN Sort Descending
BTN Columns
BTN Group by this field

## CONFIGURACION GENERAL > GESTIONAR ESPECIALIDAD (/SUROSHistoriaClinica/Vistas/Privado/Medico/Especialidad.aspx)
TITLE Especialidad medico
FIELD[datefield] CampoFecha
FIELD[textfield] Nombre
FIELD[combobox] Multiple cita {SI, NO}
BTN Aceptar
BTN Cancelar
FIELD[textfield] Recurso 1
FIELD[textfield] Recurso 2
FIELD[checkboxfield] Otras Evoluciones
FIELD[checkboxfield] Permite Remontar Agenda
FIELD[checkboxfield] Formula Medica Otras Evoluciones
FIELD[checkboxfield] Mostrar Panel Escala detección riesgo suicida en otras evoluciones?
FIELDSET Recurso que un médico utilizara al momento de atender a un paciente desde la agenda medica
FIELD[displayfield] ctl19
FIELD[textfield] textfield-1019
GRID Modulo(Recurso): Nombre
FIELD[displayfield] ctl41
FIELD[textfield] textfield-1028
FIELD[textfield] TextField1
FIELD[displayfield] ctl91
FIELD[textfield] textfield-1038
FIELD[textfield] textfield-1041
BTN Nuevo
BTN Editar
BTN Eliminar
GRID Tipo especialidad: Descripción | Multiple cita
FIELD[displayfield] ctl152
FIELD[textfield] textfield-1055
FIELD[textfield] textfield-1058
FIELD[textfield] textfield-1061
FIELD[textfield] textfield-1064
FIELD[displayfield] ctl124
FIELD[textfield] textfield-1075
GRID : Tipo especialidad
BTN Transferir a
GRID Especialidad: Modulo(Recurso) principal | Modulo(Recurso) secundario | Otras Evoluciones
FIELD[displayfield] displayfield-1088
FIELD[textfield] TIES_NOMBRE
FIELD[combobox] TIES_MULTIPLECITA {SI, NO}

## CONFIGURACION GENERAL > PAGINAS DEL SISTEMA (/SUROS/Vistas/Privado/General/Paginas.aspx)
TITLE Paginas del sistema
FIELD[combobox] Estado {ACTIVO, INACTIVO}
FIELD[textfield] Nombre pagina
FIELD[textfield] Url
BTN Aceptar
BTN Cancelar
WINDOW Adicionar pagina al sistema
BTN Crear una nueva pagina
BTN Actualizar arbol
TREE Recursos disponibles del sistema
FIELD[textfield] TextID
FIELD[textfield] NombreP
FIELD[textfield] TextUrl
FIELD[textfield] TextPagina
BTN Actualizar lista
GRID Paginas disponibles en el sistema: ID | Nombre | Url pagina | Nombre pagina | Estado
BTN Eliminar pagina del sistema

## CONFIGURACION GENERAL > ROLES Y MODULOS (/SUROS/Vistas/Privado/Usuario/Roles/RolModulos.aspx)
TITLE Rol modulos
BTN Actualizar lista
BTN Aceptar
BTN Cancelar
WINDOW Iconos disponibles
GRID : Tipo doc | Numero documento | Nombre usuario
BTN Salir
WINDOW Usuarios asociados al rol
FIELD[combobox] Estado {ACTIVO, INACTIVO}
FIELD[combobox] Tipo rol
FIELD[textfield] Nombre rol
FIELD[textareafield] Observacion
FIELD[checkboxfield] Programa Agenda
WINDOW Nuevo rol
FIELD[textfield] NombreP
FIELD[textfield] TextNombreP
FIELD[textfield] TextUrl
GRID : Nombre | Nombre pagina | Url pagina
BTN Actualiza lista de paginas
WINDOW Paginas disponibles
FIELD[textfield] Nombre modulo
FIELD[numberfield] Orden
FIELD[textfield] Pagina
BTN Mostrar lista de paginas disponibles
FIELD[textfield] Icono
BTN Mostrar lista de icono disponibles
FIELD[combobox] Especialidad
WINDOW Adicionar Modulo
GRID : Usuario | Programa Agenda
WINDOW Copiar modulos a otro rol
BTN Editar nombre
BTN Editar Modulo
BTN Eliminar modulo
BTN Adicionar grupo
BTN Adicionar modulo
BTN Insertar en este grupo
BTN Copiar a otro rol
GRID : Descripción | Permiso
FIELD[combobox] ComboModulosIndirectos
BTN Actualizar lista de permisos
WINDOW Gestionar permisos a modulos indirectos
FIELD[textfield] TextField1
FIELD[displayfield] ctl162
FIELD[textfield] textfield-1065
FIELD[textfield] textfield-1068
FIELD[textfield] textfield-1071
BTN Nuevo
BTN Editar
BTN Eliminar
BTN Ver usuarios
BTN Modulos indirectos
BTN Actualizar Lista.
GRID Roles del sistema: Usuario | Programa Agenda | Estado
FIELD[combobox] ComboTipoModulo {INICIO, HISTORIA CLINICA, PAGINA WEB, ALMACEN}
BTN Actualizar arbol
TREE Configuración de los modulos
BTN Subir orden
BTN Bajar orden
BTN Actualiza la lista de los permisos
BTN Guardar
GRID Asignar permisos al modulo: Descripción | Permiso
TOOLTIP Editar modulos
TOOLTIP Habilitar modulo permisos

## CONFIGURACION GENERAL > USUARIOS ACTIVOS EN SUROS (/SUROS/Vistas/Privado/SignalR/UsuariosActivos.aspx)
TITLE Comunicacion
FIELD[textareafield] Mensaje
BTN Enviar Mensaje
BTN Cancelar
WINDOW Envio Masivo
BTN Preparar Publicación
BTN Enviar mensaje masivo
GRID : Id usuario | Nombre usuario | Conectado desde | Ip | Rol | Especialidad | Fecha y Hora conexion | Id Signal
BTN Cerrar sesión
BTN Iniciar Chat

## CONFIGURACION GENERAL > CONFIGURACIÓN LABORATORIO (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Laboratorios/LaboratorioClinico.aspx)
TITLE Estudio de laboratorios
FIELD[displayfield] ctl17
FIELD[textfield] textfield-1014
FIELD[textfield] textfield-1017
FIELD[textfield] textfield-1020
GRID : Id | Descripción | Estado
FIELD[textfield] Registrar unid/med
BTN Guardar nueva unidad de medida
BTN Eliminar unidad de medida
FIELD[combobox] Estado {TODOS, ACTIVO, INACTIVO}
BTN Actualizar
BTN Cerrar
WINDOW Unidad medida
FIELD[textfield] Código
FIELD[textfield] Descripción
FIELD[textfield] Abreviatura
FIELD[combobox] Unid/Med
FIELD[textfield] Formula
FIELD[displayfield] TextTD2
FIELD[textfield] Valor minimo
FIELD[textfield] Valor maximo
FIELD[numberfield] Alarma val. minimo
FIELD[numberfield] Alarma val. maximo
FIELD[textareafield] Valor de referencia
BTN Gestionar unid/med
BTN Guardar
BTN Cancelar
FIELD[displayfield] ctl99
FIELD[textfield] textfield-1041
FIELD[textfield] textfield-1044
FIELD[textfield] textfield-1047
FIELD[textfield] textfield-1050
FIELD[textfield] textfield-1053
FIELD[textfield] textfield-1056
FIELD[textfield] textfield-1059
FIELD[textfield] textfield-1062
FIELD[textfield] textfield-1065
BTN Actualizar lista
GRID : Id | Descripción | Abreviatura | Unid/Med | Valor min. | Valor Max. | Alarma max. | Alarma min. | Estado
BTN Eliminar
WINDOW Gestionar análitos
GRID : Código | Descripción
BTN Aceptar
WINDOW Coincidencias encontradas
FIELD[triggerfield] Código Cups
FIELD[triggerfield] Descripción
FIELD[combobox] Estado {ACTIVO, INACTIVO}
FIELD[combobox] Sección {BANCO DE SANGRE, CITOPATOLOGIA, COAGULACION, COPROANALISIS, HEMATOLOGIA , INMUNOLOGIA, ESPECIAL, INMUNOLOGIA I, INMUNOLOGIA II, INMUNOLOGIA III, INMUNOLOGIA IV, INMUNOLOGIA V, LIQUIDOS, MICROBIOLOGIA , QUIMICA, HORMONAS, MICROSCOPIA}
FIELD[combobox] Técnica {AGLUTINACION, COAGULOMETRICO, COLORIMETRICO, COLORIMETRICO DE PUNTO FINAL, COLORIMETRICO ENZIMATICO, ELECTRODO DE ION SELECTIVO, ELISA, ENZIMATICO, INMUNOENSAYO DE CROMATOGRAFIA DE FLUJO, INMUNOENSAYO ENZIMATICO EIA, INMUNOFLUORESCENCIA, INMUNOTURBIDIMETRIA, LECTURA MICROSCOPICA, MICROELISA, NO DEFINIDA, QUIMICA SECA, QUIMIOLUMINISCENCIA, TURBIDIMETRIA}
FIELD[combobox] Tipo muestra {NO DEFINIDA, ESPUTO, MATERIA FECAL, ORINA, ORINA 24 HORAS + SUERO, SECRECIONES VARIAS, PLASMA, SUERO, SANGRE TOTAL}
FIELD[combobox] Nivel {I NIVEL, II NIVEL, III NIVEL, IV NIVEL, V NIVEL}
FIELD[textfield] Dias almacen
FIELD[combobox] Tipo almacen {NO APLICA, CONGELACION, TEMPERATURA, AMBIENTE, REFRIGERADA}
FIELD[combobox] Sexo {AMBOS, HOMBRE, MUJER}
FIELD[textfield] Prefijo cod. barras
FIELD[combobox] Confidencial {SI, NO}
FIELD[numberfield] Valor min
FIELD[numberfield] Valor max
FIELD[numberfield] Alerta max
FIELD[numberfield] Alerta min
FIELD[displayfield] TextTD1
FIELD[combobox] Agregar análito
BTN Adicionar analito
BTN Unidad de medida
BTN Analitos
BTN Gestionar
GRID : LEXAID | LAANID | Pos | Descripción | Abreviatura | Unid/Med | Valor min. | Valor Max. | Alarma max. | Alarma min.
BTN Subir item
BTN Bajar item
BTN Aceptar y salir
BTN Salir
WINDOW Agregar estudio de laboratorio
FIELD[textareafield] TextLista
WINDOW Registrar opciones de respuesta
FIELD[displayfield] ctl321
FIELD[textfield] textfield-1122
FIELD[textfield] textfield-1125
FIELD[textfield] textfield-1128
FIELD[textfield] textfield-1131
FIELD[textfield] textfield-1134
FIELD[textfield] textfield-1137
FIELD[textfield] textfield-1140
FIELD[textfield] textfield-1143
FIELD[textfield] textfield-1146
FIELD[textfield] textfield-1149
FIELD[textfield] textfield-1152
FIELD[textfield] textfield-1155
FIELD[textfield] textfield-1158
FIELD[textfield] textfield-1161
FIELD[textfield] textfield-1164
FIELD[textfield] textfield-1167
BTN Nuevo
BTN Modificar
GRID : Procedimiento | Abreviatura | Unid/Med | Seccion | Técnica | Tipo muestra | Nivel complejidad | Dias almacenamiento | Almacenamiento | Sexo | Pref. codigo barra | Valor min | Valor max | Alarma min | Alarma max | Estado

## CONFIGURACION GENERAL > CREDENCIALES SISPRO (/SUROS/Vistas/Privado/WebSispro/CredencialesWebSispro.aspx)
NO_EXT 

## CONFIGURACION GENERAL > EMPRESAS (/SUROS/Vistas/Privado/Empresa/Empresa.aspx)
TITLE 

## CONFIGURACION GENERAL > SUBPLANES SERVICIOS (/SUROSFacturacion/Vistas/Privado/SubPlanes/SubPlanesServicios.aspx)
TITLE SubPlanes Servicios
FIELD[triggerfield] Servicio
BTN Servicios
GRID Servicios: Servicio
GRID SubPlanes asignados: Id Unico | SubPlan
BTN Elimina SubPlan dal servicio
BTN Agregar SubPlan al servicio
FIELD[displayfield] ctl48
FIELD[textfield] textfield-1026
BTN Subplanes
GRID SubPlanes disponibles: SubPlan
BTN Aceptar
BTN Cancelar
FIELD[displayfield] displayfield-1039
FIELD[displayfield] displayfield-1040
FIELD[triggerfield] SUSE_ID
FIELD[displayfield] SUPL_NOMBRE

## HERRAMIENTAS > UNIFICACION HISTORIA CLINICA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/UnificarHistoriaClinica.aspx)
TITLE Unificacion Historia Clinica
GRID : DOCUMENTO | NOMBRE PACIENTE
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
GRID : Descripción
WINDOW Transferir información
FIELD[textfield] Celula\Nombre
FIELD[textfield] TextPaciente1
BTN Eliminar paciente
BTN Transferir información
BTN Opciones del paciente.
GRID Paciente 1: ID | FECHA ENTRADA | FECHA SALIDA | PROFESIONAL QUIEN REGISTRA | ESTADO
FIELD[textfield] TextPaciente2
GRID Paciente 2: ID | FECHA ENTRADA | FECHA SALIDA | PROFESIONAL QUIEN REGISTRA | ESTADO

## HERRAMIENTAS > DISEÑADOR DE CONSENTIMIENTOS (/SUROS/Vistas/Privado/Formatos/Formatos.aspx)
TITLE Formatos
FIELD[textfield] Procedimiento
BTN Buscar procedimientos medicos!
GRID : CODIGO | DESCRIPCIÓN
BTN Salir
WINDOW Procedimientos
GRID : CÓDIGO | DESCRIPCIÓN
BTN Aceptar
WINDOW Coincidencias encontradas
FIELD[textfield] Nombre
FIELD[textareafield] Descripción
BTN Guardar y Salir
BTN Guardar
WINDOW Tipo de Formato
BTN Switch to source editing mode.
FIELD[htmleditor] AreaDescripcion
BTN Cancelar
WINDOW HTML
BTN Insertar comodin con el nombre del formato para agregar a la cabecera!
BTN Insertar comodin con el codigo de esta version para agregar al formato!
BTN Insertar comodin con la version del formato!
BTN Insertar comodin con el logo de la empresa!
BTN Insertar tabla Cargue una tabla de diseño para el uso en este formato
BTN Ver Ayuda de Comodines
BTN Cerrar
WINDOW Ayuda - Tipos de Formatos
WINDOW Ayuda - Edición de Versiones
FIELD[textfield] Filtrar por nombre...
BTN Nueva
BTN First Page
BTN Previous Page
BTN Next Page
BTN Last Page
BTN Refresh
GRID Tipos de Formatos: Titulo
FIELD[textfield] Titulo
FIELD[textfield] Codigo
FIELD[textfield] Version
BTN Buscar
BTN Nuevo
BTN Refrescar
GRID Versiones de Formatos: Titulo | Código | Versión
BTN Nueva versión para este formato
BTN Copiar esta versión
BTN Eliminar esta versión del formato
FIELD[textfield] Versión
FIELD[combobox] Tipo de Consentimiento {CONSENTIMIENTOS INFORMADOS}
BTN Align text to the left.
BTN Center text in the editor.
BTN Align text to the right.
FIELD[htmleditor] Cabecera
BTN Para ingresar en modo HTML, active este icono. Antes de guardar por favor desactive.
FIELD[htmleditor] Contenido Principal
FIELD[htmleditor] Pie de Página
BTN Previsualizar en PDF
FORM Nueva Versión de Formato
BTN Ayuda
BTN Ayuda sobre edición y comodines
BTN Abrir esta ventana en un panel HTML externo!
FIELD[combo] Cabecera
BTN Insertar comodin con nombre de persona para agregar al formato!
BTN Insertar comodin con documento de identificación de la persona!
BTN Insertar comodin con el tipo de documento del paciente!
BTN Insertar comodin con firma de la persona!
BTN Insertar comodin con huella digital de la persona!
BTN Insertar comodin con medico en sesión!
BTN Insertar comodin con firma del medico en sesión!
BTN Insertar comodin con especialidad del medico!
BTN Insertar comodin con nombre del representante legal o familiar!
BTN Insertar comodin con identificación y parentesco del paciente!
BTN Insertar comodin con fecha actual!
BTN Insertar comodin con nombre de la empresa!
BTN Insertar comodin con nombre del gerente de la empresa!
BTN Insertar comodin con contenido!
BTN Insertar comodin con el codigo y nombre del procedimiento a realizar!
BTN Insertar comodin con el codigo y nombre del procedimiento realizado!
BTN Justificar a la izquierda
BTN Justificar al centro
BTN Justificar a la derecha
BTN Justificar completo
FIELD[combo] Pie de Pagina
WINDOW Imprimir formatos
FIELD[textfield] NOTI_ID
FIELD[combobox] Categoria
FIELD[datefield] Fecha Publicacion
FIELD[textfield] Palabras Claves
FIELD[combobox] Estado
FIELD[combobox] Periodista
FIELD[textfield] Url
FIELD[textfield] Orden
FIELD[filefield] Imagen Principal
BTN Negrilla
BTN Make the selected text italic.
BTN Underline the selected text.
BTN Change the color of the selected text.
BTN Color de Fondo
BTN Make the selected text a hyperlink.
BTN Start a numbered list.
BTN Start a bulleted list.
FIELD[htmleditor] Resumen
FIELD[textfield] NOTI_IMAGENN
BTN Imprimir
BTN Eliminar
BTN salir
WINDOW Formatos
BTN BR
BTN Destacado
BTN Nota
BTN Alerta
FIELD[filefield] Imagen
BTN Subir y Guardar Imagen
FIELD[filefield] Seleccione un documento
BTN Subir y Guardar Documento
FIELD[textfield] Buscar Documento
BTN Entendido
WINDOW Ayuda - Uso de Comodines y Edición
BTN Editar este tipo
BTN Eliminar este tipo

## FACTURACIÓN > ADMON FACTURACION > BUSCAR UNA FACTURA (/SUROSFacturacion/Vistas/Privado/Facturacion/BuscarFactura.aspx)
TITLE 
FIELD[combobox] Consultar por {POR CÉDULA, POR NÚMERO DE FACTURA, POR NÚMERO PREFACTURA, POR IMPORTACIÓN DE ARCHIVO EXCEL}
FIELD[datefield] Fecha inicio
FIELD[datefield] Fecha fin
FIELD[numberfield] Numero documento
FIELD[textfield] N° Factura
BTN Consultar
FIELD[filefield] BTN_IMPORTAR
FIELD[textfield] textfield-1014
FIELD[textfield] textfield-1017
FIELD[textfield] textfield-1020
FIELD[textfield] textfield-1023
FIELD[textfield] textfield-1026
FIELD[textfield] textfield-1029
FIELD[textfield] textfield-1032
BTN Exportar factura en formato PDF
GRID Facturas: N° FACTURA | ESTADO | FECHA INGRESO | FECHA SALIDA | CONTRATO | REGISTRADO POR | FECHA REGISTRO
GRID : Descripción | Carta
BTN Aceptar
WINDOW Selecione Tipo Imprecion

## FACTURACIÓN > ADMON FACTURACION > GENERADOR RIPS (/SUROSFacturacion/Vistas/Privado/Rips/GeneradorRips.aspx)
TITLE Rips
FIELD[netmulticombo] Prestador Del Servicio {TODOS}
FIELD[combobox] Empresa {PARTICULAR (OTRO), ASMET SALUD EPS SAS (SUBSIDIADO), ASMET SALUD EPS SAS (CONTRIBUTIVO)}
FIELD[combobox] Contrato:
FIELD[netmulticombo] SubPlan: {TODOS}
FIELD[combobox] Clasificacion: {TODOS, POS, NO POS}
FIELD[datefield] Fecha inicial
FIELD[datefield] Fecha Final
FIELD[combobox] GENERAR CODIGOS COMO: {CUPS, SOAT}
FIELD[filefield] BTN_IMPORTAR
BTN Consultar
BTN Aceptar
WINDOW Generar RIPS

## FACTURACIÓN > ADMON FACTURACION > LISTADO FACTURAS (/SUROSFacturacion/Vistas/Privado/Reportes/ReporteFacturasContrato.aspx)
TITLE Reporte facturas
FIELD[combobox] Tipo {UN SOLO DOCUMENTO PDF, DOCUMENTO ZIP POR PACIENTE, DOCUMENTO ZIP POR FACTURA}
FIELD[checkboxfield] CheckTodoCarta
BTN Aceptar
GRID Ítems del Archivo: Descripción | Adjuntar
WINDOW Archivos A Imprimir
GRID Facturas enviadas a la DIAN: Número Factura
GRID Facturas fallidas: Número Factura
WINDOW Reporte Envio Factura Electronica
GRID : Descripción | Carta
WINDOW Selecione Tipo Imprecion
FIELD[combobox] Resolución
WINDOW Seleccione resolución
FIELD[netmulticombo] ComboPrestadorServicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] ComboEstadoContrato {ACTIVOS, INACTIVOS, TODOS}
FIELD[combobox] ComboContrato
FIELD[netmulticombo] ComboSubplan
FIELD[datefield] TextFechaInicio
FIELD[datefield] TextFechaFin
BTN Consultar
FIELD[combobox] drpTipoExporte {Exportar Listado a Excel, Exportar Facturas a Pdf}
FIELD[combobox] TipoProgramaEspecial {TODAS, NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}
BTN Exportar
BTN Obtener Xml Electronico
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Reporte Facturas: Validada Rips | Prefijo | Número Factura | Tipo Doc. | Documento | Nombre | Empresa | Tipo Afiliación | Prestador de Servicio | Contrato | Fecha Facturado | Fecha ingreso | Fecha Egreso | Copago | Couta Moderadora | Pagos Compartidosen planes voluntarios de salud | Anticipo | No Aplica | Valor Total | Subplan | Realizado por | Cod. Diag | Descripcion | Medico
BTN Facturar Electronicamente
BTN Imprimir Factura
BTN Convertir A Factura
BTN Editar Documento
BTN Enviar a la Dian
BTN Validar Rips
BTN Generar Nota Credito
BTN Editar Documento Res. 1557
BTN Enviar a NEOSAGE
BTN Validar Rips sin Factura
FIELD[textfield] TextFainIdSoloProcedimientoJson
FIELD[textfield] TextProcIdSoloProcedimientoJson
FIELD[textfield] TextPaciIdSoloProcedimientoJson
FIELD[textfield] TextFainIdSoloProcedimientoN
FIELD[textfield] TextProcIdSoloProcedimientoN
FIELD[textfield] TextPaciIdSoloProcedimientoN
BTN Cancelar
BTN Enviar
FIELD[combobox] Credenciales WebSisPro {<valor omitido>}
BTN VALIDAR
WINDOW Validar Rips

## FACTURACIÓN > GENERAR FACTURAS > FACTURA GLOBAL (/SUROSFacturacion/Vistas/Privado/Facturacion/FacturaGeneral.aspx)
TITLE 
BTN First Page
BTN Previous Page
BTN Next Page
BTN Last Page
BTN Refresh
GRID : Opciones
WINDOW Documentos Factura Global
BTN Sort Ascending
BTN Sort Descending
BTN Columns
BTN Group by this field
GRID : EMPRESA | CONTRATO | TIPO CONTRATO
WINDOW Listado de empresas
BTN Aceptar
BTN Cancelar
FIELD[textfield] FAGO_ID_TF
WINDOW Selecione Tipo Imprecion
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
FIELD[textfield] Código
FIELD[textareafield] Concepto
FIELD[numberfield] Cantidad
FIELD[numberfield] Valor unitario
FIELD[textfield] Valor total
FIELD[textareafield] Observación
BTN Añadir
WINDOW Nuevo consolidado
FIELD[textfield] Filtrar
GRID : Código | Nombre | Tipo
BTN Seleccionar
WINDOW Seleccionar producto
GRID : EMPRESA | No CONTRATO | TIPO CONTRATO
FIELD[combobox] Forma de pago {Efectivo}
FIELD[combobox] Concepto pago {COPAGO, CUOTA MODERADORA, COPAGO REGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS DE SALUD, ANTICIPO, NO APLICA}
WINDOW Nuevo recibo de pago
FIELD[textfield] Buscar
GRID Datos del contrato: NIT | EMPRESA | CONTRATO | TIPO CONTRATO | REGIMEN | Opciones
FIELDSET Datos de contacto
FIELD[datefield] Fecha inicial de facturaciòn
FIELD[datefield] Fecha final de facturaciòn
FIELDSET Periodo de facturación
FIELD[combobox] FORMA DE PAGO {CONTADO, CREDITO}
FIELD[combobox] MEDIO DE PAGO {EFECTIVO, TARJETA DEBITO, TARJETA CREDITO, TRANSFERENCIA ELECTRONICA}
BTN Agregar item
GRID Consolidado: No | CODIGO | CONCEPTO | OBSERVACION | CANTIDAD | V/U | V/T
BTN Agregar recibo de pago
GRID Recibo de pago: No | FOMA DE PAGO | CONCEPTO PAGO | CANTIDAD | V/U | OBSERVACIÒN | V/T
FIELD[textfield] Total factura
FIELD[combobox] Pres. Servicio {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Resolución
FIELD[combobox] Contrato {RIS-016-23-PGP, RIS-014-26-PGPC, RIS-011-26-PGPS, RIS-005-26-PGPS, RIS-006-26-PGPC, RIS-012-26-PGPC, NAC-236-C20, PART-012020, NAC-233-S20, 73-2019-028, APREHSI-012022, RIS-013-26-PGPS}
FIELD[combobox] Empresa
FIELD[datefield] Fecha de facturaciòn
BTN Cargar
FORM Facturacion global
FIELD[datefield] Selecciona una fecha
BTN Consultar
BTN Imprimir
BTN Facturar Electronicamente
GRID : ID FACTURA | FACTURA NUMERO | FECHA DE FACTURA | FECHA INICIO PERIODO FACTURADO | FECHA FIN PERIODO FACTURADO
FIELD[filefield] Archivo
WINDOW Cargar archivo CUV (TXT o JSON)
GRID Facturas enviadas a la DIAN: Número Factura
GRID Facturas fallidas: Número Factura
WINDOW Reporte Envio Factura Electronica

## FACTURACIÓN > GENERAR FACTURAS > FACTURADOR AUTOMATICO (/SUROSFacturacion/Vistas/Privado/Facturacion/ListaIngresos.aspx)
TITLE 
FIELD[datefield] Fecha a facturar:
FIELD[datefield] DateFechaFin
FIELD[triggerfield] TriggerField1
TREE TreeMenuInformes
FIELD[datefield] Rango de fechas:
FIELD[datefield] FechaFinIngresoSinFacturar
GRID Ítems de impresión: Descripción | Check
BTN Exportar
PANEL Exportar pacientes sin facturar
FORM Listado de servicios
TABPANEL Facturación Surós

## FACTURACIÓN > GENERAR FACTURAS > FACTURADOR MANUAL V2 (/SUROSFacturacion/Vistas/Privado/Facturacion/FacturadorV2/FacutradorV2.aspx)
TITLE 
FIELD[checkboxfield] Facturar sin un ingreso previo
FIELD[checkboxfield] Facturación de larga instancia
FIELD[triggerfield] Buscar
FIELD[datefield] Fecha inicial
FIELD[datefield] Fecha final
GRID :
PANEL Ingresos Sin facturar
PANEL Ingresos facturados
BTN Aceptar
WINDOW Lista de procedimientos para facturar
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
GRID : Código | Descripción
BTN Salir
WINDOW Coincidencias encontradas en el CIE10
BTN Enviar
BTN Cancelar
FIELD[textfield] TextField1
FIELD[textfield] TextField2
FIELD[textfield] TextField3
GRID : Descripción | Carta
WINDOW Selecione Tipo Imprecion
FIELD[textfield] TextField4
FIELD[textfield] TextField5
FIELD[textfield] TextField6
FIELD[combobox] Resolución
FIELD[textfield] TextFainIdSoloProcedimiento
FIELD[textfield] TextProcIdSoloProcedimiento
FIELD[textfield] TextPaciIdSoloProcedimiento
FIELD[textfield] TextFainIdSoloProcedimientoJson
FIELD[textfield] TextProcIdSoloProcedimientoJson
FIELD[textfield] TextPaciIdSoloProcedimientoJson
FIELD[combobox] Credenciales WebSisPro {<valor omitido>}
BTN VALIDAR
WINDOW DESEA FACTURAR ELECTRONICAMENTE?
FIELD[textfield] TextFainIdSetPruebasJson
FIELD[textfield] TextProcIdSetPruebasJson
FIELD[textfield] TextPaciIdSetPruebasJson
BTN PRE VALIDAR
FIELD[textfield] TextFainIdSoloProcedimientoN
FIELD[textfield] TextProcIdSoloProcedimientoN
FIELD[textfield] TextPaciIdSoloProcedimientoN
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
GRID : Iss | Valor Iss | Soat | Valor Soat
WINDOW Seleccione el homologo con el que desea facturar
GRID : Código | Descripción | Cantidad
WINDOW Procedimientos que no se pueden facturar
FIELD[textfield] Buscar procedimiento
BTN Buscar Procedimiento ingresado
FIELD[textfield] Autorizacion
BTN Traer número autorización principal
BTN Replicar info a todos los procedimientos
FIELD[textfield] MIPRES
FIELD[combobox] Persona Ejecuta
FIELD[combobox] Unidad de Funcional {AMBULATORIO, URGENCIAS/OBSERVACION, HOSPITALIZACION, CIRUJIA, UCI}
FIELD[combobox] Modalidad de Atencion {INTRAMURAL, EXTRAMURAL UNIDAD MÓVIL, EXTRAMURAL DOMICILIARIA, EXTRAMURAL JORNADA DE SALUD, TELEMEDICINA INTERACTIVA, TELEMEDICINA NO INTERACTIVA, TELEMEDICINA TELEXPERTICIA, TELEMEDICINA TELEMONITOREO}
FIELD[combobox] Grupo de Servicios {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}
FIELD[combobox] Servicios
FIELD[combobox] Finalidad Procedimietno
FIELD[datefield] Fecha Ejecucion
FIELD[timefield] Hora Ejecucion
FIELD[numberfield] Cantidad
FIELD[numberfield] Valor/U
FIELD[numberfield] Valor Total
FIELD[numberfield] Comisión
FIELD[numberfield] Descuento
FIELD[textareafield] Observacion
BTN Agregar
BTN Agregar y Cerrar
WINDOW Panel asistencial
FIELD[numberfield] ctl403
FIELD[numberfield] ctl406
FIELD[numberfield] ctl409
FIELD[textfield] Código CUPS - Nombre o código:
GRID : Código | Código | Descripción | Cantidad | Valor Unitario | Valor total
WINDOW PAQUETE PARTOS
GRID : Número Factura | Principal | Fecha Factura | Fecha Ingreso | Fecha Egreso | Valor Total Factura
FIELD[datefield] Fecha Inicio
FIELD[datefield] Fecha Fin
BTN Buscar facturas para relacionar al paquete
BTN Confirmar
WINDOW FACTURAS A RELACIONAR
WINDOW Adjuntar recibo de pago
FIELD[triggerfield] Búsqueda
FIELD[textfield] Num. Mipres
FIELD[textfield] Cum
FIELD[textfield] Medicamento
FIELD[combobox] Profesional que formula
FIELD[datefield] Fecha Aplicacion:
FIELD[timefield] Hora de Aplicacion:
FIELD[numberfield] Dias de Tratamiento
FIELD[numberfield] Valor real
BTN Agregar y cerrar
WINDOW Panel Medicamentos
FIELD[textfield] Procedimiento
WINDOW Panel Procedimientos Quirurgicos
BTN Copago relacionado
BTN Nuevo copago
WINDOW Opciones
FIELD[textfield] PACIENTE:
GRID : ID | Información de la cita | Información del copago
BTN ACEPTAR
BTN CANCELAR
WINDOW RELACIONAR COPAGOS
GRID : Código | Descripción | Forma Farmaceutica | Volumen|Peso Presentación | Concentración | Existencias
WINDOW Coincidencia de medicamentos
FIELD[textfield] Autorización
FIELD[textfield] Num Mipres
FIELD[textfield] Codigo
FIELD[textfield] Insumo
WINDOW Panel Insumos
GRID : Código | Nombre | Presentación | Existencias
WINDOW Coincidencia de Insumos
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : ID | Fecha Registro | Profesional quien registra | Prev
WINDOW Registros de actividades
FIELD[numberfield] Autorizacion
FIELD[combobox] Via de ingreso: {DEMANDA ESPONTANEA, DERIVADO DE CONSULTA EXTERNA, DERIVADO DE URGENCIAS, DERIVADO DE HOSPITALZACION, DERIVADO DE SALA DE CIRUGIA, DERIVADO DE SALA DE PARTOS, RECIEN NACIDO EN LA INSTITUCION, RECIEN NACIDO EN OTRA INSTITUCION, DERIVADO O REFERIDO DE HOSPITALIZACION DOMICILIARIA, DERIVADO DE ATENCION DOMICILIARIA, DERIVADO DE TELEMEDICINA, DERIVADO DE JORNADA DE SALUD, REFERIDO DE OTRA INSTITUCION, CONTRAREFERIDO DE OTRA INSTITUCION}
FIELD[datefield] Fecha Salida
FIELD[timefield] Hora Salida
WINDOW Panel Estancias
FIELD[textfield] ctl999
FIELD[textfield] ctl1030
FIELD[numberfield] ctl1150
FIELD[numberfield] ctl1153
FIELD[numberfield] ctl1156
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
FIELD[textfield] No. ingreso:
FIELD[textfield] Identificación
FIELD[textfield] Nombre Completo:
FIELD[textfield] Nombre1:
FIELD[textfield] Fecha de nacimiento
FIELD[textfield] Género
FIELD[textfield] Municipio residencia:
FIELD[textfield] Zona residencial:
FIELD[combobox] ComboEmpresa {PIJAOS SALUD E.P.S.I - SUBSIDIADO, PARTICULAR - OTRO, ATENCION PREHOSPITALARIA Y SEGURIDAD INDUSTRIAL-APREHSI LTDA - OTRO, ASMET SALUD EPS SAS - SUBSIDIADO, ASMET SALUD EPS SAS - CONTRIBUTIVO}
FIELD[combobox] No. Contrato:
FIELD[combobox] Tipo programa especial: {NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}
BTN Datos de ingreso
BTN BUSCAR ULTIMA FACTURA
BTN Consolidado
BTN Asistencial
BTN Recibo de pago
BTN Medicamentos
BTN Insumos
BTN Partos - Paquete
BTN Paquete, Canasta o Grupo de Atenciones Integrales
BTN Cirugia
BTN Estancias
BTN Furips
NETMENUPANEL Facturación
BTN Control de caja
BTN Egresos
NETMENUPANEL Tesorería
FIELD[combobox] Prestador del servicio: {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[combobox] Grupo SubPlan:
FIELD[combobox] Médico:
FIELD[combobox] Especialidad
FIELD[combobox] Subplan:
PANEL Información Prestador del servicio
FIELD[textfield] No autorización:
FIELD[textfield] No aprobación:
FIELD[datefield] Fecha facturación:
FIELD[textfield] Número de autorización para todos los items de la factura:
FIELD[combobox] Cobertura/Pagador: {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[combobox] Forma de Pago {CREDITO, CONTADO}
PANEL Información Factura
FIELD[textfield] Numero de poliza (Solo Para Seguros o Polizas)
FIELD[textfield] Numero de Siras
PANEL Información Soat - Si aplica para este ingreso!
FIELD[combobox] Es gestante {SI, NO}
FIELD[combobox] Trabajo de parto {NO, TRABAJO DE PARTO - NACIDO EN LA INSTITUCIÓN , TRABAJO DE PARTO - REMITIDO}
PANEL Datos Gestantes
FIELD[combobox] Tipo identificación: {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}
FIELD[textfield] Número de identificación:
FIELD[combobox] Sexo: {MASCULINO (M), FEMENINO (F)}
FIELD[numberfield] Edad gestacional
FIELD[textfield] # Controles
FIELD[datefield] Fecha de nacimien
FIELD[timefield] Hora nacimiento:
FIELD[numberfield] Peso:
FIELD[textfield] IDCIE10DiagnosticoPrincipal
FIELD[triggerfield] Diagnostico pricipal:
FIELD[combobox] Est. salida {PACIENTE MUERTO, PACIENTE CON DESTINO A SU DOMICILIO, PACIENTE DERIVADO A OTRO SERVICIO, REFERIDO A OTRA INSTITUCION, CONTRAREFERIDO A OTRA INSTITUCION, DERIVADO O REFERIDO A HOSPITALIZACION DOMICILIRIA, DERIVADO A SERVICIO SOCIAL, PACIENTE CONTINUA EN EL SERVICIO (CORTE FACTURACION)}
FIELD[datefield] Fecha egreso:
FIELD[timefield] Hora egreso:
FIELD[textfield] IDCIE10MurteNacimiento
FIELD[triggerfield] Causa basica de muerte CIE10:
PANEL Datos Recien Nacido
FIELD[combobox] Categorias {JORNADA DE SALUD, VISITA DOMICILIARIA, UNIDAD MOVIL}
FIELD[combobox] Equipo de atención
FIELD[combobox] Zona Atención
PANEL Información de APS
FIELD[datefield] Fecha ingreso:
FIELD[timefield] Hora de ingreso:
FIELD[combobox] Causa externa: {ACCIDENTE DE TRABAJO, LESION POR AGRESION, LESION AUTO INFLIGIDA, ENFERMEDAD GENERAL, SOSPECHA DE VIOLENCIA SEXUAL, OTRO TIPO DE ACCIDENTE, ACCIDENTE EN EL HOGAR, ACCIDENTE DE TRÁNSITO DE ORIGEN COMÚN, ENFERMEDAD LABORAL, INTERVENCIÓN COLECTIVA, ATENCIÓN DE POBLACIÓN MATERNO PERINATAL, RIESGO AMBIENTAL, OTROS EVENTOS CATASTRÓFICOS, ACCIDENTE DE MINA ANTIPERSONAL – MAP, ACCIDENTE DE ARTEFACTO EXPLOSIVO IMPROVISADO – AEI, ACCIDENTE DE MUNICIÓN SIN EXPLOTAR- MUSE, OTRA VÍCTIMA DE CONFLICTO ARMADO COLOMBIANO, PROMOCIÓN Y MANTENIMIENTO DE LA SALUD – INTERVENCIONES INDIVIDUALES, ACCIDENTE DE TRÁNSITO DE ORIGEN LABORAL, EVENTO CATASTRÓFICO DE ORIGEN NATURAL, SOSPECHA DE VIOLENCIA FÍSICA, SOSPECHA DE VIOLENCIA PSICOLÓGICA, SOSPECHA DE NEGLIGENCIA Y ABANDONO, IVE RELACIONADO CON PELIGRO A LA SALUD O VIDA DE LA MUJER, IVE POR MALFORMACIÓN CONGÉNITA INCOMPATIBLE CON LA VIDA, IVE POR VIOLENCIA SEXUAL, INCESTO O POR INSEMINACIÓN ARTIFICIAL O TRANSFERENCIA DE OVULO FECUNDADO NO CONSENTIDA, EVENTO ADVERSO EN SALUD, ACCIDENTE EN EL ENTORNO EDUCATIVO}
PANEL Datos de ingreso
FIELD[datefield] Fecha Egreso:
FIELD[timefield] Hora de egreso:
FIELD[combobox] Incapacidad {SI, NO}
FIELD[combobox] Destino: {SALIDA, MORGUE, SALIDA POR REFERENCIA Y CONTRAREFERENCIA, RETIRO VOLUNTARIO, FUGA, EN TRATAMIENTO(SALIDA), INICIAR TRATAMIENTO, TRATAMIENTO TERAPIA FÍSICA, CANCELAR CIRUGIA, SALA DE ADMISIÓN}
PANEL Datos de Egreso
FIELD[textfield] Buscar Diagnostico
BTN Buscar registros del CIE10
FIELD[combobox] Tipo Diagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
PANEL Diagnostico de Ingreso
FIELD[combobox] Buscar Diagnostico {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
BTN Importar Diagnostico de ingreso
PANEL Diagnostico de Egreso
GRID : Código | Descripción | Prioridad
BTN Subir orden
BTN Bajar orden
FIELD[textareafield] OBSERVACION
BTN Eliminar Registros seleccionados
BTN Agregar Numero Autorizacion para todo
BTN Ver Actividades
GRID Consolidado: ID | Cum/Cód | Concepto | Finalidad | Fecha Aplicacion | Hora Aplicacion | Unidad Funcional | Num. Autorización | Cod Mipres | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
GRID Cirugia: ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
GRID Recibo de pago: Caja | Concepto | Forma de pago | Cantidad | Observación | Valor | Total a pagar | Total pago | Saldo
FIELD[textfield] Valor Total:
GRID Facturas Agregadas: Número Factura | Fecha Factura | Fecha Ingreso | Fecha Egreso | Valor Total Factura
FIELD[combobox] Cirujano
FIELD[combobox] Anestesiologo
FIELD[combobox] Ayudante:
FIELD[combobox] Tipo cirugia: {LIMPIA, LIMPIA CONTAMINADA, CONTAMINADA, SUCIA}
FIELD[combobox] Tipo anestesia: {LOCAL, REGIONAL, BLOQUEO, GENERAL}
FIELD[datefield] Fecha Cirugia:
FIELD[combobox] Vía de acceso: {BILATERALES, UNICA VIA IGUAL CIRUJANO, DISTINTA VIA IGUAL CIRUJANO, DIFERENTES ESPECIALISTAS POR IGUAL O DISTINTA VIA}
FIELD[textfield] Código/Nombre CIE10
FIELD[combobox] ComboTipoDiagnosticoCirugia {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
FIELDSET Ejecución de procedimientos
FIELD[textfield] HidenPrquIdPer
FIELD[textfield] HiddenPrquCodigoPer
FIELD[textfield] HiddenPrquDescripcionPer
FIELD[textfield] TextCantidadPer
FIELD[textfield] TextValorPer
FIELD[textfield] TextDescuentoPer
FIELD[textfield] TextValorTotalPer
FIELD[textfield] TextValorOriginaPerl
FIELD[textfield] HidenIncrementoPer
FIELD[textfield] HidenServicioPer
FIELD[textfield] Nombre usuario
FIELD[textfield] Contraseña
BTN Continuar
FORM El procedimiento ya se encuentra en la lista, Para agregar ingrese credenciales
WINDOW Ingresar credenciales
BTN Guardar
PANEL Facturación
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
PANEL INFORMACIÓN DEL PRESTADOR
FIELD[combobox] CONDICIÓN DEL ACCIDENTADO {CONDUCTOR, PEATON, OCUPANTE, CICLISTA}
PANEL DATOS DE LA VICTIMA DEL EVENTO CATASTRÓFICO O ACCIDENTE DE TRANSITO
FIELD[combobox] NATURALEZA DEL EVENTO {TRANSITO, NATURALES, TERRORISTAS}
FIELD[combobox] TIPO DE EVENTO
FIELD[datefield] FECHAEVENTOACCIDENTE
FIELD[timefield] HORAEVENTO
FIELD[textfield] DIRECCIONACCIDENTE
FIELD[combobox] DEPARTAMENTO
FIELD[combobox] MUNICIPIO
FIELD[radiofield] RURAL
FIELD[radiofield] URBANO
FIELD[radiogroup] ZONA
FIELD[textareafield] CARACTERISTICASACCIDENTE
PANEL DATOS DEL SITIO DONDE OCURRIÓ EL EVENTO CATASTRÓFICO O EL ACCIDENTE DE TRANSITO
FIELD[combobox] ESTADO DE ASEGURAMIENTO {ASEGURADO, NO ASEGURADO, VEHICULO FANTASMA, POLIZA FALSA, VEHICULO EN FUGA}
FIELD[textfield] MARCAVEHICULO
FIELD[textfield] PLACAVEHICULO
FIELD[combobox] TIPO SERVICIO {PARTICULAR, PUBLICO, OFICIAL, VEHICULO DE EMERGENCIAS, VEHICULO DE SERVICIO DIPLOMATICO O CONSULADO, VEHICULO DE TRANSPORTE MASIVO, VEHICULO ESCOLAR}
FIELD[combobox] TIPO VEHICULO
FIELD[textfield] SIRAS
FIELD[textfield] NOMBREASEGURADORA
FIELD[textfield] NUMEROPOLIZAASEGURADORA
FIELD[datefield] VIGENCIA DESDE
FIELD[datefield] HASTA
FIELD[checkboxfield] SI
PANEL DATOS DEL VEHICULO DEL ACCIDENTE DE TRANSITO
FIELD[combobox] TIPO PROPIETARIO {PERSONA NATURAL, PERSONA JURIDICA}
FIELD[textfield] PRIMERAPELLIDOPROPIETARIO
FIELD[textfield] SEGUNDOAPELLIDOPROPIETARIO
FIELD[textfield] PRIMERNOMBREPROPIETARIO
FIELD[textfield] SEGUNDONOMBREPROPIETARIO
FIELD[textfield] RAZONSOCIALPROPIETARIO
FIELD[combobox] TIPO DE DOCUMENTO {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}
FIELD[textfield] DOCUMENTOPROPIETARIO
FIELD[textfield] TELEFONOPROPIETARIO
FIELD[textfield] DIRECCIONPROPIETARIO
PANEL DATOS DEL PROPIETARIO DEL VEHÍCULO
FIELD[textfield] PRIMERAPELLIDOCONDUCTOR
FIELD[textfield] SEGUNDOAPELLIDOCONDUCTOR
FIELD[textfield] PRIMERNOMBRECONDUCTOR
FIELD[textfield] SEGUNDONOMBRECONDUCTOR
FIELD[textfield] DOCUMENTOCONDUCTOR
FIELD[textfield] TELEFONOCONDUCTOR
FIELD[textfield] DIRECCIONCONDUCTOR
PANEL DATOS DEL CONDUCTOR DEL VEHÍCULO
FIELD[datefield] FECHAREMISION
FIELD[textfield] PRESONAREMITIDADE
FIELD[textfield] PERSONAQUEREMITE
FIELD[textfield] CARGOPERSONAREMITE
FIELD[textfield] DIRECCIONIPSREMITE
FIELD[textfield] TELEFONOREMITE
FIELD[combobox] DEPARTAMENTO IPS QUE REMITE
FIELD[combobox] MUNICIPIO IPS QUE REMITE
FIELD[datefield] FECHAACEPTACION
FIELD[textfield] PERSONAREMITIDAA
FIELD[textfield] PERSONAQUERECIBE
FIELD[textfield] CARGOPERSONARECIBE
FIELD[textfield] DIRECCIONIPSRECIBE
FIELD[textfield] TELEFONORECIBE
FIELD[combobox] DEPARTAMENTO IPS QUE RECIBE
FIELD[combobox] MUNICIPIO IPS QUE RECIBE
PANEL DATOS DE REMISION
FIELD[textfield] PLACAAMBULANCIA
FIELD[textfield] PRIMERAPELLIDOAMBULANCIA
FIELD[textfield] SEGUNDOAPELLIDOAMBULANCIA
FIELD[textfield] PRIMERNOMBREAMBULANCIA
FIELD[textfield] SEGUNDONOMBREAMBULANCIA
FIELD[textfield] DOCUMENTOAMBULANCIA
FIELDSET DATOS DEL CONDUCTOR QUE TRANSPORTABA LA VICTIMA
FIELD[textfield] TRASPORTEVICTIMADESDE
FIELD[textfield] TRANSPORTEVICTIMAHASTA
FIELD[combobox] TIPO TRANSPORTE {AMBULANCIA BASICA, AMBULANCIA MEDICA}
PANEL AMPARO DE TRANSPORTE Y MOVILIZACION DE LA VICTIMA
FIELD[datefield] FECHAINGRESO
FIELD[timefield] HORAINGRESO
GRID DIAGNOSTICO DE INGRESO: Código | Descripción | Prioridad
FIELD[datefield] FECHAEGRESO
FIELD[timefield] HORAEGRESO
GRID DIAGNOSTICO DE EGRESO: Código | Descripción | Prioridad
PANEL DATOS DE LA ATENCIÓN MEDICA DELA VICTIMA COMO PRUEBA DEL ACCIDENTE O EVENTO
FIELD[textfield] PRIMERAPELLIDOMEDICOFURIPS
FIELD[textfield] SEGUNDOPELLIDOMEDICOFURIPS
FIELD[textfield] PRIMERNOMBREMEDICOFURIPS
FIELD[textfield] SEGUNDONOMBREMEDICOFURIPS
FIELD[textfield] TIPODOCUMENTOMEDICOFURIPS
FIELD[textfield] DOCUMENTOMEDICOFURIPS
FIELD[textfield] NUMEROREGISTROMEDICO
FIELDSET MEDICO O PROFESIONAL TRATANTE
FIELD[textfield] BuscarMedico
BTN Buscar Paciente
PANEL DATOS DEL MEDICO O PROFESIONAL DE LA SALUD TRATANTE
FIELD[textfield] TxtGastoMediQuiVTF
FIELD[textfield] TxtGastoMediQuiVRF
FIELD[textfield] TxtGastosTransMovVictiVTF
FIELD[textfield] TxtGastosTransMovVictiVRF
PANEL AMPARO QUE RECLAMA
WINDOW FURIPS
FIELD[checkboxfield] Facturar sin un estado de cuenta
GRID : Numero de poliza | Fecha de registro
WINDOW Lista de Estados de cuenta
GRID : 1ER NOMBRE | 2DO NOMBRE | 1ER APELLIDO | 2DO APELLIDO | T.D. | DOCUMENTO
WINDOW Medicos encontradas
WINDOW Registrar Nuevo Paciente
FIELD[textfield] txtCopaId
FIELD[textfield] txtAgenda
FIELD[textfield] txtAgendaId
WINDOW Enviar Copago a Dian

## FACTURACIÓN > CAJA > APERTURA DE CAJA (/SUROSFacturacion/Vistas/Privado/Configuracion/AperturaCaja.aspx)
TITLE 
FIELD[textfield] Nombre:
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Cajas: Codigo | Nombre | Estado
BTN Agregar
BTN Cancelar
WINDOW Caja
FIELD[combobox] Caja: {<valores omitidos: nombres de personas y sedes>}
BTN Agregar caja
FIELD[combobox] Funcionario:
FIELD[textfield] Fecha/Hora
FIELD[numberfield] Valor
FIELD[textfield] Observaciones
BTN Guardar Apertura
FIELD[textfield] textfield-1038
FIELD[textfield] textfield-1041
FIELD[textfield] textfield-1044
FIELD[textfield] textfield-1047
FIELD[textfield] textfield-1050
FIELD[textfield] textfield-1053
FIELD[textfield] textfield-1056
GRID Aperturas: Codigo | Caja | Responsable | Fecha | Valor | Observaciones | Estado

## FACTURACIÓN > CAJA > CIERRE DE CAJA (/SUROSFacturacion/Vistas/Privado/Configuracion/ArqueoCaja.aspx)
TITLE 
GRID : Caja | Responsable
BTN Seleccionar
WINDOW Cajas seleccionadas
GRID : Caja | Responsable | Fecha apertura
WINDOW Selecciona la caja de tu interes
FIELD[datefield] Fecha inicia
FIELD[datefield] Fecha final
BTN Consultar cajas
FIELD[textfield] Cajas seleccionadas
FIELD[combobox] Con valor incial {SI, No}
FIELD[netmulticombo] Elementos a Visualizar {FACTURA, POS, COPAGO, CUOTA MODERADORA, COPAGO REGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS DE SALUD, ANTICIPO, NO APLICA}
BTN Consulta
GRID Arqueo: Tipo Fac | Numero copago | Numero Factura | Fecha Registro | No Documento | Persona | Empresa | No Cotrato | PROCEDIMIENTOS | OBSERVACIÓN | No. Nota credito | Valor Nota credito | T.Facturado | C.Recuperado | Subsidiado | Recaudado
BTN Exportar
BTN Imprimir
BTN Guardar Arqueo
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas

## FACTURACIÓN > CAJA > IMPRIMIR CIERRES (/SUROSFacturacion/Vistas/Privado/Configuracion/ImprimirArqueos.aspx)
TITLE 
FIELD[combobox] ComboOpcionFecha {MES, RANGO DE FECHAS}
FIELD[numberfield] TextAno
FIELD[combobox] ComboMes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] FechaI
FIELD[datefield] FechaF
FIELD[combobox] Cierre de Caja {<valores omitidos: nombres de personas y sedes>}
BTN Consultar
GRID : CAJA | FECHA APERTURA | RESPONSABLE | DOCUMENTO RESPONSABLE
GRID : Tipo Fac | No | Fecha | No Documento | Persona | Empresa | No Cotrato | PROCEDIMIENTOS | OBSERVACIÓN | No. Nota credito | Valor Nota credito | T.Facturado | C.Recuperado | Subsidiado | Recaudado
BTN Exportar
BTN Imprimir
WINDOW Arqueo

## FACTURACIÓN > HOMOLOGADORES > HOMOLOGADOR (/SUROSFacturacion/Vistas/Privado/Homologador/Homologador.aspx)
TITLE 
FIELD[displayfield] ctl21
FIELD[textfield] textfield-1014
FIELD[textfield] textfield-1017
FIELD[textfield] textfield-1020
GRID : CODIGO | DESCRIPCION | VALOR
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
FIELD[textfield] Código CUPS - Nombre o código:
PANEL Homologar con:
PANEL #
PANEL Tipo
PANEL Nombre o código
PANEL Valor (Unidad)
FIELD[textfield] ctl70
FIELD[textfield] TextReservado1
FIELD[textfield] TextISS
FIELD[textfield] TextISSValor
FIELD[textfield] ctl80
FIELD[textfield] TextReservado2
FIELD[textfield] TextSOAT
FIELD[textfield] TextSOATValor
FIELD[combobox] Facturar como: {RPMS CICLO 1 PRIMERA INFANCIA 0A a 5A, RPMS CICLO 2 INFANCIA 6A a 11A, RPMS CICLO 3 ADOLESCENTES 12A a 17A, RPMS CICLO 4 JOVENES 18A a 28A, RPMS CICLO 5 ADULTOS 29A a 59A, RPMS CICLO 6 ADULTOS MAYORES 60A, RPMS CONSULTA PRECONSEPCIONAL, RPMS CONSULTA PRENATAL, RPMS PARTOS, RPMS POST PARTO , RPMS RECIEN NACIDO, CONSULTA EXTERNA MEDICINA GENERAL., ATENCION INMEDIATA, INTERNACION, CONSULTA EXTERNA ODONTOLOGIA GENERAL., CONSULTA EXTERNA ENFERMERIA., PROCEDIMIENTOS EXTERNOS DE JEFE ENFERMERIA., PROCEDIMIENTOS EXTERNOS MEDICOS., IMAGENES DIAGNOSTICAS, FARMACIA, LABORATORIO CLINICO, VACUNACION, MEDICINA ESPECIALIZADA, TERAPIAS, TRASLADO ASISTENCIAL, OTROS}
FIELD[combobox] Concepto: {CONSULTAS, Procedimientos de diagnosticos, Procedimientos terapeuticos no quirurgicos, Procediminetos terapeuticos quirurgicos, Procedimientos de Promoción y prevención, ESTANCIAS, HONORARIOS, DERECHOS DE SALA, MATERIALES E INSUMOS, BANCO DE SANGRE, PRÓTESIS Y ÓRTESIS, Medicamentos POS, Medicamentos NO POS, TRASLADO DE PACIENTES, VACUNAS}
FIELD[combobox] Centro de costos:
FIELD[combobox] Archivo RIPS: {ARCHIVO DE PROCEDIMIENTOS, ARCHIVO DE CONSULTA, ARCHIVO DE OTROS SERVICIOS}
FIELD[combobox] Clasificación: {POS, NO POS}
FIELD[combobox] Valor Finalidad RPMS(PYP)
FIELD[textfield] Codigos
FIELD[textfield] TextEntidad
BTN Limpia la seleccion de los codigos de servicios
BTN Selecciona las entidades.
FIELD[combobox] Plan Unico de Cuenta:
FIELD[textareafield] Observación
FIELD[textareafield] TextRecomendaciones
PANEL Recomendaciones para la realización del procedimiento
GRID Clasificaciones CUPS: Clasificación Específica
BTN Aceptar y guardar
BTN Guardar
BTN Salir
WINDOW Homologador de manuales tarifarios con CUPS (Código único de procedimientos)
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field
FIELD[textfield] textfield-1064
FIELD[textfield] textfield-1067
FIELD[textfield] textfield-1070
FIELD[textfield] textfield-1073
FIELD[textfield] textfield-1076
FIELD[textfield] textfield-1079
FIELD[textfield] textfield-1082
FIELD[textfield] textfield-1085
FIELD[textfield] textfield-1088
FIELD[textfield] textfield-1091
FIELD[textfield] textfield-1094
FIELD[textfield] textfield-1097
FIELD[textfield] textfield-1100
FIELD[filefield] Seleccione una archivo XLS
BTN Crear homologación
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : Creación | CUPS | ISS | SOAT | Descripción | Facturar como | Concepto | Centro de costos | Archivo RIPS | Clasificación | Estado | Observación | Recomendaciones
BTN Editar
BTN Eliminar
FIELD[textfield] textfield-1123
FIELD[textfield] textfield-1125
GRID : DESCRIPCION | CODIGO
WINDOW Seleccionar los codigos de servicio

## FACTURACIÓN > HOMOLOGADORES > HOMOLOGADOR PROCEDIMIENTOS QUIRURGICOS (/SUROSFacturacion/Vistas/Privado/Homologador/HomologadorProcedimientosQuirurgicos.aspx)
TITLE 
FIELD[displayfield] ctl10
FIELD[textfield] textfield-1014
FIELD[textfield] textfield-1017
FIELD[textfield] textfield-1020
GRID : CODIGO | DESCRIPCION | VALOR
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
FIELD[textfield] Código CUPS - Nombre o código:
FIELD[combobox] Tipo intervención: {CRUENTOS, INCRUENTOS}
FIELD[combobox] Manual tarifario: {ISS 2001, SOAT 2019, SOAT 2018, SOAT 2017, SOAT 2020}
FIELD[textfield] Descripción:
FIELD[textfield] UVR:
FIELD[textfield] Grupo qx:
BTN Calcular valores
GRID : Id | Descripción | Código | Nombre del honorario | Valor
BTN Aceptar y guardar
BTN Salir
WINDOW Homologador procedimientos quirúrgicos
FIELD[textfield] textfield-1043
FIELD[textfield] textfield-1046
FIELD[textfield] textfield-1049
FIELD[textfield] textfield-1052
FIELD[textfield] textfield-1055
BTN Crear homologación
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : ID | CUPS | Descripción: | Manual tarifario | Valor total

## FACTURACIÓN > NOTAS CREDITOS > NOTA CREDITO (/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCredito.aspx)
TITLE 
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
FIELD[checkboxfield] Factura
FIELDSET DATOS FACTURA ELECTRÓNICA DE VENTA
FIELDSET DATOS DEL CLIENTE
FIELDSET DATOS DEL PACIENTE
FIELD[combobox] Motivo DIAN: {SELECCIONE, Devolución de parte de los bienes; no aceptación de partes del servicio, Anulación de factura electronica, Rebaja total aplicada, Descuento toal aplicado, Rescisión: Nulidad por falta de requisitos, Otros}
FIELD[combobox] ComboFormaPago {EFECTIVO, TARJETA DE CREDITO, TARJETA DÉBITO, CHEQUE, CREDITO, CONTADO}
FIELD[numberfield] txtPlazo
FIELDSET DATOS DE NOTA CREDITO
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
FIELD[textfield] PACIENTE:
GRID : ID | Información de la cita | Información del copago
BTN ACEPTAR
BTN CANCELAR
WINDOW RELACIONAR COPAGOS
FIELD[textfield] txtfainid
FIELD[textfield] tztnocdid
BTN Enviar
BTN Cancelar
FIELD[displayfield] ctl149
FIELD[textfield] textfield-1048
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : 
BTN Aceptar
BTN Salir
WINDOW Soportes factura
GRID Consolidado: ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total | Acción
GRID Cirugia: ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
BTN Relacionar Copago
GRID Recibo de pago: Caja | Concepto | Forma de pago | Cantidad | Valor a pagar | Total a pagar | Total pago | Saldo
FIELD[textfield] Valor Total:
FIELD[textareafield] txtObservacion
FIELD[datefield] Fecha facturación:
BTN Guardar
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas

## FACTURACIÓN > NOTAS CREDITOS > LISTADO NOTAS CREDITO (/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCredito.aspx)
TITLE 
GRID Facturas enviadas a la DIAN: Número Factura
GRID Facturas fallidas: Número Factura
WINDOW Reporte Envio Factura Electronica
FIELD[combobox] Consultar Por: {Numero Factura, Numero Nota, Rango de Fechas}
FIELD[textfield] Numero Factura
FIELD[textfield] Numero Nota
FIELD[datefield] Fecha Inicio
FIELD[datefield] Fecha Fin:
BTN Consultar
BTN Nota Credito Electronica
BTN Excel
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Reporte Notas Credito: CUV | Prefijo Nota | Número Nota | Prefijo Factura | Número Factura | Documento | Nombre | Empresa | Regimen | Contrato | Fecha Facturado | Fecha Nota | Valor Total Factura | Valor Total Nota
FIELD[textfield] TextNocdIdSoloProcedimientoJson
BTN Aceptar
BTN Cancelar
GRID : Descripción | Carta
BTN Enviar
FIELD[combobox] Credenciales WebSisPro {<valor omitido>}
BTN VALIDAR
WINDOW Validar Rips
BTN Imprimir Nota Credito
BTN Imprimir Factura Relacionada
BTN Validar al Ministerio

## FACTURACIÓN > NOTAS CREDITOS > NOTA CREDITO GLOBAL (/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCreditoGlobal.aspx)
TITLE 
FIELD[textfield] Numero de factura global
BTN Buscar Informacion de la factura global.
FIELD[checkboxfield] Factura
FIELDSET DATOS FACTURA ELECTRÓNICA DE VENTA
FIELDSET DATOS DEL CLIENTE
FIELD[combobox] Motivo DIAN: {SELECCIONE, Devolución de parte de los bienes; no aceptación de partes del servicio, Anulación de factura electronica, Rebaja total aplicada, Descuento total aplicado, Rescisión: Nulidad por falta de requisitos, Otros}
FIELD[combobox] ComboFormaPago {EFECTIVO, TARJETA DE CREDITO, TARJETA DÉBITO, CHEQUE, CREDITO, CONTADO}
FIELD[numberfield] txtPlazo
FIELDSET DATOS DE NOTA CREDITO
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
FIELD[textfield] txtfainid
FIELD[textfield] tztnocdid
BTN Enviar
BTN Cancelar
FIELD[displayfield] ctl95
FIELD[textfield] textfield-1032
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : 
BTN Aceptar
BTN Salir
WINDOW Soportes factura
FIELD[combobox] Forma de pago {Efectivo}
FIELD[combobox] Concepto pago {COPAGO, CUOTA MODERADORA, COPAGO REGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS DE SALUD, ANTICIPO, NO APLICA}
FIELD[numberfield] Cantidad
FIELD[numberfield] Valor unitario
FIELD[textfield] Valor total
FIELD[textareafield] Observación
BTN Añadir
WINDOW Nuevo recibo de pago
GRID Consolidado: ID | Cód | Concepto | Observacion | Cantidad | Valor/U | Valor Total
BTN Relacionar Copago
GRID Recibo de pago: Concepto | Forma de pago | Cantidad | Valor Unitario | Valor Total
FIELD[textfield] Valor Total:
FIELD[textareafield] txtObservacion
FIELD[datefield] Fecha facturación:
BTN Guardar

## FACTURACIÓN > NOTAS CREDITOS > LISTADO NOTA CREDITO GLOBAL (/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCreditoGlobal.aspx)
TITLE 
GRID Facturas enviadas a la DIAN: Número Factura
GRID Facturas fallidas: Número Factura
WINDOW Reporte Envio Factura Electronica
FIELD[combobox] Consultar Por: {Numero Factura, Numero Nota, Rango de Fechas}
FIELD[textfield] Numero Factura
FIELD[textfield] Numero Nota
FIELD[datefield] Fecha Inicio
FIELD[datefield] Fecha Fin:
BTN Consultar
BTN Nota Credito Electronica
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Reporte Facturas: Prefijo Nota | Número Nota | Prefijo Factura | Número Factura | Documento | Nombre | Empresa | Regimen | Contrato | Fecha Facturado | Fecha Nota | Valor Total Factura | Valor Total Nota
FIELD[textfield] TextNocdIdSoloProcedimientoJson
BTN Aceptar
BTN Cancelar
GRID : Descripción | Carta
BTN Enviar
FIELD[combobox] Credenciales WebSisPro {<valor omitido>}
BTN VALIDAR
WINDOW Validar Rips
BTN Imprimir Nota Credito
BTN Imprimir Factura Relacionada
BTN Validar al Ministerio

## FACTURACIÓN > NOTAS DEBITO > NOTAS DEBITO (/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaDebito.aspx)
TITLE 
FIELD[numberfield] ctl309
FIELD[numberfield] ctl312
FIELD[numberfield] ctl315
FIELD[textfield] ctl559
GRID : Documento | Nombre paciente
BTN Cerrar
WINDOW Coincidencia con el parámetro ingresado
FIELD[textfield] PACIENTE:
GRID : ID | Información de la cita | Información del copago
BTN ACEPTAR
BTN CANCELAR
WINDOW RELACIONAR COPAGOS
FIELD[textfield] txtfainid
FIELD[textfield] tztnocdid
BTN Enviar
BTN Cancelar
FIELD[displayfield] ctl76
FIELD[textfield] textfield-1036
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : 
BTN Acelptar
BTN Salir
WINDOW Soportes factura
BTN Agregar
WINDOW Adjuntar recibo de pago
FIELD[textfield] Buscar procedimiento
BTN Buscar Procedimiento ingresado
FIELD[numberfield] Cantidad
FIELD[numberfield] Valor/U
FIELD[numberfield] Valor Total
FIELD[numberfield] Comisión
FIELD[numberfield] Descuento
FIELD[textareafield] Observacion
BTN Agregar y Cerrar
WINDOW Panel asistencial
FIELD[triggerfield] Búsqueda
FIELD[textfield] Medicamento
FIELD[textfield] Cum
FIELD[numberfield] Valor real
WINDOW Panel Medicamentos
BTN Copago relacionado
BTN Nuevo copago
WINDOW Opciones
GRID : Código | Descripción | Forma Farmaceutica | Volumen|Peso Presentación | Concentración | Existencias
BTN Aceptar
WINDOW Coincidencia de medicamentos
FIELD[textfield] Insumo
FIELD[textfield] Codigo
WINDOW Panel Insumos
GRID : Código | Nombre | Presentación | Existencias
WINDOW Coincidencia de Insumos
FIELD[textfield] HidenPrquIdPer
FIELD[textfield] HiddenPrquCodigoPer
FIELD[textfield] HiddenPrquDescripcionPer
FIELD[textfield] TextCantidadPer
FIELD[textfield] TextValorPer
FIELD[textfield] TextDescuentoPer
FIELD[textfield] TextValorTotalPer
FIELD[textfield] TextValorOriginaPerl
FIELD[textfield] HidenIncrementoPer
FIELD[textfield] HidenServicioPer
FIELD[textfield] Nombre usuario
FIELD[textfield] Contraseña
BTN Continuar
FORM El procedimiento ya se encuentra en la lista, Para agregar ingrese credenciales
WINDOW Ingresar credenciales
GRID : Iss | Valor Iss | Soat | Valor Soat
WINDOW Seleccione el homologo con el que desea facturar
GRID : Código | Descripción | Tipo manual
WINDOW Coincidencias encontradas
FIELD[combobox] Cirujano
FIELD[combobox] Anestesiologo
FIELD[combobox] Ayudante:
FIELD[textfield] No autorización:
FIELD[combobox] Tipo cirugia: {LIMPIA, LIMPIA CONTAMINADA, CONTAMINADA, SUCIA}
FIELD[combobox] Tipo anestesia: {LOCAL, REGIONAL, BLOQUEO, GENERAL}
FIELD[datefield] Fecha Cirugia:
FIELD[combobox] Vía de acceso: {BILATERALES, UNICA VIA IGUAL CIRUJANO, DISTINTA VIA IGUAL CIRUJANO, DIFERENTES ESPECIALISTAS POR IGUAL O DISTINTA VIA}
FIELD[textfield] Código/Nombre CIE10
BTN Buscar registros del CIE10
FIELD[combobox] ComboTipoDiagnosticoCirugia {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}
GRID : Código | Descripción | Prioridad
FIELDSET Ejecución de procedimientos
FIELD[textfield] Código CUPS - Nombre o código:
GRID : Código | Código | Descripción | Cantidad | Valor Unitario | Valor total
WINDOW Cirujia
GRID : Código | Descripción
WINDOW Coincidencias encontradas en el CIE10
FIELD[textfield] Documento/Nombre
BTN Buscar paciente en base al parámetro ingresado.
FIELD[checkboxfield] Factura
FIELDSET DATOS FACTURA ELECTRÓNICA DE VENTA
FIELDSET DATOS DEL CLIENTE
FIELDSET DATOS DEL PACIENTE
FIELD[combobox] Motivo DIAN: {SELECCIONE, Intereses, Gastos por cobrar, Cambio del valor, Otro}
FIELD[combobox] ComboFormaPago {EFECTIVO, TARJETA DE CREDITO, TARJETA DÉBITO, CHEQUE, CREDITO, CONTADO}
FIELD[numberfield] txtPlazo
FIELDSET DATOS DE NOTA CREDITO
BTN Asistencial
BTN Recibo de pago
BTN Medicamentos
BTN Insumos
BTN Cirugia
BTN RPMS
GRID Consolidado: ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
GRID : ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
GRID Cirugia: ID | Cum/Cód | Concepto | Observacion | Valor Real | % | Cantidad | Valor/U | Descuento | Valor Total
BTN Relacionar Copago
GRID Recibo de pago: Caja | Concepto | Forma de pago | Cantidad | Valor a pagar | Total a pagar | Total pago | Saldo
GRID Recibo de pago: Caja | Concepto | Forma de pago | Cantidad | Valor | Total a pagar | Total pago | Saldo
FIELD[textfield] Valor Total:
FIELD[textareafield] txtObservacion
FIELD[datefield] Fecha facturación:
BTN Guardar
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas

## FACTURACIÓN > NOTAS DEBITO > LISTADO NOTAS DEBITO (/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasDebito.aspx)
TITLE 
GRID Facturas enviadas a la DIAN: Número Factura
GRID Facturas fallidas: Número Factura
WINDOW Reporte Envio Factura Electronica
FIELD[combobox] Consultar Por: {Numero Factura, Numero Nota, Rango de Fechas}
FIELD[textfield] Numero Factura
FIELD[textfield] Numero Nota
FIELD[datefield] Fecha Inicio
FIELD[datefield] Fecha Fin:
BTN Consultar
BTN Nota Debito Electronica
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Reporte Nota Debito: Prefijo Nota | Número Nota | Prefijo Factura | Número Factura | Documento | Nombre | Empresa | Regimen | Contrato | Fecha Facturado | Fecha Nota | Valor Total Factura | Valor Total Nota
BTN Imprimir Nota Debito
BTN Imprimir Factura Relacionada

## FACTURACIÓN > CONTRATACIÓN (/SUROSFacturacion/Vistas/Privado/Contratos/ListaContratos.aspx)
TITLE 
FIELD[textfield] Nombre del Archivo Soporte
FIELD[combobox] Tipo Soporte {COLUMNA, SCRIPT}
FIELD[combobox] Columna de Tabla Soporte
FIELD[combobox] Elija Script
BTN Guardar
BTN Cancelar
WINDOW Agregar nuevo archivo soporte
GRID :
BTN Nuevo
WINDOW Configuración de generación de PDF
BTN Cerrar
WINDOW Detalle objeto del contrato
FIELD[textfield] No Otro Si:
FIELD[datefield] Inicio otro si:
FIELD[datefield] Fin otro si:
FIELD[numberfield] Valor otro sí:
FIELD[textareafield] TextObjetoContrato
BTN Aceptar y guardar
BTN Salir
WINDOW Crear Otro Sí
FIELD[displayfield] ctl96
FIELD[textfield] textfield-1043
FIELD[textfield] textfield-1046
GRID : CODIGO | NOMBRE
BTN Aceptar
WINDOW Coincidencia encontrada
FIELD[textfield] Nombre servicio
FIELD[textfield] Título del servicio
FIELD[combobox] Tipo de atención
FIELD[combobox] Manual Tarifario
FIELD[combobox] Incremento
FIELD[numberfield] Valor
FIELD[netmulticombo] Definición de ingreso
FIELD[combobox] Estado {ACTIVO, INACTIVO}
FIELD[displayfield] ctl138
FIELD[textfield] textfield-1059
FIELD[textfield] textfield-1062
FIELD[combobox] ComboEspecialidad
GRID : Codigo | Nombre
BTN Eliminar
WINDOW Asignar servicio a contrato
FIELD[displayfield] ctl174
FIELD[textfield] textfield-1075
FIELD[textfield] textfield-1078
FIELD[textfield] textfield-1081
FIELD[textfield] textfield-1083
FIELD[textfield] textfield-1085
FIELD[textfield] textfield-1088
FIELD[textfield] textfield-1090
FIELD[textfield] textfield-1093
BTN Agregar
GRID : Id | Fecha Creación | Nombre | Manual tarifario | Incremento | Valor | Definición ingreso | Estado
BTN Editar
WINDOW Lista de servicios del contrato
WINDOW Crear Contrato
GRID : ID | Nombre | Obligatorio? | Grupo | Sigla | Activo
WINDOW Configurar archivos de soporte por contrato
FIELD[textfield] textfield-1115
FIELD[textfield] textfield-1118
FIELD[textfield] textfield-1121
FIELD[textfield] textfield-1124
FIELD[textfield] textfield-1127
FIELD[textfield] textfield-1130
FIELD[displayfield] ctl285
GRID : Id | MODALIDAD COBRO | CONDICION | VALOR CONDICION | CODIGO | DESCRIPCION
WINDOW Configurar Tiempo Instancia
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Lista de chequeo soportes: NOMBRE
WINDOW Agregar lista de chequeo
FIELD[combobox] Seleccione una instancia a facturar {OBSERVACIÓN, HOSPITALIZACIÓN, AFINAMIENTO}
FIELD[triggerfield] Procedimiento con el que facturará
FIELDCONTAINER Condición
FIELD[combobox] Seleccione Condición {DURACION, CANTIDAD EVOLUCIONES, ESPECIALIDAD, ORDEN OSPITALIZACION, ANEXO}
FIELDSET Tipo de condición
FIELD[combobox] Especialidad
FIELDSET Especialidades
FIELD[textfield] Incial
FIELD[textfield] Final
FIELDSET DURACION
FIELD[textfield] Cantidad
FIELDSET CANTIDAD EVOLUCIONES
FIELD[checkboxfield] Orden Obligatoria
FIELDSET ORDEN
WINDOW Agregar Condicion para facturación de instancia
FIELD[displayfield] ctl357
FIELD[textfield] textfield-1167
FIELD[textfield] textfield-1170
FIELD[textfield] textfield-1173
GRID : Nombre | Concepto | Estado
BTN Nuevo grupo
BTN Editar grupo
BTN Eliminar grupo
BTN Items del grupo
FIELD[combobox] Estado {Activo, Inactivo, Todos}
BTN Actualizar lista
WINDOW Tarifa propia
FIELD[textfield] Nombre
FIELD[combobox] Concepto
FIELD[combobox] Estado {Activo, Inactivo}
FIELD[triggerfield] Nombre
FIELD[textfield] CUMM
FIELD[numberfield] CONSEC
FIELD[textfield] Grupo
FIELD[combobox] Modalidad: {Paquete, Costo fijo, Manual Tarifario, Incremento, Costo Fijo Externo}
FIELD[numberfield] Valor fijo:
FIELD[displayfield] ctl438
FIELD[textfield] textfield-1209
FIELD[textfield] textfield-1212
FIELD[textfield] textfield-1215
BTN Actualizar información
GRID : Descripción | Clasificación Rips | Estado/Clasificación
FIELD[displayfield] ctl485
FIELD[textfield] textfield-1241
FIELD[textfield] textfield-1244
FIELD[textfield] textfield-1247
FIELD[displayfield] ctl532
FIELD[textfield] textfield-1273
FIELD[textfield] textfield-1276
FIELD[textfield] textfield-1279
FIELD[displayfield] ctl579
FIELD[textfield] textfield-1305
FIELD[textfield] textfield-1308
FIELD[textfield] textfield-1311
FIELD[displayfield] ctl612
FIELD[textfield] textfield-1337
GRID : 
FIELD[combobox] Tipo De Contenido {PRECEDIMINETOS, MEDICAMENTOS, INSUMOS}
FIELD[filefield] BTN_IMPORTAR
FIELD[combobox] Accion {AGREGAR, NO AGREGAR}
FIELD[combobox] Grupos Del Contrato
BTN Procedimientos
BTN Medicamemtos
BTN Insumos
BTN Descargar Archivos De Ejemplo
WINDOW Cargar Precios
FIELD[textfield] textfield-1356
GRID : SERVICIOS
FIELD[textfield] textfield-1361
FIELD[textfield] textfield-1364
FIELD[textfield] textfield-1367
BTN Seleccionar Todos
GRID : INCLUIDO | ID UNICO | NOMBRE SUBPLAN
WINDOW Sub Planes del Contrato
GRID : CODIGO | DESCRIPCION
PANEL Actualizados
PANEL Completos Nuevos
PANEL No Actualizados
BTN Exportar
WINDOW RESULTADO
FIELD[combobox] Estado de contratos {ACTIVO, CANCELADO, EJECUTADO, EN EJECUCIÓN, INACTIVO, LIQUIDADO}
FIELD[textfield] INGRESE UN VALOR DE BÚSQUEDA
BTN Crear un contrato
BTN Refrescar
GRID : INFORMACIÓN DEL CONTRATO | FECHAS | VALOR DEL CONTRATO | Id | EMPRESA CONTRATANTE | ESTADO | OTRO SÍ
BTN Crear Otro Sí
BTN Agregar Procedimientos al contrato
BTN Configurar archivos de soporte
BTN Configurar Tiempo instancia
BTN Cargar Archivo de Precios
BTN Agregar Sub Plan
BTN VER OBJETO CONTRATO

## FACTURACIÓN > PARAMETROS DE FACTURACION (/SUROSFacturacion/Vistas/Privado/Configuracion/ParametroFactura.aspx)
TITLE 
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Lista de parámetros ingresados: ID | Resolucion | Prefijo | Numeración | Vigencia
BTN Editar
FIELD[textfield] Resolución:
FIELD[textfield] Pie de página
FIELD[textfield] Texto Anexo
FIELD[textfield] Prefijo inicio
FIELD[textfield] Prefijo Fin
FIELD[textfield] No. Inicial
FIELD[textfield] No. Final
FIELD[textfield] No. Inicio Factura
FIELD[checkboxfield] Estado
FIELD[combobox] Tipo de Factura {POS, FACTURA ELECTRONICA DE VENTA, DOCUMENTO DE COTIZACION, PREFACTURA, DOCUMENTO SOPORTE, POS ELECTRONICA, NOTA CREDITO FACTURA, NOTA DEBITO FACTURA, NOTA CREDITO DOCUMENTO SOPORTE, NOTA DEBITO DOCUMENTO SOPORTE, NOTA CREDITO DOCUMENTO EQUVALENTE, NOTA DEBITO DOCUMENTO EQUVALENTE}
FIELD[textfield] Descripcion de la resolución
FIELD[datefield] Fecha vigencia:
FIELD[datefield] Fecha vencimiento:
BTN Guardar
BTN Cancelar
GRID PRESTADOR DE SERVICIO DE LA RESOLUCION: Prestador Servicio | Codigo Habilitacion
GRID RESOLUCIONES DISPONIBLES: Resolucion | Prefijo
FORM Parámetros factura

## INFORMES > INFORMES (/SUROSHistoriaClinica/Vistas/Privado/Informes/InicioInformes.aspx)
TITLE Inicio Historia clinica
FIELD[displayfield] ctl11
FIELD[textfield] textfield-1012
FIELD[combobox] Especialidad
GRID : MEDICO
BTN Aceptar
BTN Cancelar
WINDOW Seleccionar medicos
TOOLTIP Actualizar
FIELD[textfield] textfield-1026
GRID : ESPECIALIDAD
WINDOW Seleccionar especialidad
FIELD[textfield] textfield-1038
FIELD[textfield] textfield-1040
GRID : EMPRESA | REGIMEN
WINDOW Seleccionar Entidad
FIELD[textfield] TextMedicos
BTN Limpia la selección
BTN Selecciona los medicos.
FIELD[textfield] TextEspecialidad
BTN Limpia la seleccion de las especialidades
BTN Selecciona las especialidades.
FIELD[netmulticombo] ComboEstadoCita {CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}
FIELD[textfield] TextEntidad
BTN Limpia la seleccion de las entidades
BTN Selecciona las entidades.
FIELD[triggerfield] TriggerField1
TREE LISTA DE INFORMES
PANEL CONFIGURACIÓN GENERAL
FIELD[combobox] Opcion de fecha {MES, RANGO DE FECHAS}
FIELD[numberfield] Año
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] Fecha inicial
FIELD[datefield] Fecha Final
BTN Exportar A EXCEL
BTN Consultar
FIELD[combobox] PROCESOCREATE
FIELD[datefield] FECHAINICIOCREATE
FIELD[datefield] FECHAFINCREATE
FIELD[numberfield] ctl132
FIELD[combobox] ComboBox3
FIELD[combobox] ComboBox4
FIELD[textfield] FECHAINCIO
BTN Guardar
BTN Salir
WINDOW Crear informe de resolucion 256
FIELD[textfield] INDICA
FIELD[datefield] FECHAINICIOEMPRESA
FIELD[datefield] FECHAFINEMPRESA
FIELD[numberfield] ESTANDARNUMEROREPORTENUEVO
FIELD[combobox] Selecciona una opción
WINDOW Nuevo reporte
FIELD[textfield] NOMBREDOMINIO
WINDOW CREAR NUEVO DOMINIO
FIELD[combobox] PROCESOCARPETA
FIELD[datefield] FECHAINICIOEDITMODULO
FIELD[datefield] FECHAFINEDITMODULO
FIELD[numberfield] STANDARVALUE
WINDOW Editar modulo
BTN Crear nueva carpeta
BTN Editar modulo
BTN Nuevo reporte
BTN Crear modulo
BTN Crear nuevo reporte por especialidad
FIELD[datefield] FECHAINICIOESPECIALIDAD
FIELD[datefield] FECHAFINESPECIALIDAD
FIELD[numberfield] NUMEROESPECIALIDADESTANDAR
FIELD[netmulticombo] COMBOBOXESPECIALIDAD
WINDOW Nuevo reporte por especialidad
FIELD[datefield] FECHAIEDITAR
FIELD[datefield] FECHAFEDITAR
FIELD[numberfield] ESTANDAREDITAR
FIELD[combobox] Selecciona una opción {DIAS, MENSUAL, TRIMESTRE, SEMESTRE, ANUAL, %, MINUTOS}
FIELD[combobox] Selecciona una opción {DIAS, MENSUAL, TRIMESTRE, SEMESTRE, ANUAL, MINUTOS}
FIELD[combobox] Selecciona una opción {PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
WINDOW Editar reporte
LABEL 200
LABEL OK
FIELD[htmleditor] htmleditor-1130
WINDOW Request Failure

## INFORMES > REPORTE REMISIONES (/SUROSHistoriaClinica/Vistas/Privado/Informes/ReporteRemisiones.aspx)
TITLE Reporte Remisiones
FIELD[combobox] Tipo de Consulta {Rango De Fechas, Mes}
FIELD[datefield] Inicial
FIELD[datefield] Final
FIELD[numberfield] Año
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
BTN Consultar
BTN Exportar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID Reporte Remisiones: Documento | Paciente | Departamento | Telefono | Fecha Soli | Cantidad | Codigo | Descripción | Observacion | Especialidad Remite | Empresa | Cie10 | Cie Descripción | Persona Remite | Edad | Genero

## INFORMES > REPORTE CITAS MEDICAS (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Reportes/ReporteCitasMedicas.aspx)
TITLE Reporte citas medicas
GRID : Código | Descripción
BTN Aceptar
BTN Salir
WINDOW Coincidencias encontradas en el CIE10
WINDOW Coincidencias encontradas de CUPS
FIELD[textfield] Código/Nombre CIE10
BTN Buscar registros del CIE10
BTN Cancelar
WINDOW Diagnosticos
FIELD[textfield] Código/Nombre CUPS
BTN Buscar registros del CUPS
WINDOW CUPS
FIELD[displayfield] ctl72
FIELD[textfield] textfield-1036
FIELD[combobox] Especialidad
FIELD[combobox] Estado {TODOS, ACTIVOS, INACTIVOS}
GRID : MEDICO
WINDOW Seleccionar medicos
TOOLTIP Actualizar
FIELD[textfield] textfield-1050
GRID : ESPECIALIDAD
WINDOW Seleccionar especialidad
FIELD[textfield] textfield-1062
FIELD[textfield] textfield-1064
GRID : EMPRESA | REGIMEN
WINDOW Seleccionar Entidad
FIELD[textfield] TextMedicos
BTN Limpia la seleccion de los medicos
BTN Selecciona los medicos.
FIELD[textfield] TextEspecialidad
BTN Limpia la seleccion de las especialidades
BTN Selecciona las especialidades.
FIELD[textfield] TextEntidad
BTN Limpia la seleccion de las entidades
BTN Selecciona las entidades.
FIELD[textfield] TextContrato
BTN Limpia la seleccion de los contratos
BTN Selecciona los contratos.
PANEL Parametros generales
FIELD[combobox] ComboOpcionFecha {MES, RANGO DE FECHAS}
FIELD[combobox] ComboBoxIdPrestadorServicio {TODOS, PRORED - FLORENCIA - CAQUETA, PRORED - CAUCA, PRORED - PASTO - NARIÑO, PRORED - RISARALDA}
FIELD[numberfield] TextAno
FIELD[combobox] ComboMes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] FechaI
FIELD[datefield] FechaF
FIELD[netmulticombo] TIPOCONSULTA {CITAS MEDICAS, CIRUGIAS, PROCEDIMIENTOS, RAYOS X, LABORATORIOS, URGENCIAS, QUIMIOTERAPIA}
FIELD[netmulticombo] Estado de la cita: {CIRUGIA, CANCELADO, NO ASISTIO, ASIGNADO, EN ATENCION, ATENDIDO, CANCELADO REPROGRAMACION, ACTIVADO, FACTURADO, ASIGNADA POR BOT}
FIELD[textfield] TextDiagnostico
BTN Limpia la seleccion de los diagnosticos
BTN Selecciona los procedimientos.
FIELD[textfield] TextoCUPS
BTN Limpia la seleccion de los CUPS
FIELD[netmulticombo] Prioridad {PRINCIPAL, SECUNDARIO}
FIELD[netmulticombo] Jornada {TURNO 1, TURNO 2, TURNO 3, TURNO 4, TURNO 5, TURNO 6, TURNO 7, TURNO 8, TURNO 9, TURNO 10}
FIELD[combobox] ComboCampos {GENERAL, RESUMIDO}
BTN Reporte de Citas Demdicas
BTN Info. Mensaje Masivos
BTN EXPORTAR A EXCEL
BTN CONSULTAR
FORM Filtros del reporte
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : FECHA ASIGNACIÓN | FECHA ATENCIÓN | TURNO | TIPOTIPO SOICITUD | TIPOTIPO CONSULTA | TIPOCITA | ESTADOCITA | ESTADOINGRESO | JORNADA | HORA | TIPO DOC | DOCUMENTO | NOMBRE PACIENTE | FECHA NACIM | ETNIA | GENERO | PRESTADOR SERVICIO | EMPRESA | CONTRATO | REGIMEN | COD. DIAGNOSTICO. | DESCRIPCION DIAGNOSTICO | PRIORIDAD DIAGNOSTICO | CODIGO CUPS | PROCEDIMIENTOS | DOC. MEDICO | NOMBRE MEDICO | ESPECIALIDAD | TIPO HISTORIA | OBSERVACION
FIELD[textfield] textfield-1111
GRID : CONTRATO
WINDOW Seleccionar los contratos

## MI CUENTA > CAMBIAR CONTRASEÑA (/SUROS/Vistas/Privado/Funcionario/CambiarContrasena.aspx)
TITLE Cambiar contraseña
FIELD[textfield] Ingrese la contraseña actual
FIELD[textfield] Nueva contraseña
FIELD[textfield] Ingrese nuevamente la Contraseña
BTN Aceptar
FORM Cambiar contraseña

## MI CUENTA > DATOS PERSONALES (/SUROS/Vistas/Privado/Funcionario/FormularioFuncionarioPersonal.aspx)
TITLE Datos personales funcionario

## PACIENTE > CONSULTAR CITAS DEL PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/ReporteCitasPaciente.aspx)
TITLE Reporte Citas Paciente
GRID : DOCUMENTO | NOMBRE PACIENTE
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
FIELD[textfield] Documento/Nombre
BTN Consultar
FIELD[textfield] TextDocumentoPaciente
FIELD[textfield] TextNombrePaciente
GRID Citas medicas del paciente: Mes | Fecha | Turno | Hora | Medico | Registrado por | Nota | Tipo asignación | Estado
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field

## PACIENTE > DATOS PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/FormularioPaciente.aspx)
TITLE Formulario Paciente
WINDOW Actualizando Foto de Inicio
FIELD[filefield] Imagen
BTN Establecer
BTN Cancelar
WINDOW Cargar documento (Frente)
WINDOW Cargar documento (Reverso)
FIELD[textfield] Documento
FIELD[textfield] Nombre
FIELD[textfield] Telefono
FIELD[textfield] Parentesco
FIELD[combobox] EPS afiliado
FIELD[textfield] Otra EPS
BTN Aceptar
WINDOW Datos del Responsable
FIELD[combobox] Pais
FIELD[combobox] Departamento
FIELD[combobox] Municipio
FIELD[checkboxfield] .
WINDOW Municipio
GRID : DOCUMENTO | NOMBRE PACIENTE
WINDOW Coincidencia encontrada
FIELD[textfield] textfield-1027
FIELD[textfield] textfield-1029
FIELD[textfield] textfield-1032
FIELD[textfield] textfield-1035
GRID : PERTENECE | CÓDIGO | NOMBRE
WINDOW Grupo Poblacional
PANEL Foto de perfil
PANEL Cara A del documento
PANEL Cara B del documento
PANEL Datos del paciente
PANEL Datos Biométricos
FIELD[combobox] ComboTipoDocumento {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}
FIELD[textfield] TextDocumento
FIELD[textfield] ExpedidaEn
BTN Buscar Municipio
FIELD[datefield] dd/mm/yyyy
FIELD[textfield] TextEdadPaciente
FIELD[combobox] ComboGenero {MUJER, INDETERMINADO O INTERSEXUAL, HOMBRE}
FIELD[combobox] IdentidadGenero {NEUTRO, MASCULINO, FEMENINO, TRANSGENERO, NO LO DECLARA}
FIELD[combobox] ComboOcupacion
FIELD[combobox] ComboCargo
FIELD[textfield] TextEmail
FIELD[textfield] TextPNombre
FIELD[textfield] TextSNombre
FIELD[textfield] TextPApellido
FIELD[textfield] TextSApellido
FIELD[combobox] ComboTipoAfiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR / AMPARADO ARL, TOMADOR / AMPARADO SOAT, TOMADOR / AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXEPCION NO COTIZANTE LEY 352 DE 1997}
FIELD[textfield] TextNombreCotizante
FIELD[combobox] ComboEmpresa
FIELD[checkboxfield] Exonerado Copago?
FIELD[combobox] ComboTipoExoneracion
FIELD[textfield] TextMunicipioNac
FIELD[textfield] TextMunicipioRec
FIELD[combobox] ComboEtnia {OTRAS ETNIAS, INDIGENA, RAIZAL (ARCHIPIELAGO SAN ANDRÉS Y PROVIDENCIA), GITANO, PALENQUERO DE SAN BASILIO, NEGRO(A) O MULATO(A) O AFROCOLOMBIANO(A) O AFRODESCENDIENTE, AFROCOLOMBIANO}
FIELD[combobox] ComboEstadoCivil {ESTADO NO SUMINISTRADO, CASADO(A), DIVORCIADO(A), MENOR DE EDAD, SOLTERO(A), UNION LIBRE, VIUDO}
FIELD[combobox] ComboDiscapacidad {DISCAPACIDAD FÍSICA, DISCAPACIDAD VISUAL, DISCAPACIDAD AUDITIVA, DISCAPACIDAD INTELECTUAL, DISCAPACIDAD SICOSOCIAL, SORDOCEGUERA, DISCAPACIDAD MÚLTIPLE, SIN DISCAPACIDAD}
FIELD[combobox] ComboNivelEducativo {NO DEFINIDO, PRESCOLAR, BASICA PRIMARIA, BASICA SECUNDARIA, MEDIA ACADEMICA O CLASICA, MEDIA TECNICA, NORMALISTA, TECNICA PROFESIONAL, TECNOLOGICA, PROFESIONAL, ESPECIALIZACION, MAESTRIA, DOCTORADO}
FIELD[textfield] TextDireccion
FIELD[combobox] ComboUbicacionResidencial {RURAL, URBANA}
FIELD[textfield] TextCelular
FIELD[textfield] TextTelefono
FIELD[textfield] TextAcudiente
BTN Asignar datos del acompañante
BTN Borrar acompañante
FIELD[combobox] CBEstadoPaciente
FIELD[combobox] CBContinuaAtencion {Si, No}
FIELD[textfield] TextGrupoPoblacional
BTN Buscar Grupos Pobalcionales
FIELD[filefield] Seleccione una archivo XLS
FIELD[textfield] Documento/Nombre
BTN Buscar paciente
FIELD[combobox] Tipo paciente:
BTN Guardar
BTN Guardar y cerrar
BTN Limpiar formulario
FORM Gestionar datos del paciente

## PACIENTE > PACIENTES (/SUROSHistoriaClinica/Vistas/Privado/Paciente/Paciente.aspx)
TITLE Persona
FIELD[textfield] TextIdFilter
FIELD[textfield] TextDocumentoFilter
FIELD[textfield] TextNombreFilter
FIELD[textfield] TextGeneroFilter
FIELD[datefield] DateFechaNacimientoFilter
FIELD[textfield] TextCelularFilter
FIELD[textfield] TextEmailFilter
FIELD[combobox] ComboBoxEmpresaFilter {ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I}
BTN Total Pacientes!
BTN Refrescar Lista
BTN Exportar
BTN Esta lista contiene mis pedidos de insumos
BTN First Page
BTN Previous Page
BTN Next Page
BTN Last Page
BTN Refresh
GRID : ID | Foto | Documento | Nombre | Sexo | Nacimiento | Celular | Email | EPS
BTN Consultar y gestionar

##  > ALMACEN (/SUROSAlmacen/Vistas/InicioAlmacen.aspx)
TITLE SoftProject|Almacenes
WINDOW Sesión finalizada
FIELD[textfield] Nueva contraseña
FIELD[textfield] Confirmar contraseña
FIELD[displayfield] TextoDescripcionNuevaCC
BTN Aceptar
WINDOW Asignar nueva contraseña
FIELD[textareafield] Mensaje
FIELD[combobox] Seleccione
BTN Enviar
BTN Salir
FIELD[combobox] Rol a notificar
FIELD[combobox] Especialidad
WINDOW Envio de notificación médica
TREE TreeMenuOpciones
PANEL Inicio

##  > HISTORIA CLINICA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/InicioHistoria.aspx)
TITLE Inicio Historia clinica
FIELD[combobox] Credenciales
BTN CONECTAR
BTN VALIDAR
GRID : TIPO | Codigo | Suministro | Solicitada | Entregada
GRID Suministros en inventario: Cant. Entrega | Item | Presentación | Lote | Fecha Venc. | Cant. Actual | Cant. Descargada. | Cant. Almacenada.
FIELD[combobox] Almacen Stock
BTN Finalizar
WINDOW Despacho de suministros desde enfermeria
BTN Sort Ascending
BTN Sort Descending
BTN Columns
FIELD[displayfield] DataMedicamento
GRID : ID | MECA ID | Fecha Solicitud | Tipo de procedimiento | Solicitado por | Cantidad | Und/Med | Cada | Und/Med | Via deAdministración | Tiempo | Und/Med | Modificado | Suspendido
WINDOW Tratamiento anterior
FIELD[textfield] TextFainIdSoloProcedimiento
FIELD[textfield] TextProcIdSoloProcedimiento
FIELD[textfield] TextPaciIdSoloProcedimiento
GRID : Descripción | Carta
BTN Aceptar
WINDOW Seleccione Tipo Imprecion
WINDOW Descargar Consolidado
FIELD[displayfield] DisplayField2
FIELD[displayfield] DisplayField3
BTN Cerrar
FIELD[displayfield] MECA_CCUM
BTN First Page
BTN Previous Page
BTN Next Page
BTN Last Page
BTN Refresh
GRID : ID | Código | Nombre | Forma farmacéutica | Concentración | Presentación | Cant. Dosis | Posología
BTN Salir
FIELD[displayfield] MsgPrev
FIELD[textfield] Nombre usuario
FIELD[textfield] Contraseña
BTN Continuar
WINDOW Ingresar credenciales
FIELD[combobox] ComboEstadoIngreso
FIELD[datefield] FechaSalidaConfig
FIELD[timefield] HoraSalidaConfig
FIELD[combobox] ComboDestinoMedico
FIELD[combobox] ComboDestinoEnfermera
BTN Cancelar
WINDOW Configurar estados del ingreso
WINDOW Detalle datos del paciente
GRID : Descripción | Prev
WINDOW Ver formatos
FIELD[checkboxfield] Un solo documento
FIELD[checkboxfield] CheckTodoCarta
FIELD[checkboxfield] CheckTodoTirilla
GRID Ítems de impresión: Descripción | Carta | Tirilla
GRID Información de encabezado: Descripción | Selección
FIELD[combobox] Opcion de fecha {RANGO DE FECHAS}
FIELD[datefield] Inicial
FIELD[datefield] Final
FIELD[numberfield] Año
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
BTN Buscar
GRID Impresión para Facturación: Descripción | Ok
WINDOW Imprimir formatos
GRID Ítems de impresión: Descripción | Carta
GRID : Documento | Nombre paciente
WINDOW Coincidencia con el parámetro ingresado
BTN Guardar
WINDOW Formulación
FIELD[displayfield] ctl358
FIELD[textfield] textfield-1253
FIELD[textfield] textfield-1256
FIELD[textfield] textfield-1259
FIELD[textfield] textfield-1262
FIELD[displayfield] ctl381
GRID : ID | Fecha Registro | Profesional quien registra | Destino paciente | Opciones
WINDOW Registros de actividades
FIELD[displayfield] ctl415
FIELD[textfield] textfield-1312
FIELD[textfield] textfield-1315
FIELD[textfield] textfield-1318
FIELD[textfield] textfield-1321
FIELD[displayfield] ctl438
GRID :
WINDOW Incluir en el reporte de epicrisis
FIELD[combobox] Seleccione empresa
FIELD[combobox] Seleccione Contrato
FIELD[textareafield] Motivo
WINDOW Asignar empresa a ingreso
FIELD[displayfield] ctl477
FIELD[textfield] textfield-1353
FIELD[combobox] Especialidad
GRID : MEDICO
WINDOW Seleccionar medicos
TOOLTIP Actualizar
FIELD[combobox] ComboOpcionFechaRG {MES, RANGO DE FECHAS}
FIELD[radiofield] Trimestral
FIELD[radiofield] Mensual
FIELD[radiogroup] radiogroup-1365
FIELD[numberfield] NumberAnoRG
FIELD[combobox] ComboMesRG {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] DateFechaInicialRG
FIELD[datefield] DateFechaFinalRG
BTN Consultar Procedimientos
FIELD[checkboxfield] ZIP
BTN Generar PDF
WINDOW Impresión de procedimientos médicos
FIELD[combobox] ComboOpcionFecha {MES, RANGO DE FECHAS}
FIELD[numberfield] TextAno
FIELD[combobox] ComboMes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] FechaI
FIELD[datefield] FechaF
FIELD[radiofield] Un solo documento
FIELD[radiofield] Documentos individuales
FIELD[radiogroup] radiogroup-1394
FIELD[textfield] TextMedicos
BTN Limpia la selección de los medicos
BTN Selecciona los medicos.
WINDOW Informe corte de larga instancia
FIELD[radiogroup] radiogroup-1404
WINDOW Informe de ingreso
FIELD[textareafield] Motivo de anulación
WINDOW Anular factura
FIELD[displayfield] ctl615
FIELD[textfield] textfield-1415
FIELD[displayfield] ctl623
GRID : Opciones
WINDOW Soportes factura
BTN Group by this field
FIELD[displayfield] ctl637
FIELD[textfield] textfield-1450
FIELD[textfield] textfield-1453
FIELD[textfield] textfield-1456
FIELD[datefield] DateField2
FIELD[displayfield] ctl658
GRID : ID | Número Acta | Ciudad De Entrega | Fecha Entrega | Opciones
WINDOW Soportes Actas de Entrega
FIELD[textfield] Documento/Nombre
FIELD[textfield] TextDocumento
FIELD[textfield] TextNombre
FIELD[textfield] TextGenero
FIELD[textfield] TextFNacimiento
FIELD[textfield] TextEdad
BTN Información paciente
FIELD[combobox] ComboBoxIdEstadoFilter {EN ATENCIÓN, PREFACTURADO, FACTURADO, ATENDIDO, EN TRATAMIENTO}
FIELD[datefield] FechaEntradaFilter
FIELD[datefield] FechaSalidaFilter
FIELD[triggerfield] Especialidad o médico
BTN Generar consolidado de los ingresos
BTN Lista de Anexos
BTN Generar consolidado de Ayudas DX
BTN Generar consolidado de Laboratorios
BTN Generar consolidado de Recomendaciones
BTN Generar consolidado de Remisiones
BTN Generar consolidado de Procedimientos
BTN Generar Ingreso sin Cita
GRID : Id | Estado | Fecha ingreso | Fecha salida
FIELD[triggerfield] TipoProcedimiento
BTN Imprimir
BTN Trazabilidad
BTN Generar reporte de epicrisis
BTN Mas opciones...
BTN Epicrisis
BTN Generar informe de larga instancia
BTN Generar informes de ingreso
BTN Enviar RDA PACIENTE
BTN Enviar RDA CONSULTA EXTERNA
BTN Enviar RDA URGENCIAS
BTN Enviar RDA HOSPITALIZACION
GRID : Impr | Id | Tipo Procedimiento | Estado | Fecha de registro | Opciones
TREE Modulos
PANEL Inicio
BTN Asignar empresa
BTN Configurar estados del ingreso
BTN Eliminar Ingreso
BTN Firmar Ingreso
FIELD[datefield] FechaIngresoIngresoSinCita
FIELD[timefield] HoraIngresoFechaSinCita
FIELD[datefield] FechaSalidaIngresoSinCita
FIELD[timefield] HoraSalidaIngresoSinCita
GRID : Identificador | Numero | Modificado Por | Opciones
WINDOW Ver Folios Anulados
WINDOW Familiograma

## CATALOGO PRINCIPAL > PLANTILLA MEDICAMENTOS (/SUROSFacturacion/Vistas/Privado/Plantillas/PlantillaMedicamentos.aspx)
TITLE 
FIELD[textfield] Nombre de la plantilla:
BTN Add
BTN Eliminar
GRID Lista de medicamentos:: Código | Nombre genérico | Nombre comercial | Forma farmacéutica | Concentración | Valor para EPS
FIELD[textareafield] Observación
BTN Aceptar y guardar
BTN Guardar
BTN Salir
WINDOW Plantilla de medicamentos
FIELD[displayfield] ctl51
FIELD[textfield] textfield-1031
FIELD[textfield] textfield-1034
FIELD[textfield] textfield-1037
FIELD[textfield] textfield-1040
FIELD[textfield] textfield-1043
GRID : CODIGO | NOMBRE GENERICO | NOMBRE COMERCIAL | FORMA | CONCENTRACIÓN
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
FIELD[textfield] textfield-1051
FIELD[textfield] textfield-1054
FIELD[textfield] textfield-1057
FIELD[textfield] textfield-1060
BTN Nueva plantilla de medicamentos
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : Fecha Creación: | Nombre de plantilla: | Activo: | Observación:
BTN Editar

## CATALOGO PRINCIPAL > PLANTILLA INSUMOS (/SUROSFacturacion/Vistas/Privado/Plantillas/PlantillaInsumos.aspx)
TITLE 
FIELD[textfield] Nombre de la plantilla:
BTN Add
BTN Eliminar
GRID Lista de medicamentos:: Descripción: | Unidad de medida | Valor para EPS
FIELD[textareafield] Observación
BTN Aceptar y guardar
BTN Guardar
BTN Salir
WINDOW Plantilla de medicamentos
FIELD[displayfield] ctl45
FIELD[textfield] textfield-1028
FIELD[textfield] textfield-1031
FIELD[textfield] textfield-1034
GRID : CODIGO | NOMBRE | NOMBRE
BTN Aceptar
BTN Cancelar
WINDOW Coincidencia encontrada
FIELD[textfield] textfield-1042
FIELD[textfield] textfield-1045
FIELD[textfield] textfield-1048
FIELD[textfield] textfield-1051
BTN Nueva plantilla de medicamentos
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : Fecha Creación: | Nombre de plantilla: | Activo: | Observación:
BTN Editar

## CATALOGO PRINCIPAL > MEDICAMENTO (/SUROSFacturacion/Vistas/Privado/Medicamentos/Medamento.aspx)
TITLE 
FIELD[textfield] Nombre medicamento:
FIELD[combobox] Es principioActivo {SI, NO}
FIELD[textfield] Codigo DCI
FIELD[textfield] Clave
FIELD[combobox] Activo {SI, NO}
BTN Aceptar y guardar
BTN Guardar
BTN Salir
WINDOW Agregar nombre medicamento
FIELD[textfield] textfield-1017
FIELD[textfield] textfield-1020
BTN Agregar Medicamento
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : Nombre: | Principio Activo:
BTN Editar
BTN Eliminar

## CATALOGO PRINCIPAL > ADMINISTRACIÓN CATALOGO MEDICAMENTOS (/SUROSFacturacion/Vistas/Privado/Medicamentos/AdministracionMedicamentos.aspx)
TITLE 
FIELD[textfield] Código:
FIELD[combobox] Nombre Genérico:
FIELD[combobox] Nombre comercial:
FIELD[combobox] Forma farmacéutica:
FIELD[combobox] Concentracion:
BTN Aceptar y guardar
BTN Guardar
BTN Salir
WINDOW Agregar al catálogo principal
FIELD[textfield] textfield-1019
FIELD[textfield] textfield-1022
FIELD[textfield] textfield-1025
FIELD[textfield] textfield-1028
FIELD[textfield] textfield-1031
FIELD[textfield] textfield-1034
FIELD[textfield] textfield-1037
BTN Agregar al catálogo
BTN Refrescar
BTN Primera página
BTN Página anterior
BTN Página siguiente
BTN Última página
BTN Actualizar
GRID : Fecha Creación | Codigo | Nombre genérico | Nombre comercial | Forma farmacéutica | Concentración | Estado
BTN Editar
BTN Eliminar

## CATALOGO PRINCIPAL > PAGINA WEB (/SUROSPaginaWeb/Vistas/InicioPaginaWeb.aspx)
TITLE SoftProject | CMS
WINDOW Sesión finalizada
TREE TreeMenuOpciones

## CATALOGO PRINCIPAL > AGENDA CONSULTAS TERMINADAS (/SUROSTurnero/Vistas/Privado/Agenda/AgendaConsultasTerminadas.aspx)
TITLE Agenda consulta externa
FIELD[displayfield] ctl03
FIELD[combobox] Asesor
BTN Crear Nuevo
BTN Establecer
WINDOW PUESTO DE ASESOR
FIELD[textfield] Nombre
FIELD[combobox] Sede
BTN Crear
BTN Cancelar
WINDOW CREAR PUESTO
GRID : Descripción | Prev
BTN Aceptar
WINDOW Ver formatos
FIELD[checkboxfield] Un solo documento
FIELD[checkboxfield] CheckTodoCarta
FIELD[checkboxfield] CheckTodoTirilla
GRID Ítems de impresión: Descripción | Carta | Tirilla
WINDOW Imprimir formatos
FIELD[displayfield] ACT_ctl09
FIELD[textfield] textfield-1050
FIELD[textfield] textfield-1053
FIELD[textfield] textfield-1056
FIELD[textfield] textfield-1059
FIELD[textfield] textfield-1062
FIELD[textfield] textfield-1065
FIELD[textfield] textfield-1068
FIELD[displayfield] ACT_ctl47
GRID : ID | Paciente | Documento | Consultorio | Procedimiento Médico | Médico | Fecha
FIELD[netmulticombo] ComboConsultorio
FIELD[combobox] Especialidad
FIELD[displayfield] Asesor
BTN Cerrar Puesto
FIELD[datefield] dd/mm/yyyy
BTN Consultar
BTN Mostrar toda la agenda
BTN Actualiza lista de turnos
BTN Activar
BTN Imprimir Ordenes.
BTN Realizar nuevamente el llamado!
BTN Atendido
BTN No atendio llamado
BTN Activar nuevamente el turno.

## CATALOGO PRINCIPAL > AGENDA HOSPITALIZACIÓN (/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaFacturacionHospitalizacion.aspx)
TITLE Agenda de enfermeria
FIELD[displayfield] ctl55
FIELD[textfield] textfield-1012
FIELD[textfield] textfield-1014
FIELD[textfield] textfield-1016
FIELD[textfield] textfield-1018
FIELD[textfield] textfield-1020
FIELD[textfield] textfield-1022
FIELD[textfield] textfield-1024
FIELD[textfield] textfield-1026
FIELD[textfield] textfield-1028
BTN Ayuda de colores
BTN Mostrar solo salidas del medico
FIELD[combobox] Opción {MES, RANGO DE FECHAS}
FIELD[numberfield] Año
FIELD[combobox] Mes {ENERO, FEBRERO, MARZO, ABRIL, MAYO, JUNIO, JULIO, AGOSTO, SEPTIEMBRE, OCTUBRE, NOVIEMBRE, DICIEMBRE}
FIELD[datefield] Fec. Inicial
FIELD[datefield] Fec. Final
FIELD[combobox] Empresa {TODAS, ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I}
FIELD[combobox] Tipo {PDF, EXCEL}
BTN Generar Reporte
BTN Reporte Instancia
BTN Actualiza agenda de enfermeria
GRID : Fecha ingreso | Cama | Tipo Doc | Documento | Nombre Paciente | EPS | Nota de ingreso | Observación de ingreso | Caso especial

## CATALOGO PRINCIPAL > TICKETS (/SurosTickets/Vistas/Ticket.aspx)
TITLE Soporte de Ayuda SoftProject
PANEL Soporte de Ayuda SoftProject

## CATALOGO PRINCIPAL > ATENCIÓN AL USUARIO (/SUROSTurnero/Vistas/Privado/Agenda/AgendaServicios.aspx)
TITLE Agenda consulta externa
FIELD[displayfield] ctl03
FIELD[combobox] Asesor
BTN Establecer
BTN Cancelar
WINDOW PUESTO DE ASESOR
GRID : ID | Instancia | Sigla | Turno | Hora | Asistio | No atendio el llamado | Metodo | Puesto
FIELD[netmulticombo] ComboPuesto
FIELD[displayfield] Asesor
BTN Cerrar Puesto
FIELD[datefield] dd/mm/yyyy
BTN Consultar
BTN Mostrar toda la agenda
BTN Actualiza lista de turnos
BTN Ordenar en forma ascendente
BTN Ordenar en forma descendente
BTN Columnas
BTN Group by this field

## CATALOGO PRINCIPAL > PUNTO DE VENTA (http://puntoventa.suros.co/Vista/Privado/Inicio.aspx)
ERR Failed to read a named property 'Ext' from 'Window': Blocked a frame with origin "http://prored.suros.co" from accessing a cross-origin frame.

## CATALOGO PRINCIPAL > PUNTO LOCAL (http://localhost:61167/Vista/Privado/Inicio.aspx)
ERR Failed to read a named property 'Ext' from 'Window': Blocked a frame with origin "http://prored.suros.co" from accessing a cross-origin frame.