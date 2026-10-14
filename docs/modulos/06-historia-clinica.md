# Historia clínica y atención

Módulo `SUROSHistoriaClinica` (ASP.NET + Ext.NET). Base de rutas: `/SUROSHistoriaClinica/Vistas/Privado/`. Fuente: extracción de UI (solo observación, sin datos de paciente) y, para las pantallas de historia clínica, enfermería y evolución médica, el JavaScript propio de cada página (`_codigo-js.md`). Las marcas "confirmado/corregido en código" citan la función del JS; la lógica del servidor (métodos `SRV.*`) no es visible. Se documentan 24 pantallas (home + 23 del árbol por especialidad). Las pantallas compartidas (agenda médica, historia clínica de consulta externa) se extrajeron una vez; el árbol indica qué áreas las usan.

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
- **Flujos y reglas**: Asignado → toma de muestra (parcial/realizada) → registro de resultado (parcial/completo) → resultados entregados; anulado/rechazado terminales (inferido). La orden proviene de una orden médica de la HC (confirmado en código: `DatosSolicitudLaboratorio`; el estudio guarda el ingreso de origen `INGR_ID_ORIGENORDEN` y puede no tenerlo). Rangos mín/máx sirven para marcar valores alterados (inferido).
- **Hallazgos del código** (`LaboratorioClinicoAtencion.aspx`):
  - Opciones por fila de paciente: "Marcar Inasistencia" (`Inasistencia`), "Datos de Solicitud" (`DatosSolicitudLaboratorio` → `SRV.DatosSolicitudLaboratorioOrden`) y "Anular Orden" (`AnularTurno`, ventana de eliminar turno de urgencia). Por fila de estudio: "Anular Estudio" (`AnularEstudio`), que no se ofrece cuando el estado del estudio es `ESLAID = 8`.
  - Sin ingreso de origen avisa: "Este laboratorio no tiene relacionado una historia".
  - Si la cita está en estado `ESAGID = 7` bloquea la acción: "El paciente se encuentra inactivo por inasistencia en esta cita, por favor active nuevamente el paciente desde el icono de Activación ubicado al final del registro en la lista." (`setPanel`).
  - El menú contextual habilita la opción `MB2` solo para `ESLAID` 2, 4 y 5 (`showMenu`); el mapeo de esos ids a los nombres de estado de la UI no está en el JS.
  - Columnas calculadas: turno (fecha-hora, destino asistencial = estancia, asignado por), paciente (tipo y documento, sexo, edad, empresa, zona) y facturación (n.º de documento, fecha, registrado por).
  - La lista de estudios se pide con turno, paciente, procedimiento e ingreso (`SRV.LP`); la cabecera muestra "EPS de afiliación" y "EPS de ingreso" con el mismo valor de empresa.

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
- **Flujos y reglas**: el destino determina el paso siguiente: hospitalización/cirugía generan ingreso a esas agendas, referencia genera formato de remisión (inferido). Los botones REALIZAR HISTORIA CONSULTA EXTERNA / REALIZAR FORMATO PROCEDIMIENTOS (ventana "Opciones") eligen el tipo de formato (inferido). Las órdenes de procedimientos y las fórmulas viven en el panel de formatos que recarga "Actualizar formatos" (confirmado en código: `ActualizaFormatos`, `SelDestino`: pestañas de fórmula médica y grilla de procedimientos solicitados); las interconsultas no aparecen en el JS.
- **Hallazgos del código** (`ConsultaExterna.aspx`):
  - La página corre dentro de una pestaña del contenedor: el paciente sale de `parent.Pac` y la agenda/cabecera se refrescan vía `parent.ActualizaAgenda` / `parent.Actualiza`. El ingreso sale de la grilla de datos básicos (`GridDatosBasicos`). Los formatos (procedimientos, órdenes) se cargan en `PanelFormatos` con parámetros `H` (historia), `INGRID` y `PACIID` (`ActualizaFormatos`).
  - No hay función de guardado entre las funciones propias de la página (a diferencia de Historia urgencia, que tiene `GHC`); el guardado de consulta externa no es visible en este JS.
  - **IMC** = peso / talla² × 10000 (talla en cm); **superficie corporal (m2)** = peso × 4 + 7 (el código no divide por peso + 90). Si peso y talla valen 0 deja ambos en 0 (`CalcIMC`).
  - Etiqueta de peso y riesgo según IMC (`calcularPesoEtiqueta`): <16 Delgadez Severa / Infrapeso; 16-16,99 Delgadez Moderada / Infrapeso; 17-18,49 Delgadez Aceptable / Infrapeso; 18,5-24,9 Normal / Normal (Peso saludable); 25-29,9 Preobeso / Aumentado; 30-34,9 Obeso Tipo I / Moderado; 35-39,9 Obeso Tipo II / Severo; ≥40 Obeso Tipo III / Muy severo (Obesidad mórbida).
  - Alertas de color en signos vitales (`CSV`): TA media = (2×sistólica + diastólica)/3, roja si es menor de 76,66 con edad ≥14 o mayor de 143,33; FC roja <50 o >120 y amarilla 50-60 o 100-120 con edad ≥7; SatO2 amarilla 88-91 y roja <88. Al cambiar la sistólica recalcula el riesgo Framingham-Wilson (`framinghamWilson.setFraminGhamDS`, `validarFraminghamWilson`).
  - Si la edad es menor de 8 se oculta el examen mental y sus 14 campos pasan a opcionales (`setEdad`). "Marcar normal" de revisión por sistemas, examen físico y mental se ejecuta junto (`CargaRapida`).
  - Diagnósticos: no permite repetir un código ("El diagnóstico con código CIE10 <b>…</b> ya está en la lista."); el primero queda PRINCIPAL y los siguientes SECUNDARIO (`SelecCIE10`, `Prioridad`); la búsqueda CIE-10 con Enter exige texto: "Es necesario que escriba un parámetro de búsqueda." (`SRV.CONS`).
  - Antecedentes V1: el botón "Cargar otros antecedentes (V1)" (`cargarOtrosAntecedentesV1`) llama `SRV.ANTV1.CargaAntecedentesPorPaciente(género, paciente, '1,2,3,4')`; sin paciente: "Debe seleccionar un paciente primero."; con error: "No se pudieron cargar los antecedentes V1."; el género por omisión es 'M'.
  - Borrador local: `OffLine.Guardar` al cambiar signos vitales y al agregar diagnósticos, `OffLine.Eliminar('P'+paciente)` al actualizar formatos (los datos se serializan como JSON en el navegador, `BDCliente.js`).
  - Visor RDA: panel plegado que al expandirse carga por iframe el módulo `SUROSRDA` (`VisorRDA.aspx?PaciId&IngresoId&Usuario`); el RDA es un módulo aparte (`CargarVisorRDALazy`).
  - Queda código de prueba en producción: `CargarTestSV` rellena la historia con "DE PRUEBA PARA TEST" y el diagnóstico G112.

