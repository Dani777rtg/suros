# Historia clínica y atención

Módulo `SUROSHistoriaClinica` (ASP.NET + Ext.NET). Base de rutas: `/SUROSHistoriaClinica/Vistas/Privado/`. Fuente: extracción de UI (solo observación, sin datos de paciente). Se documentan 24 pantallas (home + 23 del árbol por especialidad). Las pantallas compartidas (agenda médica, historia clínica de consulta externa) se extrajeron una vez; el árbol indica qué áreas las usan.

## Resumen

El módulo es **agenda-céntrico**: cada área de atención carga un árbol de menú (`ListaArbol(id)`) cuyas hojas son agendas (listas de pacientes/ingresos) desde las que se abre el formulario clínico del encuentro. Tres familias de pantalla:

1. **Agendas** (consulta externa, urgencia, enfermería, evolución médica, cirugía, PyP, procedimientos externos): grid de pacientes + filtros + acciones (atender, inasistencia, dar salida, soltar).
2. **Formularios clínicos** (`ConsultaExterna.aspx`, `HistoriaUrgencia.aspx`, `Triage.aspx`): anamnesis, antecedentes estructurados (Res. 1888/2025, RDA), signos vitales, examen, diagnóstico CIE-10, conducta/destino.
3. **Soporte**: entrega de turno, laboratorio clínico, inicio de historia (home por paciente con ingresos, procedimientos, trazabilidad, epicrisis, despacho de suministros).

## Mapa de áreas de atención