Catálogo **Causa externa** (RIPS, 27 valores): accidente de trabajo; lesión por agresión; lesión autoinfligida; enfermedad general; sospecha de violencia sexual; otro tipo de accidente; accidente en el hogar; accidente de tránsito de origen común; enfermedad laboral; intervención colectiva; atención de población materno perinatal; riesgo ambiental; otros eventos catastróficos; accidente de mina antipersonal (MAP); artefacto explosivo improvisado (AEI); munición sin explotar (MUSE); otra víctima del conflicto armado; promoción y mantenimiento de la salud (intervenciones individuales); accidente de tránsito de origen laboral; evento catastrófico de origen natural; sospecha de violencia física; sospecha de violencia psicológica; sospecha de negligencia y abandono; IVE por peligro a la salud o vida de la mujer; IVE por malformación incompatible con la vida; IVE por violencia sexual/incesto/inseminación no consentida; evento adverso en salud; accidente en el entorno educativo.

## Atención de urgencia > Enfermería > Agenda procedimiento enfermería
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Urgencia/AgendaProcedimientosEnfermeria.aspx`

- **Propósito**: lista de pacientes de urgencias con procedimientos de enfermería.
- **Funcionalidades**: El usuario puede actualizar la agenda, dar salida al paciente y marcar inasistencia con nota.
- **Listados**: Fecha ingreso | Tipo doc | Documento | Nombre paciente | EPS.

## Atención de urgencia > Enfermería > Cirugía > Agenda cirugía urgenciada
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaCirugiaUrgenciada.aspx`

- Página sin componentes extraídos (título vacío). Propósito (inferido): pacientes en cirugía de urgencia para enfermería. Por verificar.
- **Hallazgos del código**: solo reenvía `AccionAgendaG` al padre; es un contenedor y la lista vive en otra página.

## Atención de urgencia > Enfermería > Cirugía > Agenda enfermería cirugía programada
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaCirugiaProgramada.aspx`

- **Propósito**: agenda de enfermería de pacientes con cirugía programada.
- **Funcionalidades**: El usuario puede filtrar por fecha, actualizar, dar salida al paciente, **cambiar estancia/destino del paciente** (ventana "CAMBIAR DESTINO PACIENTE", combo Destino) y registrar inasistencia.
- **Listados**: Jornada | Hora | Fecha ingreso institución | Fecha ingreso estancia | Fecha última evolución | Documento | Nombre paciente | Procedimiento | EPS | Acudiente | Médico | Estado.
- **Hallazgos del código** (`AgendaEnfermeriaCirugiaProgramada.aspx`): abre "ACTIVIDADES DE ENFERMERIA" (`ActividadesEnfermeria.aspx`) con el ingreso del paciente, o sin ingreso si aún no existe (`SRV.SP`). Si la enfermera ya definió una salida (`DEPC_IDENFERMERA` distinto de vacío y de '22') bloquea: "El paciente tiene una salida definida por enfermería, no es posible abrir el modulo de actividades de enfermería". "Dar salida" solo se habilita con `INGR_ESTADO` 3 o 4; "Cambiar estancia" se oculta cuando el destino médico y el de enfermería coinciden (`CambiarEstanciaPaciente`, `CambiarDestino` → `SRV.ActualizarDestinoPaciente`). Filas: `ESCI_ID = 1` se pinta como inasistencia y `DEPC_ID = '1'` como salida. Activar una cita inasistente pide "Está seguro de activar la cita?" (`AC`).

## Atención de urgencia > Enfermería > Entrega de turno enfermería
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/EntregaTurno/EntregaTurnoEnfermera.aspx`

- **Propósito**: relevo de turno entre enfermeras por instancia.
- **Funcionalidades**: El usuario puede elegir instancia {OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA}, generar o cargar la lista de pacientes (selección por habitación, seleccionar todo/limpiar), anotar por paciente observación y pendientes, registrar nota general, **entregar turno**, **recibir turno** (credenciales de quien recibe; check "También recibo el turno"; fecha/hora de registro), editar observación, eliminar, ver detalle, exportar PDF.
- **Listados**: Turno actual: Cama | Nombre paciente | Edad | Especialidad | Diagnóstico | Observación | Pendientes/Observación. Historial: Fecha | Enfermera(o) entrega | Enfermera(o) recibe | Instancia | Cantidad | Nota. Selección: Paciente | Cama.
- **Flujos y reglas**: la entrega queda pendiente hasta que otro usuario la recibe con su clave (confirmado en código: `RL`, `CP`; ver hallazgos).
- **Hallazgos del código** (`EntregaTurnoEnfermera.aspx`; el de médico es equivalente):
  - Dos operaciones en la misma pantalla: `CP` fija `ENTR = 1` (entregar) y envía los pacientes seleccionados (`SRV.CIP`); si no hay ninguno: "No hay pacientes seleccionados para continuar". Con `ENTR = 2` (recibir) se toma el turno elegido en `GridListaTurnos` (`ENFE_ID` y `FUNC_IDENTREGA`; en médico `ENME_ID` y `MEES_IDENTREGA`).
  - `RL` valida en este orden: "Ingrese usuario.", "Ingrese contraseña.", "Ingrese la fecha.", "Ingrese la hora."; envía usuario y contraseña de quien firma, instancia (`DEPCID`), fecha-hora, indicador `RECIBE` (check "También recibo el turno") y la nota solo si recibe (`SRV.RET`). Entregar y recibir se autentican con credenciales.
  - Los pacientes se cargan por instancia y habitaciones (`SRV.CLP`); la observación editada se guarda en el campo `OBSERVACION` (enfermería) o `PENDIENTES` (médico); `GML` guarda cambios de un turno entregado (`SRV.MPT`). Cada nombre enlaza al paciente (`SRV.DR(tipo, ingreso)`). El detalle médico muestra CAMA, DIAGNOSTICO y OBSERVACIÓN.

## Atención de urgencia > Enfermería > Hospitalización > Agenda hospitalización
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaHospitalizacion.aspx`

- Solo título "Agenda Enfermería Hospitalización"; sin componentes extraídos. Propósito (inferido): pacientes hospitalizados para registros de enfermería.
- **Hallazgos del código**: contenedor sin lógica propia; delega en el padre la apertura de pestañas (`AccionAgendaG`) y recarga el panel interno con `App.Viewport1.getBody().Actualizar()`. El contenido real está en una página anidada no extraída.

## Atención de urgencia > Enfermería > Observación > Agenda de observación
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaObservacion.aspx`

- Mismo caso para pacientes en observación (el título extraído repite "Hospitalización"). Por verificar.
- **Hallazgos del código**: igual que hospitalización (`AccionAgendaG`, `Viewport1.getBody().Actualizar()`).

## Atención de urgencia > Médico > Agenda de hospitalización médico
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionHospitalizacion.aspx`

- Solo título "Agenda Evolución Hospitalización". Propósito (inferido): evolución médica diaria de hospitalizados.
- **Hallazgos del código**: contenedor sin lógica propia; reenvía `AccionAgendaG` y `CargaDataExterno` al padre (abre la historia o evolución en otra pestaña).

## Atención de urgencia > Médico > Agenda de observación médico
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionObservacion.aspx`

- Solo título "Agenda Evolucion Observación". Propósito (inferido): evolución médica de pacientes en observación.
- **Hallazgos del código**: contenedor sin lógica propia; reenvía `AccionAgendaG` y `CargaDataExterno` al padre (abre la historia o evolución en otra pestaña).

## Atención de urgencia > Médico > Cirugía > Agenda nota quirúrgica
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaCirugia.aspx`

- Solo título "Agenda cirugia". Propósito (inferido): pacientes de cirugía de urgencia para registrar la nota quirúrgica.
- **Hallazgos del código**: contenedor sin lógica propia; reenvía `AccionAgendaG` y `CargaDataExterno` al padre (abre la historia o evolución en otra pestaña).

## Atención de urgencia > Médico > Consulta de urgencia > Historia urgencia
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/HistoriaUrgencia.aspx`

- **Propósito**: historia clínica de la atención médica de urgencias.
- **Funcionalidades**: El usuario puede registrar el formato de ingreso (nota de ingreso, caso especial, observación), motivo, causa externa, enfermedad actual, antecedentes (mismos paneles que consulta externa, más "Cargar otros antecedentes (V1)" y ver versión anterior), signos vitales, examen físico, resultados de ayudas DX, conducta, diagnósticos, destino y referencia/contrarreferencia, plantillas, adjuntos, visor y envío de RDA al Ministerio, enviar al final de la agenda.
- **Datos** (diferencias frente a consulta externa):
  - Caso especial {NINGUNA, EMBARAZO, DISCAPACITADOS, ALERGIAS, ENFERMEDAD MENTAL}.
  - Examen físico por segmentos con "Marcar normal": aspecto general, cabeza, ojos, oídos, nariz, orofaringe, cuello, tórax, pulmonar, cardiovascular, perfusión, abdomen, extremidades, genitourinario, neurológico, piel, observaciones.
  - Signos vitales como en consulta externa; el guardado envía perímetro encefálico y no se ve perímetro de cintura (corregido según código: `GHC`).
  - Antecedente de vacuna de fiebre amarilla: "Aplicación fiebre amarilla" {SI, NO}.
  - Donación de órganos: Donante detectado {SI, NO}, Voluntad anticipada {SI, NO}, Nota.
  - Diagnóstico: CIE-10, tipo de diagnóstico, prioridad, observación.
  - Destino {SALIDA, OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA, MORGUE, SALIDA POR REFERENCIA Y CONTRAREFERENCIA, RETIRO VOLUNTARIO, FUGA}; botones Editar destino y Editar referencia y contrarreferencia (pregunta SI/NO).
  - Botones GUARDAR CONSULTA DE URGENCIA, Actualizar formatos.