| Área (id) | Pantallas que usa |
|---|---|
| Agenda de urgencia (#548) | Agenda Urgencia |
| Medicina general (#157, #172) | Agenda médica, Historia clínica (consulta externa); #157 además Atención laboratorio clínico |
| Atención de urgencia (#158) – Enfermería | Agenda procedimiento enfermería, Cirugía urgenciada, Cirugía programada, Entrega de turno enfermería, Agenda hospitalización, Agenda observación |
| Atención de urgencia (#158) – Médico | Agenda evolución hospitalización, evolución observación, Nota quirúrgica, Agenda urgencia, Historia urgencia, Triage, Entrega de turno médico |
| Enfermería (#559) / Médico (#560) | Mismas hojas que las ramas homónimas de #158 (acceso directo por rol) |
| Odontología (#160): Cirugía maxilofacial #179, Endodoncia #180, Higiene oral #178, Odontología general #177 | Sin hojas extraídas; el triage puede enviar a "Odontología general" |
| Apoyo terapéutico (#161): Fonoaudiología #181, Optometría #164, Psicología #166 (subgrupo "Grupo cuatro"), Terapia física #169, ocupacional #165, respiratoria #168 | Sin hojas extraídas |
| Medicina especializada (#162): Anestesia #190, Dermatología #188, Ginecobstetricia #183, Nutrición #167, Oftalmología #187, Ortopedia #185, Pediatría #184 | Sin hojas extraídas (inferido: usarían Agenda médica + Historia clínica compartidas; no verificado) |
| PyP (#1357) | Agenda afinamiento #1358, Agenda de crónicos #1362, Agenda preingreso #1360, Agenda de PyP #1415, Afinamientos y preingresos #1367 |
| Laboratorio clínico (#1701) | Atención laboratorio clínico |
| Procedimientos externos (#2454) | Agenda procedimientos externos |

El botón "Partograma" en Agenda Urgencia implica un formulario obstétrico no extraído.

## Elementos comunes a las agendas

- Filtro por fecha (`dd/mm/yyyy`) y botones "Mostrar toda la agenda" / "Actualizar lista".
- **Nota de inasistencia** (ventana con justificación): marca la cita como inasistente.
- Ventanas **Detalle datos del paciente** e **Información del acudiente**.
- **Citas pendientes por definir** (cierre de agenda): "VER EL DETALLE DE LAS CITAS PENDIENTES" / "MARCAR TODAS LAS CITAS COMO INASISTENCIA", con nota.
- Grid con ordenar, columnas y agrupar por campo.

---

## Agenda de urgencia > Agenda Urgencia
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaConsultaUrgencia.aspx` (también bajo Atención de urgencia > Médico > Consulta de urgencia)

- **Propósito**: lista de pacientes ingresados a urgencias que esperan o están en atención médica.
- **Funcionalidades**: El usuario puede filtrar por ID, estado de ingreso, fecha de registro, documento, paciente, empresa, observación, modo de ingreso, médico y rango de fechas; mostrar toda la agenda; "Soltar paciente" (liberar la atención, con observación de la actividad); "No continuar con la atención" (nota de inasistencia); abrir Partograma; ver detalle del paciente y del acudiente.
- **Datos**: Observación de la actividad; justificación de inasistencia.
- **Listados**: Agenda: ID | Clasificación | Fecha-Hora | Documento | Nombre paciente | EPS ingreso | Observación ingreso | Modo ingreso | Médico | Estado.
- **Flujos y reglas**: "Clasificación" es la prioridad del triage (inferido). "Soltar" devuelve el paciente a la cola para que otro médico lo tome (inferido).

## Medicina general > Atención laboratorio clínico
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Laboratorios/LaboratorioClinicoAtencion.aspx`

- **Propósito**: ciclo del laboratorio: toma de muestra, código de barras, registro de resultados y entrega al paciente.
- **Funcionalidades**: El usuario puede buscar paciente por documento/nombre o por código de barras (con empresa); listar por estado de cita y mes o rango de fechas (botón HOY), exportar XLS y generar reporte; ver estudios solicitados; registrar **toma de muestra** (genera código de barras); adjuntar archivos; **registrar resultados**; imprimir seleccionados; **entregar resultado** (a quién: el mismo paciente u otra persona con parentesco); anular estudio (con motivo); eliminar turno de urgencia; marcar inasistencia; ver datos de la solicitud (orden médica, HC de solicitud, especialidad, profesional que solicita); reautenticar con usuario/contraseña.
- **Datos**:
  - Toma de muestra: fecha/hora ingreso y salida, fecha, hora, "Nueva toma", Proceso a seguir {ENVIAR A LABORATORIO, ENVIAR Y RECIBIR EN LABORATORIO, ENVIAR A LABORATORIO EXTERNO}, Tipo tapa/envase {TAPA ROJA, NARANJA, AMARILLA, CELESTE, LILA, VERDE, NEGRA, GRIS, FRASCO PARA RECOLECTOR DE ORINA, FRASCO RECOLECTOR MATERIA FECAL, VIAL RECOLECTOR MUESTRA VAGINAL (FROTIS VAGINAL), LAMINA RECOLECTORA PARA CITOLOGIA}, Convenio, Responsable de toma, Hora de toma, Observación, Observación de anulación.
  - Entrega de resultados: Documento*, Nombre*, Parentesco.
  - Filtros: Estado cita {TODOS, ASIGNADO, TOMA DE MUESTRA REALIZADA, TOMA DE MUESTRA PARCIAL, REGISTRO DE RESULTADO REALIZADO, REGISTRO DE RESULTADO PARCIAL, CON RESULTADOS COMPLETOS, RESULTADOS ENTREGADOS, ANULADO, RECHAZADO}; Empresa {PRORED Florencia-Caquetá, Cauca, Pasto-Nariño, Risaralda}; Opción de fecha {MES, RANGO DE FECHAS}.
- **Listados**: Lista de pacientes: ID | Estado laboratorio | No. autorización | Datos asignación de turno | Datos del paciente | Datos facturación | Opciones. Estudios solicitados: PRPOID | Estado | Acción | No. autorización | Código de barra | Procedimiento | No. laboratorio | Datos adicionales | Estudio de laboratorio | Muestra realizada | Observaciones | Opciones. Resultados: Descripción | Fecha registro | Unidad/Medida | V. mínimo | V. máximo. Archivos: Nombre | Tamaño | Observación. Coincidencias: Documento | Nombre. Otra: Estado lab | Fecha creación | Código de barras | Sede | N.º impresión | Fecha/Entrega a. Estancia.
- **Flujos y reglas**: Asignado → toma de muestra (parcial/realizada) → registro de resultado (parcial/completo) → resultados entregados; anulado/rechazado terminales (inferido). La orden proviene de una orden médica de la HC (inferido). Rangos mín/máx sirven para marcar valores alterados (inferido).

## Medicina general > Agenda médica
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaConsultaExterna.aspx` (Medicina general #157/#172; otras especialidades inferido)

- **Propósito**: agenda diaria de consulta externa del profesional.
- **Funcionalidades**: El usuario puede elegir fecha, mostrar toda la agenda, actualizar lista, ver detalle del paciente y acudiente, ver procedimientos de la cita, registrar inasistencia y cerrar agenda (ver pendientes / marcar todas como inasistencia).
- **Datos**: ventana Procedimientos: Código | Descripción | Cantidad | Observación.
- **Listados**: Jornada | ID | Turno | Hora | Documento | Nombre paciente | EPS | Régimen | Acudiente | Estado.
- **Flujos y reglas**: seleccionar una cita abre `ConsultaExterna.aspx` (inferido). "Jornada" = mañana/tarde (inferido).

## Medicina general > Historia clínica (consulta externa)
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/ConsultaExterna.aspx`

- **Propósito**: historia clínica de consulta externa (Res. 1995/1999) con antecedentes estructurados conforme a Res. 1888/2025 (RDA, Resumen Digital de Atención).
- **Funcionalidades**: El usuario puede consultar historias anteriores e ingresos; registrar motivo y enfermedad actual; gestionar antecedentes por tipo; revisión por sistemas, signos vitales, examen físico y mental; riesgo cardiovascular (Framingham/Wilson); diagnósticos CIE-10; resultados de ayudas diagnósticas; recomendaciones; conducta; nota aclaratoria; destino; **plantillas personales** (nueva, editar, eliminar, cargar, guardar ítems); adjuntar archivos; "Realizar formato procedimientos"; "Actualizar formatos"; enviar **RDA al Ministerio**; "Enviar al final de la agenda"; guardar historia.
- **Datos**:
  - Encabezado: No. de historia, fecha, paciente, médico, fecha/hora ingreso y salida, Causa externa (catálogo abajo), Sintomático respiratorio {SI, NO}, Gestante {SI, NO}.
  - Anamnesis: fecha, hora, motivo de consulta, enfermedad actual.
  - Antecedentes (cada uno con ventana de alta y lista "Registros actuales", editar/eliminar):
    - Alérgicos: tipo de alergia, medicamento (búsqueda con principio activo), descripción, estado, reacción.
    - Patológicos personales: patología CIE-10/11, año, tratamiento actual, condición.
    - No patológicos: Tabaquismo {Nunca, Ex, Activo}, Alcohol {No, Social, Frecuente}, SPA {Sí/No} + observaciones, Actividad física {Sedentario, Moderada, Activa}.
    - Quirúrgicos: procedimiento CUPS, año, complicaciones {No, Sí} + observación.
    - Farmacológicos: medicamento, uso actual, dosis.
    - Familiares patológicos: patología CIE-10/11, parentesco.
    - Ginecológicos: menarquia, FUM, anticoncepción {Ninguna, DIU, Implante subdérmico, Oral, Preservativo, Inyección, Otro}, ciclo menstrual {Regular, Irregular, N/A}, citología vigente, menopausia.
    - Obstétricos: gestaciones, partos, abortos, cesáreas, ectópicos, mortinatos, vivos, muertos.
    - Nacimiento: edad gestacional, peso, talla, APGAR 1 y 5 min, tamizaje neonatal {Normal, Alterado, Pendiente}; condición al nacer: llanto inmediato, reanimación, hospitalización neonatal {Sí/No}, complicaciones (dificultad respiratoria, ictericia, sepsis, hipoglucemia, otra), alimentación inicial {Materna, Mixta, Artificial}, inicio de lactancia {<1 hora, 1 hora, no recibió}.
    - Vacunas: vacuna (catálogo código/nombre), fecha de aplicación, dosis {Única, Primera, Segunda, Tercera, Refuerzo, Booster}, estado {Completada, Pendiente, No aplica}, lote, proveedor, laboratorio.
    - Antecedente genérico (descripción libre); grilla "Antecedentes Res. 1888 (RDA)": Antecedente | Descripción | Acciones; ventana de antecedentes clínicos anteriores a la Res. 1888/2025 (consulta).
    - Factores de riesgo: tipo {QUÍMICOS, BIOLÓGICOS, BIOMECÁNICOS, FÍSICOS, OTRO}, descripción, estado {MODIFICADO, CORREGIDO, FINAL, INGRESADO EN ERROR, PRELIMINAR, CANCELADO, REGISTRADO, DESCONOCIDO}.
  - Revisión por sistema (texto por sistema, botón "Marcar normal"): cabeza, ojos, nariz, oídos, orofaringe, cuello, respiratorio, neurológico, endocrino, músculo-esquelético, hematopoyético, linforreticular, psiquiátrico, piel, cardiovascular, gastrointestinal, ginecológico, urológico, otros.
  - Signos vitales: TA (sistólica/diastólica), check "tratamiento para tensión arterial", FC, FR, SatO2, glucometría, temperatura, peso, talla, IMC, superficie corporal (m2), perímetro encefálico, perímetro de cintura; indicadores calculados de peso y riesgo.
  - Examen físico (texto): aspecto general, tórax, pulmonar, perfusión, abdomen, extremidades, genitourinario, neurológico, observaciones.
  - Examen mental: conciencia, lenguaje, orientación, sensopercepción, atención, memoria, inteligencia, afecto, ánimo, pensamiento, juicio, conducta, introspección, prospección.
  - Riesgo cardiovascular (Framingham/Wilson, "Test de Framsky Green Levine"): fecha inicio/fin, puntaje total, % riesgo, nivel de riesgo.
  - Diagnóstico: búsqueda CIE-10, tipo {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESION DIAGNOSTICA}, observación.
  - Cierre: Recomendaciones, Resultado de ayuda DX (adjuntos), Conducta general, Nota aclaratoria, Destino {SALIDA, INICIAR TRATAMIENTO, HOSPITALIZACIÓN, CIRUGÍA, SALIDA POR REFERENCIA Y CONTRAREFERENCIA}.
  - Envío RDA: ventana con ayuda y grilla de resultados.
- **Listados**: Historias previas por ingreso; Antecedentes: Antecedente | Descripción; Plantillas: Descripción; Diagnósticos: Código | Descripción | Prioridad; coincidencias CIE-10: Código | Descripción; envío RDA: Tipo | Estado | Detalle | Hora.
- **Flujos y reglas**: el destino determina el paso siguiente: hospitalización/cirugía generan ingreso a esas agendas, referencia genera formato de remisión (inferido). Los botones REALIZAR HISTORIA CONSULTA EXTERNA / REALIZAR FORMATO PROCEDIMIENTOS (ventana "Opciones") eligen el tipo de formato (inferido). Órdenes, fórmulas e interconsultas no aparecen aquí; probablemente se abren desde "Actualizar formatos" (inferido).

Catálogo **Causa externa** (RIPS, 27 valores): accidente de trabajo; lesión por agresión; lesión autoinfligida; enfermedad general; sospecha de violencia sexual; otro tipo de accidente; accidente en el hogar; accidente de tránsito de origen común; enfermedad laboral; intervención colectiva; atención de población materno perinatal; riesgo ambiental; otros eventos catastróficos; accidente de mina antipersonal (MAP); artefacto explosivo improvisado (AEI); munición sin explotar (MUSE); otra víctima del conflicto armado; promoción y mantenimiento de la salud (intervenciones individuales); accidente de tránsito de origen laboral; evento catastrófico de origen natural; sospecha de violencia física; sospecha de violencia psicológica; sospecha de negligencia y abandono; IVE por peligro a la salud o vida de la mujer; IVE por malformación incompatible con la vida; IVE por violencia sexual/incesto/inseminación no consentida; evento adverso en salud; accidente en el entorno educativo.

## Atención de urgencia > Enfermería > Agenda procedimiento enfermería
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Urgencia/AgendaProcedimientosEnfermeria.aspx`

- **Propósito**: lista de pacientes de urgencias con procedimientos de enfermería.
- **Funcionalidades**: El usuario puede actualizar la agenda, dar salida al paciente y marcar inasistencia con nota.
- **Listados**: Fecha ingreso | Tipo doc | Documento | Nombre paciente | EPS.

## Atención de urgencia > Enfermería > Cirugía > Agenda cirugía urgenciada
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaCirugiaUrgenciada.aspx`

- Página sin componentes extraídos (título vacío). Propósito (inferido): pacientes en cirugía de urgencia para enfermería. Por verificar.

## Atención de urgencia > Enfermería > Cirugía > Agenda enfermería cirugía programada
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaCirugiaProgramada.aspx`

- **Propósito**: agenda de enfermería de pacientes con cirugía programada.
- **Funcionalidades**: El usuario puede filtrar por fecha, actualizar, dar salida al paciente, **cambiar estancia/destino del paciente** (ventana "CAMBIAR DESTINO PACIENTE", combo Destino) y registrar inasistencia.
- **Listados**: Jornada | Hora | Fecha ingreso institución | Fecha ingreso estancia | Fecha última evolución | Documento | Nombre paciente | Procedimiento | EPS | Acudiente | Médico | Estado.

## Atención de urgencia > Enfermería > Entrega de turno enfermería
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/EntregaTurno/EntregaTurnoEnfermera.aspx`

- **Propósito**: relevo de turno entre enfermeras por instancia.
- **Funcionalidades**: El usuario puede elegir instancia {OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA}, generar o cargar la lista de pacientes (selección por habitación, seleccionar todo/limpiar), anotar por paciente observación y pendientes, registrar nota general, **entregar turno**, **recibir turno** (credenciales de quien recibe; check "También recibo el turno"; fecha/hora de registro), editar observación, eliminar, ver detalle, exportar PDF.
- **Listados**: Turno actual: Cama | Nombre paciente | Edad | Especialidad | Diagnóstico | Observación | Pendientes/Observación. Historial: Fecha | Enfermera(o) entrega | Enfermera(o) recibe | Instancia | Cantidad | Nota. Selección: Paciente | Cama.
- **Flujos y reglas**: la entrega queda pendiente hasta que otro usuario la recibe con su clave (inferido).

## Atención de urgencia > Enfermería > Hospitalización > Agenda hospitalización
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaHospitalizacion.aspx`

- Solo título "Agenda Enfermería Hospitalización"; sin componentes extraídos. Propósito (inferido): pacientes hospitalizados para registros de enfermería.

## Atención de urgencia > Enfermería > Observación > Agenda de observación
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaObservacion.aspx`

- Mismo caso para pacientes en observación (el título extraído repite "Hospitalización"). Por verificar.

## Atención de urgencia > Médico > Agenda de hospitalización médico
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionHospitalizacion.aspx`

- Solo título "Agenda Evolución Hospitalización". Propósito (inferido): evolución médica diaria de hospitalizados.

## Atención de urgencia > Médico > Agenda de observación médico
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionObservacion.aspx`

- Solo título "Agenda Evolucion Observación". Propósito (inferido): evolución médica de pacientes en observación.

## Atención de urgencia > Médico > Cirugía > Agenda nota quirúrgica
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaCirugia.aspx`

- Solo título "Agenda cirugia". Propósito (inferido): pacientes de cirugía de urgencia para registrar la nota quirúrgica.

## Atención de urgencia > Médico > Consulta de urgencia > Historia urgencia
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/HistoriaUrgencia.aspx`

- **Propósito**: historia clínica de la atención médica de urgencias.
- **Funcionalidades**: El usuario puede registrar el formato de ingreso (nota de ingreso, caso especial, observación), motivo, causa externa, enfermedad actual, antecedentes (mismos paneles que consulta externa, más "Cargar otros antecedentes (V1)" y ver versión anterior), signos vitales, examen físico, resultados de ayudas DX, conducta, diagnósticos, destino y referencia/contrarreferencia, plantillas, adjuntos, visor y envío de RDA al Ministerio, enviar al final de la agenda.
- **Datos** (diferencias frente a consulta externa):
  - Caso especial {NINGUNA, EMBARAZO, DISCAPACITADOS, ALERGIAS, ENFERMEDAD MENTAL}.
  - Examen físico por segmentos con "Marcar normal": aspecto general, cabeza, ojos, oídos, nariz, orofaringe, cuello, tórax, pulmonar, cardiovascular, perfusión, abdomen, extremidades, genitourinario, neurológico, piel, observaciones.
  - Signos vitales como en consulta externa, sin perímetro de cintura ni perímetro encefálico adicional de cintura.
  - Antecedente de vacuna de fiebre amarilla: "Aplicación fiebre amarilla" {SI, NO}.
  - Donación de órganos: Donante detectado {SI, NO}, Voluntad anticipada {SI, NO}, Nota.
  - Diagnóstico: CIE-10, tipo de diagnóstico, prioridad, observación.
  - Destino {SALIDA, OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA, MORGUE, SALIDA POR REFERENCIA Y CONTRAREFERENCIA, RETIRO VOLUNTARIO, FUGA}; botones Editar destino y Editar referencia y contrarreferencia (pregunta SI/NO).
  - Botones GUARDAR CONSULTA DE URGENCIA, Actualizar formatos.
- **Listados**: Antecedentes; Diagnósticos: Código | Descripción | Prioridad; envío RDA: Tipo | Estado | Detalle | Hora.
- **Flujos y reglas (inferido)**: destino OBSERVACIÓN/HOSPITALIZACIÓN/CIRUGIA mueve al paciente a las agendas respectivas; MORGUE implica defunción; RETIRO VOLUNTARIO y FUGA cierran el ingreso sin alta médica.

## Atención de urgencia > Médico > Consulta de urgencia > Triage
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Triage.aspx`

- **Propósito**: clasificación de prioridad al ingreso a urgencias (5 niveles).
- **Funcionalidades**: El usuario puede registrar signos vitales, Glasgow, anamnesis breve, información femenina (embarazo/obstétrico), reingreso, alergias a medicamentos, antecedentes, causa externa, estado de ingreso, clasificar, definir el estado de atención y asignar médico; ver ingresos previos.
- **Datos**:
  - Signos vitales: TA, FC, FR, SatO2, glucometría, fetocardia, temperatura, peso, talla, IMC, m2.
  - Glasgow: apertura ocular (combo), respuesta verbal {ORIENTADO, DESORIENTADO O CONFUSO, PALABRAS INAPROPIADAS, SONIDOS INCOMPRENSIBLES, NINGUNA}, respuesta motora {OBEDECE ORDENES VERBALES, LOCALIZA EL DOLOR, RETIRADA ANTE ESTIMULO DOLOROSO, FLEXION AL DOLOR, EXTENSION AL DOLOR, NO HAY RESPUESTA}, puntaje total.
  - Anamnesis: motivo de consulta, enfermedad actual, observación.
  - Información femenina: Aplica {SI, NO}, fecha, semanas de embarazo, embarazo {SI, NO, NO SABE}, días de posparto, triage obstétrico, fecha probable de parto.
  - Alérgico a medicamentos: búsqueda por código CUM/nombre; grilla Medicamento | Fecha registro.
  - Reingreso {SI, NO} + fecha; ingresos previos: Fecha ingreso | Fecha egreso | Diagnóstico de egreso | Médico que atiende.
  - Información general: Causa externa (mismo catálogo), Estado de ingreso {CONSCIENTE, INCONSCIENTE, MUERTO}, Clasificación urgencia {PRIORIDAD I, II, III, IV, V}, Definir estado de atención {CONTINUAR CON LA ATENCIÓN DE URGENCIA; TERMINAR ATENCIÓN DE URGENCIA; TERMINAR Y ENVIAR A CONSULTA EXTERNA; TERMINAR Y ENVIAR A ODONTOLOGÍA GENERAL}.
- **Flujos y reglas (inferido)**: prioridades bajas pueden derivarse a consulta externa u odontología sin pasar por urgencias; "Continuar" deja el ingreso en la agenda de urgencia con su prioridad.

## Atención de urgencia > Médico > Entrega de turno
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/EntregaTurno/EntregaTurnoMedico.aspx`

- **Propósito**: relevo de turno médico por instancia {OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA}.
- **Funcionalidades**: igual a la de enfermería: seleccionar pacientes por habitación, notas, entregar/recibir con credenciales, editar observación, eliminar, ver detalle.
- **Listados**: Cama | Nombre paciente | Diagnóstico | Pendientes/Observación; historial: Fecha | Médico entrega | Médico recibe | Instancia | Cantidad | Nota.

## PyP > Agenda afinamiento
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaAfinamiento.aspx`

- **Propósito**: agenda de enfermería del "afinamiento" (valoración de ingreso a programas de salud pública, inferido).
- **Funcionalidades**: El usuario puede ir a actividades de enfermería en PyP, abrir la historia inicial de afinamiento, ver las que esperan aprobación del médico, marcar inasistencia y cerrar agenda.
- **Listados**: Jornada | Turno | Hora | Documento | Nombre paciente | EPS | Régimen | Acudiente | Estado | Aprobado.
- **Flujos y reglas (inferido)**: enfermería realiza el afinamiento; el médico lo aprueba (columna Aprobado).

## PyP > Agenda de crónicos > Agenda salud pública
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionCronicos.aspx`

- **Propósito**: seguimiento médico de pacientes crónicos de programas.
- **Funcionalidades**: El usuario puede filtrar por fecha, mostrar toda la agenda y actualizar.
- **Listados**: Fecha-hora ingreso | Tipo doc | Documento | Nombre paciente | EPS | Médico que atendió | Estado.

## PyP > Agenda preingreso
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaNotaBasicaProgramasEspeciales.aspx`

- **Propósito**: agenda de enfermería de nota básica de programas especiales (preingreso).
- **Funcionalidades**: las comunes de agenda (fecha, inasistencia, cierre).
- **Listados**: Jornada | Turno | Hora | Documento | Nombre paciente | EPS | Régimen | Acudiente | Estado.

## PyP > Agenda de PyP
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaConsultaExternaPyP.aspx`

- **Propósito**: agenda de consulta externa de promoción y prevención.
- **Listados**: Jornada | Turno | Hora | Documento | Nombre paciente | Ciclo RPMS | EPS | Régimen | Acudiente | Estado. "Ciclo RPMS" se relaciona con las rutas integrales (RIAS/Res. 3280) (inferido).

## PyP > Afinamientos y preingresos > Afinamientos
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaAfinamiento.aspx`

- **Propósito**: revisión médica para aprobar o no el ingreso del paciente a un programa de salud pública.
- **Funcionalidades**: El usuario puede ver el consolidado de actividades, **clasificar al paciente al programa** (ventana: "Aprueba al programa" / "No aprueba al programa" + nota), marcar inasistencia, paginar.
- **Listados**: Fecha inicio | Fecha inicio | Fecha fin | Género | Edad | Documento | Nombre paciente | EPS | Estado atención | No. de muestras | Destino | Aprobado por | Fecha aprobación.

## PyP > Afinamientos y preingresos > Preingresos
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaPreingreso.aspx`

- Idéntica a Afinamientos (mismos botones, ventanas y columnas) para el flujo de preingreso.

## Procedimientos externos > Agenda procedimientos externos
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/AgendaProcedimientosExternos.aspx`

- **Propósito**: agenda de procedimientos fuera de la consulta ordinaria (inferido).
- **Funcionalidades**: El usuario puede filtrar por fecha, mostrar toda, actualizar y marcar inasistencia con nota.
- **Listados**: Turno | Sede atención | Fecha ingreso | Tipo doc | Documento | Nombre paciente | Tipo procedimiento | Procedimientos | Profesional tratante | Estado | EPS.

## Historia clínica > Inicio historia clínica
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/InicioHistoria.aspx`

- **Propósito**: vista central por paciente: buscar, ver ingresos y procedimientos/formatos de cada ingreso, trazabilidad, epicrisis, informes y despacho de suministros de enfermería.
- **Funcionalidades**:
  - Buscar paciente por documento/nombre (ventana de coincidencias) y ver datos básicos (documento, nombre, género, fecha de nacimiento, edad; "Información paciente").
  - Filtrar ingresos por estado {EN ATENCIÓN, PREFACTURADO, FACTURADO, ATENDIDO, EN TRATAMIENTO}, fecha de entrada/salida y especialidad o médico.
  - Sobre un ingreso: **Generar ingreso sin cita** (fecha/hora de ingreso y salida), asignar empresa (empresa, contrato, motivo), configurar estados del ingreso (estado, fecha/hora de salida, destino médico, destino enfermera), eliminar ingreso, **firmar ingreso**.
  - Listar procedimientos/formatos del ingreso por tipo; imprimir (Carta o Tirilla, un solo documento o individuales, ítems de encabezado, impresión para facturación, por mes/rango), **Trazabilidad**, **Epicrisis** y reporte de epicrisis (ventana "Incluir en el reporte de epicrisis"), informe de larga instancia, informes de ingreso.
  - Generar consolidados: ingresos, ayudas DX, laboratorios, recomendaciones, remisiones, procedimientos; lista de anexos.
  - Impresión de procedimientos médicos por mes/trimestre/rango y selección de médicos; salida ZIP o PDF.
  - **Enviar RDA**: paciente, consulta externa, urgencias, hospitalización.
  - Ver folios anulados, Familiograma, Soportes de factura (y anular factura con motivo), Soportes de actas de entrega, Formulación, Registros de actividades, Tratamiento anterior.
  - **Despacho de suministros desde enfermería**: credenciales con CONECTAR/VALIDAR; solicitudes; almacén de stock; Finalizar.
- **Listados**:
  - Ingresos: Id | Estado | Fecha ingreso | Fecha salida.
  - Procedimientos: Impr | Id | Tipo procedimiento | Estado | Fecha de registro | Opciones.
  - Suministros solicitados: Tipo | Código | Suministro | Solicitada | Entregada.
  - Inventario: Cant. entrega | Item | Presentación | Lote | Fecha venc. | Cant. actual | Cant. descargada | Cant. almacenada.
  - Medicamentos del despacho: ID | MECA ID | Fecha solicitud | Tipo de procedimiento | Solicitado por | Cantidad | Und/Med | Cada | Und/Med | Vía de administración | Tiempo | Und/Med | Modificado | Suspendido.
  - Consolidado de medicamentos: ID | Código | Nombre | Forma farmacéutica | Concentración | Presentación | Cant. dosis | Posología.
  - Registros de actividades: ID | Fecha registro | Profesional que registra | Destino paciente | Opciones.
  - Actas de entrega: ID | Número acta | Ciudad de entrega | Fecha entrega | Opciones.
  - Folios anulados: Identificador | Número | Modificado por | Opciones.
  - Impresión: Ítems de impresión: Descripción | Carta | Tirilla; Información de encabezado: Descripción | Selección.
  - Árbol "Modulos" y panel "Inicio".
- **Flujos y reglas (inferido)**: la reautenticación (usuario/clave) protege firma, despacho y entrega de turno. El ingreso progresa EN ATENCIÓN → ATENDIDO/EN TRATAMIENTO → PREFACTURADO → FACTURADO. Anular factura exige motivo.

---

## Flujo de atención (inferido)

1. **Cita / ingreso**: consulta externa nace de cita asignada (agenda médica); urgencias, de ingreso directo (también existe "Generar ingreso sin cita"). Se asignan empresa/EPS y contrato al ingreso.
2. **Triage** (urgencias): signos vitales, Glasgow, prioridad I-V, estado de ingreso; define seguir en urgencias o derivar a consulta externa/odontología.
3. **Atención médica**: Historia urgencia o Historia consulta externa (anamnesis, antecedentes RDA, examen, ayudas DX).
4. **Diagnósticos** CIE-10 (confirmado nuevo/repetido, impresión diagnóstica) con prioridad.
5. **Órdenes / fórmulas / interconsultas**: laboratorio (agenda de laboratorio), procedimientos CUPS, formulación, remisiones. Los consolidados e informes del Inicio historia lo sugieren; los formularios no se observaron.
6. **Destino**: salida, tratamiento, observación, hospitalización, cirugía, referencia/contrarreferencia, morgue, retiro voluntario, fuga.
7. **Enfermería**: agendas por instancia, procedimientos, administración y despacho de suministros; entrega de turno enfermería y médica.
8. **Evolución médica** en observación/hospitalización; nota quirúrgica en cirugía.
9. **Egreso**: configurar estados del ingreso, epicrisis, firma del ingreso, informes.
10. **Reporte**: envío de RDA al Ministerio; RIPS con causa externa y diagnósticos.
11. **Facturación**: prefacturado → facturado, soportes de factura, anulación con motivo.

## Entidades y estados

- **Paciente**, **Acudiente**, **Ingreso** (EN ATENCIÓN, PREFACTURADO, FACTURADO, ATENDIDO, EN TRATAMIENTO), **Estancia** (observación/hospitalización/cirugía), **Cita/turno** (jornada, turno, hora; estados con inasistencia).
- **Historia clínica / folio** (folios anulables), **Antecedente** (alérgico, patológico, no patológico, quirúrgico, farmacológico, familiar, ginecológico, obstétrico, nacimiento, vacuna, factor de riesgo), **Signos vitales**, **Diagnóstico** (CIE-10), **Procedimiento** (CUPS), **Medicamento** (CUM, principio activo).
- **Orden médica**, **Estudio de laboratorio** (estados: ASIGNADO, TOMA DE MUESTRA REALIZADA/PARCIAL, REGISTRO DE RESULTADO REALIZADO/PARCIAL, CON RESULTADOS COMPLETOS, RESULTADOS ENTREGADOS, ANULADO, RECHAZADO), **Muestra** (código de barras, tipo de envase).
- **Entrega de turno** (entrega/recibe, instancia), **Plantilla** personal, **Triage** (prioridad I-V, Glasgow), **Afinamiento/Preingreso** (aprueba / no aprueba), **Ciclo RPMS**, **RDA** (tipo, estado, detalle, hora), **Epicrisis**, **Despacho de suministros** (solicitado/entregado, lote, vencimiento), **Factura** (anulable con motivo), **Acta de entrega**.

## Limitación

Los formularios clínicos reales solo se abren desde un encuentro con paciente real, lo cual no se hizo (solo observación, sin datos de paciente). Lo que la UI implica que existe y no se vio:

- Formato de procedimientos, formato de ingreso, nota de evolución (observación/hospitalización), nota quirúrgica, partograma, notas de enfermería (agendas de hospitalización/observación/cirugía), actividades de enfermería en PyP, historia inicial de afinamiento, nota básica de programas especiales.
- Formulación médica, órdenes de laboratorio/ayudas diagnósticas, remisiones y referencia/contrarreferencia, recomendaciones, epicrisis, informes de ingreso y de larga instancia, familiograma.
- Las agendas de hospitalización, observación, cirugía y nota quirúrgica llegaron sin componentes (el contenido probablemente se carga por código).
- Las ramas de odontología, apoyo terapéutico y medicina especializada no tienen hojas extraídas; se desconoce qué formulario usa cada una.

## Preguntas abiertas

1. ¿Qué formularios clínicos concretos abren odontología, apoyo terapéutico y especializada, y cómo se configuran por especialidad?
2. ¿Cómo se generan y gestionan órdenes médicas (laboratorio, imágenes, procedimientos CUPS), formulación, interconsultas y remisiones, y cuál es su ciclo de estados?
3. ¿Qué contienen las agendas de hospitalización, observación, cirugía y nota quirúrgica (evoluciones, notas de enfermería, administración de medicamentos, balance de líquidos)?
4. Reglas de epicrisis, firma del ingreso, folios anulados y su relación con facturación (prefacturado/facturado, RIPS, soportes) y con el envío de RDA al Ministerio (validaciones, reintentos, estados).
5. Reglas del flujo PyP: criterios de aprobación de afinamiento/preingreso, ciclo RPMS, asignación a programas, consolidado de actividades y origen de la agenda de crónicos.