- **Listados**: Antecedentes; Diagnósticos: Código | Descripción | Prioridad; envío RDA: Tipo | Estado | Detalle | Hora.
- **Flujos y reglas**: cada destino tiene un tipo (`DEPC_TIPO`): 1 = salida; los demás son ingreso a otra instancia y exigen "información de ingreso" (confirmado en código: `SelDestino`, `GHC`). Que OBSERVACIÓN/HOSPITALIZACIÓN/CIRUGIA muevan al paciente a las agendas respectivas, que MORGUE implique defunción y que RETIRO VOLUNTARIO y FUGA cierren el ingreso sin alta médica sigue siendo inferido.
- **Hallazgos del código** (`HistoriaUrgencia.aspx`):
  - **Guardar (`GHC`)** valida en este orden, con `Ext.Msg.alert('Notificación', …)`: mensaje del panel de formatos si su validación devuelve `NO|…`; "Favor seleccione la <b>Causa externa</b>."; "Favor diligencie el <b>Motivo de la consulta</b>."; "Favor diligencie la <b>Enfermedad actual</b>."; "Favor diligencie los campos de <b>signos vitales</b>."; "Favor diligencie los campos de <b>Examen fisico</b>."; "Favor ingrese el diagnostico"; "Favor ingrese el <b>tipo de diagnostico</b>"; "Favor seleccione el <b>Donante detectado</b>"; "Favor seleccione el campo de <b>antecedentes de vacunas de fiebre amarilla</b>"; si donante = 1, "Favor seleccione el <b>Voluntad anticipada</b>"; "Favor diligencie los campos obligatorios resaltados en rojo."; "Favor seleccione el destino del paciente."; si el destino es de ingreso, "Es necesario que ingrese la información de ingreso." (abre la ventana de formato de ingreso).
  - Confirmación: "<b>Está seguro de guardar la historia clínica?</b> Una vez guardada no podrá realizar ninguna modificación." Si la historia ya existe: "La historia clínica ya fue guardada, no es posible realizar ninguna modificación." La excepción es la bandera `EHI == '1'`, que guarda sin confirmar (significado no visible).
  - Datos enviados a `SRV.GH(datos, antecedentes, diagnósticos nuevos, formatos)`: solo viajan los diagnósticos nuevos (`DICI_ID = '-1'`) y los antecedentes modificados (V2: tipo, ítem, id, descripción). Se envían también fecha-hora de ingreso y salida "para cambiar".
  - Antes de guardar registra una auditoría en el contenedor (`parent.parent.GAJ("HISTORIA URGENCIA", …)`); si falla no bloquea el guardado.
  - Saturación de oxígeno vacía se envía como 95 (`SATUOXIG`); peso y talla vacíos como la cadena 'null'.
  - Si "antecedentes de vacunas de fiebre amarilla" es NO (`AplicacionFiebreAmarilla == "0"`), agrega a la solicitud el procedimiento CUPS 993504 (`AgregarVacunacionFiebreAmarilla`).
  - Destino (`SelDestino`): salida muestra las pestañas de fórmula médica y fórmula extramural; los demás destinos abren el formato de ingreso (nota de ingreso, caso especial, observación), muestran "Editar destino" y dejan solo la fórmula intramural. Con causa externa 3 o 4 se mantiene la pestaña de fórmula extramural. Carga además tratamientos anteriores (`cargarTratamientosAnteriores`).
  - Diagnóstico: al borrar el principal, el primero restante pasa a principal (`DelDiag`). "Marcar normal" del examen físico escribe textos predefinidos en mayúsculas por segmento (por ejemplo "BUEN ESTADO GENERAL, CONDICIÓN NORMAL.", "RUIDOS CARDIACOS RÍTMICOS, SIN SOPLOS.") solo en los campos vacíos (`MNExamenFisico`).
  - Recuperación de borrador: "El paciente tiene una historia de urgencia sin guardar, desea recuperar la información de la historia?" (`RecuperaHistoria`, almacenamiento local por paciente).
  - La historia puede precargarse desde urgencia (`SRV.RHC`) o desde un registro externo (`CargaDataExterno` → `SRV.CDA`); comparte con consulta externa el IMC, las etiquetas de peso, las alertas de signos vitales y el visor RDA.
  - **Antecedentes V2** (almacén en el cliente, `AntecedenteStore`): cada alta recibe un UUID y fecha-hora de registro (dd-MM-aaaa HH:mm:ss) y muestra "Antecedente agregado correctamente" (o "Registro actualizado/eliminado correctamente"). Requeridos por tipo: alérgico = tipo de alergia, estado de verificación, reacción alérgica y medicamento o descripción del alérgeno; patológico personal = patología (CIE), año, tratamiento actual, estado, condición clínica; patológico familiar = patología familiar (CIE), parentesco, estado; farmacológico = medicamento; quirúrgico = procedimiento CUPS; ginecológico = FUM, ciclo menstrual, anticoncepción, citología vigente, menopausia; no patológico = al menos una opción ("Debe seleccionar al menos una opcion."); vacuna = "Debe seleccionar una vacuna.", "Debe seleccionar la fecha de aplicación.", "Debe seleccionar la dosis."; genérico = "Debe escribir una descripcion.". Eliminar pide confirmación o avisa "Seleccione un registro de la lista para eliminar.". Las secciones ginecológicas, obstétricas y perinatales se bloquean para género M: "Esta sección aplica solo a pacientes femeninos." (excepto vacunas perinatales).
  - Condición al nacer arma el texto de complicaciones: DIFICULTAD RESPIRATORIA, ICTERICIA NEONATAL, SEPSIS NEONATAL, HIPOGLUCEMIA, "OTRA: …" o "NO"; alimentación inicial: LACTANCIA MATERNA, MIXTA, ARTIFICIAL; inicio de lactancia: < 1 HORA, 1 HORA, NO RECIBIO.
  - El archivo contiene `CargarTestSV` (datos de prueba), igual que consulta externa.

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
- **Flujos y reglas**: la prioridad la elige el usuario (no se calcula) y la acción de atención (`ACCIONATENCION`, "Definir estado de atención") se elige por separado; el cliente no vincula una con otra, por lo que la derivación a consulta externa u odontología no depende de la prioridad en el JS (corregido según código: `GR`). Qué hace el servidor con cada acción no es visible; que "Continuar" deje el ingreso en la agenda de urgencia con su prioridad sigue siendo inferido.
- **Hallazgos del código** (`Triage.aspx`):
  - **Glasgow** = suma de los valores de apertura ocular (`APCO_VALOR`), respuesta verbal (`REVE_VALOR`) y motora (`REMO_VALOR`), mostrada como "N/15" cuando los tres están elegidos (`CalcGlasgow`); se guarda solo el número (`GLASMO`).
  - **Clasificación de urgencia** (`ComboEstadoTriage`, `CLASURG`): lista maestra con color propio (`CLAS_COLOR`) que tiñe el combo; igual el triage obstétrico (`ClasificacionRiesgoObstetrico`, `CLRO_COLOR`).
  - **Guardar (`GR`)** valida en este orden: "No se ha realizado el calculo de <b>Glasgow</b>"; "Favor Ingresar la información de los signos vitales."; "Defina la clasificación de urgencia para continuar."; "Favor ingresar el motivo de la consulta"; "Favor ingresar la observación"; "Favor ingresar la enfermedad actual"; "Defina la causa externa."; "Defina si es urgencia por reingreso."; "Defina el estado de ingreso."; si género F: "Ingrese el <b>FUR</b>" (cuando "aplica FUR" = 1) y "Defina si el paciente esta en estado de embarazo."; si embarazo = 1: "Debido a la condicion de embarazo, debes definir el estado de <b>Triage Obstetrico</b>.". Envía `SRV.GR(datos, medicamentos alérgicos, antecedentes)`.
  - Campos enviados: acción de atención, signos vitales (TA, FC, FR, SatO2, glucometría, fetocardia, temperatura, peso, talla, IMC, m2), Glasgow por componente, motivo, enfermedad actual, observación, semanas de embarazo, días de posparto, fecha probable, reingreso y fecha, estado de ingreso, embarazo, alergia (1 si hay medicamentos en la grilla), causa externa, FUR, riesgo obstétrico y clasificación. Los indicadores por sistema (NERVIOS, LOCOMOT, CARDIAC, PULMONA, DIGESTI, URINARI, OTROS) viajan fijos en 0 (campos en desuso). Al reiniciar, embarazo queda en el valor 2.
  - Alertas de color de signos vitales propias del triage (`CSV`): FC roja <50 o ≥120, amarilla 50-59 o 100-119 (edad ≥7); temperatura con edad <5: amarilla 38,5-40,1 y roja >40,1; glucometría amarilla 350-459 y roja ≥500; TA y SatO2 como en consulta externa. El triage no calcula etiquetas de peso, solo IMC y m2.
  - Reingreso: se elige un ingreso previo y queda como "Ingreso: … | Salida: …" más su identificador. Medicamentos alérgicos: "El medicamento <b>…</b> ya esta en la lista."; quitar pide "Realmente desea quitar e medicamento de la lista?" y borra en cliente los nuevos o llama `SRV.EM` para los ya guardados.

## Atención de urgencia > Médico > Entrega de turno
`/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/EntregaTurno/EntregaTurnoMedico.aspx`

- **Propósito**: relevo de turno médico por instancia {OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA}.
- **Funcionalidades**: igual a la de enfermería: seleccionar pacientes por habitación, notas, entregar/recibir con credenciales, editar observación, eliminar, ver detalle.
- **Listados**: Cama | Nombre paciente | Diagnóstico | Pendientes/Observación; historial: Fecha | Médico entrega | Médico recibe | Instancia | Cantidad | Nota.

## PyP > Agenda afinamiento
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/Enfermeria/AgendaEnfermeriaAfinamiento.aspx`

- **Propósito**: agenda de enfermería del "afinamiento" (historia inicial de afinamiento, confirmado en código: `EjecutaTab`; que sea valoración de ingreso a programas de salud pública sigue siendo inferido).
- **Funcionalidades**: El usuario puede ir a actividades de enfermería en PyP, abrir la historia inicial de afinamiento, ver las que esperan aprobación del médico, marcar inasistencia y cerrar agenda.
- **Listados**: Jornada | Turno | Hora | Documento | Nombre paciente | EPS | Régimen | Acudiente | Estado | Aprobado.
- **Flujos y reglas**: enfermería realiza el afinamiento; el médico lo aprueba (columna Aprobado) (confirmado en código: `cargarMenu`, `getRowClass`).
- **Hallazgos del código** (`AgendaEnfermeriaAfinamiento.aspx`, `AgendaNotaBasicaProgramasEspeciales.aspx`):
  - El tipo de cita (`TICI_ID`) decide el formulario (`EjecutaTab`): 4 = "HISTORIA CRÓNICOS" (`HistoriaCronicos.aspx`, tipo de procedimiento 30); 8 = "HISTORIA INICIAL DE AFINAMIENTO" (`HistoriaInicialDeAfinamiento.aspx`, 31); 9 = "NOTA BASICA DE PROGRAMAS ESPECIALES" (`HistoriaNotaBasicaDeProgramasEspeciales.aspx`, 32; agenda de nota básica). Para otras especialidades usa el módulo asignado al médico; si falta: "No se ha asignado el modulo de historia para la especialidad del medico."
  - Estado de cita (`ESCI_ID`): 1 = inasistencia (celda rojiza), 4 = atendida (celda verde); con 2 o 3 llama `SRV.SP` antes de abrir la historia; con 4 o 1 abre en modo consulta (`RETORNA: 'SI'`) la pestaña "CONSULTA EXTERNA" (`ConsultaExterna.aspx`).
  - El menú del paciente ofrece `MenuEgreso` si el procedimiento está aprobado por el médico (`PROCEDIMIENTOAPROBADO = 1`) o `MenuEsperando` si no. Si el ingreso ya fue visado por enfermería (`INGR_VISADOENFERMERIA`) pide credenciales (`WinCredenciales`) antes de abrir "ACTIVIDADES DE ENFERMERIA".

## PyP > Agenda de crónicos > Agenda salud pública
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaEvolucionCronicos.aspx`

- **Propósito**: seguimiento médico de pacientes crónicos de programas.
- **Funcionalidades**: El usuario puede filtrar por fecha, mostrar toda la agenda y actualizar.
- **Listados**: Fecha-hora ingreso | Tipo doc | Documento | Nombre paciente | EPS | Médico que atendió | Estado.
- **Hallazgos del código** (`AgendaEvolucionCronicos.aspx`): la columna de última evolución muestra "Sin evolución" o las horas transcurridas, coloreadas: <2 h amarillo, 2 a <4 h naranja, ≥4 h rojo (`CUltimaEvolucion`). Al seleccionar un paciente abre "ACTIVIDADES DE ENFERMERIA" con `VIENEDECRONICOS: 'SI'` y `VIENEDEPYP: 'SI'`, no una nota médica. Incluye un aviso por voz (`reproducirVoz`, síntesis de voz del navegador). Caso especial: 1 NINGUNO, 2 EMBARAZO, 3 DISCAPACITADO, 4 ALERGIA, 5 ENFERMEDAD MENTAL.

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
- **Hallazgos del código** (`EvolucionMedica/AgendaAfinamiento.aspx`): la lista carga las citas de tipo 8 (afinamiento) y 4 (crónicos) (`SRV.AL(..., '8', '4')`); la fila se pinta de verde cuando el paciente tiene procedimientos aprobados (`TOTALPROCEDIMIENTOSAPROBADOS > 0`); si la cita no está atendida y el procedimiento no está aprobado, abre el menú de clasificación (`cargarMenu`) y fija el paciente en el contenedor padre. La ventana "Aprueba/No aprueba al programa" no tiene función en el JS (lógica del servidor).

## PyP > Afinamientos y preingresos > Preingresos
`/SUROSHistoriaClinica/Vistas/Privado/Agenda/EvolucionMedica/AgendaPreingreso.aspx`

- Idéntica a Afinamientos (mismos botones, ventanas y columnas) para el flujo de preingreso.
- **Hallazgos del código**: el JS es idéntico al de Afinamientos (mismos tipos de cita 4 y 8 y mismas acciones; `EjecutaTab`).

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
- **Flujos y reglas**: la reautenticación (usuario/clave) protege la entrega de turno (confirmado en código: `RL`) y, por la UI, la firma y el despacho (sin evidencia en el JS; inferido). El ingreso progresa EN ATENCIÓN → ATENDIDO/EN TRATAMIENTO → PREFACTURADO → FACTURADO. Anular factura exige motivo.
- **Hallazgos del código** (`InicioHistoria.aspx`):
  - Firma manuscrita con tableta Wacom STU: la página sondea el servicio local SigCaptX hasta 20 veces, una por segundo (`checkForSigCaptX`); si no conecta solo lo registra en consola.
  - Eliminar o editar un procedimiento facturado pide confirmación: "Está seguro de ELIMINAR este procedimiento?" / "Está seguro de EDITAR este procedimiento?" más "Una vez ELIMINADO no podra recuperarlo." / "Una vez EDITADO no podra recuperarlo." (`ElimnarProcedimientoFactura`, `EditarFactura`); editar abre `Facturador.aspx` en la pestaña "SOPORTES FACTURA".
  - Descarga de soportes por tipo, procedimiento, paciente y factura (`DescargarSoporte`); "solo paquete" genera PDF por centros de costo (`FacturasSoloPaquete`).
  - Impresión de medicamentos por mes o rango: avisa "Complete el año", "Seleccione un mes", "Seleccione una fecha inicial", "Seleccione una fecha final", pero no detiene la llamada (`ImprimirMedicamentos` sigue a `SRV.ExportarAPdf`).
  - Estado de las líneas de medicamento por color: modificado en verde, suspendido en rojo; tratamientos agrupados en otro color (`getRowClassIIII`, `getRowClassIIIII`).
  - Despacho de suministros: dos acciones, "Entregar" (descuenta stock) y "EntregarSinDescontar" (`DESCONTAR` verdadero o falso), con almacén, tipo, id y cantidad (`ejecutarAccionesEnLinea` → `SRV.EntregarSuministro`).
  - Crear ingreso sin cita: fecha-hora de ingreso y de egreso, empresa y contrato opcional (`GenerarIngreso` → `SRV.CrearIngresoSinCita`).
  - **RDA**: dos pasos, validar (`EnviarRDAministerio` → `SRV.ValidarRda`) y generar/enviar (`GenerarRda` → `SRV.GenerarRdaMinisterio`), con tipo de evento (`TIPORDA`) y el ingreso; la credencial del prestador la resuelve el servidor, no el navegador. La epicrisis y el corte de instancia viajan como opciones de la misma llamada.
  - Anexos digitales y Trazabilidad se abren como pestañas (`AdjuntosDigitales.aspx`, `TABTRAZABILIDAD.aspx`) y exigen paciente o ingreso seleccionado: "Es necesario tener un paciente seleccioando para utilizar esta opcion". Familiograma es una aplicación React embebida en iframe con el árbol guardado en `localStorage` (`familyTree`).
  - Laboratorios: imprimir unificado o individual (`ImprLabs`); la formulación se registra como formato aparte (`GuardarFormulacion` → `SRV.RegistrarFormatoFormulacion`).

## Otras pantallas con código (no documentadas por UI)

- **Unificar historia clínica** (`HistoriaClinica/UnificarHistoriaClinica.aspx`): traslada ingresos de un paciente a otro (duplicados). Pide "Está seguro de continuar con el proceso?"; exige elegir al menos un ingreso del paciente origen: "Seleccione Minimo un ingreso del paciente 1 para continuar." (o 2); estado del ingreso en pantalla: 1 = EN ATENCIÓN, otro = ATENDIDO. Solo se puede eliminar el registro de un paciente si no tiene ingresos: "No puede continuar, el paciente <b>…</b> tiene registros de ingreso". Otra transferencia exige "Seleccione minimo un registro para continuar." y "Es nesesario que seleccione un paciente de destino" (`SRV.TI`, `SRV.TIP`, `SRV.EP`).
- **Reporte de remisiones** (`Informes/ReporteRemisiones.aspx`): filtros por rango de fechas, condición, mes y año (`SRV.BuscarInfo`); exporta a Excel solo si hay consulta: "Por favor, primero haga la consulta". `Informes/InicioInformes.aspx` no tiene código propio.
- **Especialidad del médico** (`Medico/Especialidad.aspx`): el check "otra evolución" (`ChkOtraEvo`) habilita la fórmula intramural y el panel de escala suicida (`PanelEscalaSuicida`), lo que indica que existe una escala de riesgo suicida en la evolución médica; columnas de recurso con "SIN DEFINIR" y "NO APLICA".
- **Formulario de funcionario** (`Funcionario/FormularioFuncionario.aspx`): si "es médico" = 1 exige registro médico: "Ingrese el registro médico para continuar"; guarda también licencia de salud ocupacional, especialidades del médico (con indicador de si realiza cirugía y si aplica a programas PyP) y convenios; evita repetir especialidad o convenio ("La especialidad … ya se encuentra en la lista"); confirma "Está seguro de crear un nuevo registro?" / "Está seguro de modificar el registro?" (`GU`).
- **Agenda facturación hospitalización** (`Agenda/Enfermeria/AgendaFacturacionHospitalizacion.aspx`): lista con leyenda de colores "PACIENTES EN PROCESO DE REFERENCIA Y CONTRAREFERENCIA", "PACIENTES EN PROCESO DE SALIDA" y "PACIENTES EN UNIDAD FUNCIONALES DE LA INSTITUCIÓN"; las filas con ingreso visado por enfermería parpadean; consulta por mes o rango de fechas (`Consulta` → `SRV.GCM`); caso especial: 1 NINGUNO, 2 EMBARAZO, 3 DISCAPACITADO, 4 ALERGIA, 5 ENFERMEDAD MENTAL.

---

## Flujo de atención (inferido; pasos 2, 3 y 6 con respaldo parcial en el JS de Triage e Historia urgencia)

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

Los formularios clínicos reales solo se abren desde un encuentro con paciente real, lo cual no se hizo (solo observación, sin datos de paciente). El JavaScript de las páginas permitió reconstruir los campos, validaciones y cálculos de Historia urgencia, Triage y los antecedentes (ver "Hallazgos del código"), pero no el servidor ni los controles cargados por iframe. Lo que sigue sin verse:

- **Consulta externa**: el guardado no está en el JS de la página; los campos de anamnesis, examen y cierre se conocen por la UI y por analogía con Historia urgencia, no por el código. La biblioteca de riesgo Framingham-Wilson y el visor RDA son archivos aparte.
- **Panel de formatos** (`PanelFormatos`): procedimientos solicitados, fórmula médica intramural y extramural, tratamientos anteriores y su validación (`Registros()` devuelve un `MSG` con formato `SI|NO` y texto); se cargan dentro de la historia y no se extrajeron.
- Formato de procedimientos, nota de evolución (observación/hospitalización), nota quirúrgica, partograma, actividades de enfermería (`ActividadesEnfermeria.aspx`), historia de crónicos, historia inicial de afinamiento y nota básica de programas especiales: solo se conoce que existen y cómo se abren.
- Epicrisis, informes de ingreso y de larga instancia, remisiones y referencia/contrarreferencia, recomendaciones y familiograma (aplicación React aparte): solo sus puntos de entrada.
- Las agendas de hospitalización, observación, cirugía y nota quirúrgica son contenedores (`Viewport1`) que cargan una página anidada no extraída.
- Las ramas de odontología, apoyo terapéutico y medicina especializada no tienen hojas extraídas; el código muestra que el formulario sale de un "módulo de historia" asignado a la especialidad del médico, pero no cuál.
- Reglas del servidor: todo lo que ocurre tras `SRV.*` (validación y reintentos del RDA, mapeo de estados de cita, de estudio y de destino, creación de ingresos).

## Preguntas abiertas

### Respondidas

1. **¿Qué formularios abren odontología, apoyo terapéutico y especializada y cómo se configuran?** La agenda abre el formulario del "módulo de historia" asignado a la especialidad del médico; si no hay: "No se ha asignado el modulo de historia para la especialidad del medico."; los tipos de cita 4, 8 y 9 abren historia de crónicos, historia inicial de afinamiento y nota básica de programas especiales. Fuente: código: `EjecutaTab`. (Qué módulo tiene cada especialidad: ver "Sin respuesta".)
2. **¿Dónde se gestionan fórmulas, procedimientos y órdenes?** En el panel de formatos de la historia: fórmula médica intramural, fórmula extramural (con destino de salida o causa externa 3 y 4) y grilla de procedimientos solicitados; el laboratorio guarda el ingreso de origen de la orden. Fuente: código: `SelDestino`, `ActualizaFormatos`, `AgregarVacunacionFiebreAmarilla`, `DatosSolicitudLaboratorio`, `GuardarFormulacion`.
3. **¿Cómo se envía el RDA al Ministerio?** En dos llamadas al servidor, validar y luego generar/enviar, con la credencial del prestador resuelta en el servidor; además hay un visor RDA como módulo aparte por iframe. Fuente: código: `EnviarRDAministerio`, `GenerarRda`, `CargarVisorRDALazy`.
4. **¿La prioridad del triage se calcula?** No: la elige el usuario de una lista maestra con color; Glasgow sí se calcula (suma, hasta 15). Fuente: código: `GR`, `CalcGlasgow`, `ClasificacionUrgencia`.
5. **¿Cuántos niveles tiene el triage y qué lo regula?** Cinco niveles (I a V). Fuente: norma: Res. 5596/2015 (criterios técnicos del triage de urgencias).
6. **¿Se puede modificar una historia de urgencia guardada?** No desde esta pantalla: pide confirmación irreversible y luego rechaza ediciones, salvo la bandera `EHI == '1'`. Fuente: código: `GHC`; coherente con norma: Res. 1995/1999 (la historia clínica es un documento legal).
7. **¿Cómo se calculan IMC, superficie corporal y clasificación de peso?** IMC = peso/talla² × 10000; m2 = peso × 4 + 7; categorías de bajo peso a obesidad tipo III con cortes en 16, 17, 18,5, 25, 30, 35 y 40. Fuente: código: `CalcIMC`, `calcularPesoEtiqueta`; los cortes coinciden con la tabla de la OMS (supuesto estándar del sector).
8. **¿Cómo funciona la entrega de turno?** Entregar (`ENTR = 1`) y recibir (`ENTR = 2`) exigen usuario y contraseña, fecha y hora; el receptor puede dejar nota; se hace por instancia y habitaciones. Fuente: código: `RL`, `CP`.
9. **¿Cómo se aprueba un afinamiento o preingreso?** El médico marca el procedimiento aprobado (`PROCEDIMIENTOAPROBADO` / `PROC_APROBADO`); mientras no lo esté la enfermería ve la opción "Esperando" y al aprobarse "Egreso". Fuente: código: `cargarMenu`, `getRowClass`. (Criterios clínicos de aprobación: ver "Sin respuesta".)
10. **¿Qué es el ciclo RPMS?** Ruta de Promoción y Mantenimiento de la Salud de las rutas integrales de atención. Fuente: norma: Res. 3280/2018 (RIAS).
11. **¿Qué significa el estado de cita `ESCI_ID`?** 1 = inasistencia y 4 = atendida (código comentado: "la agenda debe estar en estado ATENDIDO" para que enfermería actúe); las inasistentes se reactivan con "Está seguro de activar la cita?". Fuente: código: `RenderGrid`, `AC`, `SelecPaciente`.
12. **¿Qué es la agenda de crónicos realmente?** Una lista de seguimiento que abre actividades de enfermería y muestra el tiempo desde la última evolución con semáforo de 2 y 4 horas. Fuente: código: `SelecPaciente`, `CUltimaEvolucion` de `AgendaEvolucionCronicos.aspx`.
13. **¿Qué es obligatorio al guardar un antecedente?** Depende del tipo (ver hallazgos de Historia urgencia); los antecedentes se guardan primero en el navegador con UUID y viajan al guardar la historia. Fuente: código: `AntValidation.requeridos`, `reg*`, `ObtenerAntecedentesV2`.
14. **¿Cómo se firma digitalmente el ingreso?** Con tableta de firma Wacom STU a través del servicio local SigCaptX. Fuente: código: `checkForSigCaptX`.

### Sin respuesta por ingeniería inversa

1. ¿Qué módulo de historia tiene asignada cada especialidad (odontología, apoyo terapéutico, especializada)? Motivo: lógica del servidor (datos de configuración).
2. ¿Qué contienen las agendas de hospitalización, observación, cirugía y nota quirúrgica (evoluciones, notas de enfermería, medicamentos, balance de líquidos) y el módulo `ActividadesEnfermeria.aspx`? Motivo: sin acceso (páginas anidadas no extraídas).
3. ¿Cuál es el ciclo de estados de órdenes de imágenes, interconsultas y remisiones, y cómo se mapean los ids `ESLAID`, `ESCI_ID` 2 y 3 y `DEPC_TIPO` a sus nombres? Motivo: lógica del servidor.
4. ¿Qué validaciones, reintentos y estados tiene el envío del RDA y qué relación tiene con RIPS y con la facturación (prefacturado/facturado)? Motivo: lógica del servidor.
5. ¿Qué efecto tiene cada destino de urgencias (MORGUE, RETIRO VOLUNTARIO, FUGA, observación, hospitalización, cirugía) sobre el ingreso y las agendas? Motivo: lógica del servidor.
6. ¿Qué criterios clínicos aplica el médico para aprobar o no el ingreso a un programa y cómo se asigna el paciente al programa? Motivo: decisión del negocio.
7. ¿Por qué la saturación de oxígeno vacía se envía como 95 en Historia urgencia? Motivo: decisión del negocio (riesgo de dato clínico no medido).
8. ¿Qué hace la bandera `EHI == '1'` que permite guardar sin confirmación? Motivo: lógica del servidor.
9. ¿Cómo se guarda la consulta externa y qué valida? Motivo: sin acceso (la función de guardado no está en el JS de la página).
10. ¿Cómo se calcula el riesgo cardiovascular (Framingham-Wilson) y qué puntaje de salida usa? Motivo: sin acceso (biblioteca no extraída).
11. ¿Cómo se comportan con paciente real la precarga desde urgencia (`RHC`) o registro externo (`CDA`), los tratamientos anteriores y las plantillas? Motivo: requiere paciente real.
12. ¿Qué ocurre con folios, facturas y RDA ya enviados al unificar historias y trasladar ingresos? Motivo: lógica del servidor.
13. ¿Sigue accesible a usuarios finales el código de prueba (`CargarTestSV`)? Motivo: requiere paciente real.
