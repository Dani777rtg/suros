# Facturación

Módulo de facturación de SURÓS/PRORED (`/SUROSFacturacion/Vistas/Privado/...`). Cubre: administración y consulta de facturas, generación de facturas (global, automática, manual V2), facturación electrónica ante la DIAN, generación y validación de RIPS, caja (apertura, arqueo, cierres), homologadores de manuales tarifarios con CUPS, notas crédito y débito (individuales y globales), contratación con EPS/aseguradoras y parámetros de resoluciones/numeración. Se derivó de una extracción de UI y se contrastó con el JavaScript del cliente de cada pantalla; lo que sigue marcado "(inferido)" no se pudo probar en ese código (la lógica de negocio vive en el servidor). Documentación de 19 pantallas.

Convenciones: "Pres. servicio" / "Prestador" = sede PRORED (valores vistos: PRORED Florencia-Caquetá, Cauca, Pasto-Nariño, Risaralda). Empresas vistas: Pijaos Salud EPSI (subsidiado), Asmet Salud EPS (subsidiado y contributivo), APREHSI Ltda, Particular-Otro. Los nombres de cajeros y la credencial WebSisPro visibles en combos se omiten por ser datos personales.

---

## Admón. Facturación > Buscar una factura (`/SUROSFacturacion/Vistas/Privado/Facturacion/BuscarFactura.aspx`)
- **Propósito**: localizar facturas por distintos criterios y reimprimirlas/exportarlas.
- **Funcionalidades**:
  - El usuario puede consultar facturas y elegir el criterio de búsqueda.
  - El usuario puede importar un archivo Excel con los números a buscar (`BTN_IMPORTAR`).
  - El usuario puede exportar una factura en PDF eligiendo el tipo de impresión (ventana "Seleccione Tipo Impresión", con carta/formato).
- **Datos**: Consultar por {POR CÉDULA, POR NÚMERO DE FACTURA, POR NÚMERO PREFACTURA, POR IMPORTACIÓN DE ARCHIVO EXCEL}; Fecha inicio; Fecha fin; Número documento; N° Factura; 7 textfields sin etiqueta (probablemente datos de cabecera de la factura seleccionada, inferido).
- **Listados**: Facturas: N° FACTURA, ESTADO, FECHA INGRESO, FECHA SALIDA, CONTRATO, REGISTRADO POR, FECHA REGISTRO. Grid de impresión: Descripción, Carta.
- **Flujos y reglas inferidas**: los campos visibles dependen del criterio elegido (confirmado en código: `OcultaPnales`, `CamposObligatorioDinamicos`). Existe la búsqueda por PREFACTURA, con el mismo panel que "Factura" (confirmado en código: `OcultaPnales`, `FacturaPrefactura`); que sea previa a la factura no se prueba en el cliente.
- **Hallazgos del código**:
  - Obligatoriedad según criterio (`CamposObligatorioDinamicos`): "Fechas" exige Fecha inicio, Fecha fin y Número documento; "Factura" y "Prefactura" exigen solo N° Factura; "Importe" no exige nada y muestra `BTN_IMPORTAR` y la consulta por Excel.
  - Servidor: `FAC.BuscarFacturas(Data, tipo)`, `FAC.GenerarPdf`, `FAC.FacturasSoloPaquete` (PDF solo de paquete, filtrado por centros de costo).
  - Imprimir sin selección: "Recuerda seleccionar una factura de la lista, antes de imprimir".

## Admón. Facturación > Generador RIPS (`/SUROSFacturacion/Vistas/Privado/Rips/GeneradorRips.aspx`)
- **Propósito**: generar los archivos RIPS por empresa/contrato y periodo.
- **Funcionalidades**:
  - El usuario puede filtrar y consultar los registros a incluir.
  - El usuario puede importar un archivo (`BTN_IMPORTAR`) para acotar la selección (confirmado en código: `Mensaje`; Excel con PREFIJO INICIAL en la primera columna y NÚMERO DE FACTURA en la segunda, la fila 1 se ignora por ser títulos).
  - El usuario puede generar RIPS (ventana "Generar RIPS", botón Aceptar).
- **Datos**: Prestador del servicio (multi, TODOS); Empresa {Particular-Otro, Asmet Salud subsidiado, Asmet Salud contributivo}; Contrato; SubPlan (multi, TODOS); Clasificación {TODOS, POS, NO POS}; Fecha inicial; Fecha final; Generar códigos como {CUPS, SOAT}.
- **Flujos y reglas inferidas**: el contrato depende de la empresa; el subplan del contrato (inferido). La opción CUPS/SOAT decide el manual de codificación que sale en el archivo.
- **Hallazgos del código**:
  - Validaciones (`GI`): "Favor ingrese el <b>tipo de GENERACION</b>" (combo CUPS/SOAT obligatorio) y "Campos obligatorios sin diligenciar" (si el formulario no es válido). Los chequeos de empresa y contrato están comentados.
  - Servidor: `SRV.GI` recibe empresa(s), contrato(s), GRUPO (no "subplan"), clasificación, fechas inicial/final (en `Y/m/d` y `d/m/Y`), prestador(es) y `CODIGOS` (CUPS o SOAT). Empresa, contrato, grupo y prestador viajan como arreglos JSON (selección múltiple).
  - El resultado se publica como enlace (`TextLink`), no como descarga directa.

## Admón. Facturación > Listado facturas (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteFacturasContrato.aspx`)
- **Propósito**: reporte central de facturas por contrato con acciones de facturación electrónica, RIPS y notas.
- **Funcionalidades**:
  - El usuario puede consultar facturas por prestador, empresa, estado del contrato, contrato, subplan, rango de fechas y tipo de programa especial.
  - El usuario puede exportar el listado a Excel o las facturas a PDF (`drpTipoExporte`), y elegir formato: un solo PDF, ZIP por paciente o ZIP por factura; con selección de archivos a imprimir (Ítems del archivo: Descripción, Adjuntar; "Todo carta").
  - El usuario puede obtener el XML electrónico.
  - Sobre facturas seleccionadas: Facturar electrónicamente, Imprimir factura, Convertir a factura, Editar documento, Editar documento Res. 1557, Enviar a la DIAN, Enviar a NEOSAGE, Validar RIPS, Validar RIPS sin factura, Generar nota crédito.
  - Ventana "Seleccione resolución" para escoger la resolución con la que se emite.
  - Ventana "Reporte Envío Factura Electrónica": resultado con facturas enviadas a la DIAN y facturas fallidas (número).
  - Ventana "Validar RIPS": elegir credencial WebSisPro y VALIDAR (validación contra servicio externo del Ministerio; confirmado en código: `AutenticarSispro` -> `SRV.ConectarSispro`, `ValidarRipsSispro` -> `SRV.ValidacionFacturaEvento`); campos ocultos con ids de factura/procedimiento/paciente para "solo procedimiento" (JSON y N).
- **Datos**: Prestador (multi); Empresa; Estado contrato {ACTIVOS, INACTIVOS, TODOS}; Contrato; Subplan (multi); Fecha inicio/fin; Tipo programa especial {TODAS, NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}; Tipo exporte; Tipo (PDF/ZIP).
- **Listados**: Reporte Facturas: Validada RIPS, Prefijo, Número, Tipo doc., Documento, Nombre, Empresa, Tipo afiliación, Prestador, Contrato, Fecha facturado, Fecha ingreso, Fecha egreso, Copago, Cuota moderadora, Pagos compartidos en planes voluntarios, Anticipo, No aplica, Valor total, Subplan, Realizado por, Cod. Diag, Descripción, Médico.
- **Flujos y reglas inferidas**: "Convertir a factura" cambia el tipo de documento de una factura que aún no es electrónica (corregido según código: `ConvertirDocumento` -> `SRV.CambiarDocumento(factura, contrato)` tras confirmar "Esta seguro de CONVERTIR esta factura!"; `showMenu` oculta la opción cuando la fila ya es electrónica; que parta de una prefactura o cotización no se prueba en el cliente). "Enviar a NEOSAGE" es integración con un sistema contable/ERP externo (confirmado en código: `EnviarContable` y, en las notas, el listener `startNeosageListener`; en esta pantalla `EnviarContable` solo confirma y no llama al servidor). Marca "Validada RIPS" por factura: es "Validada" si la factura tiene CUV (`ValidadaRips`: `FAIN_CUV` no vacío). "Editar documento Res. 1557" abre el editor antiguo `EditorFacturador.aspx`, mientras "Editar documento" abre `EditorFacturadorV2.aspx` (corregido según código: `AbrirEditorFacturas1557` / `AbrirEditorFacturas`; el contenido normativo de "1557" no se ve en el cliente).
- **Hallazgos del código**:
  - Confirmaciones: "<b>Está seguro de facturar electronicamente?</b>" (`EjecutarFacturaElectronica` -> `SRV.FacturaElectronica`), "<b>Está seguro de realizar accion?</b>" (XML, `SRV.XmlFacturaElectronica`), "Esta seguro de imprimir este documento!" (`SRV.ImprUnaFactura`), "Esta seguro de CONVERTIR esta factura!", "Esta seguro de Editar este documento!", "Esta seguro de ENVIAR este documento!".
  - Exportar (`Exportar`): tipo 0 = Excel del grid (`SRV.GenerarExcel`; sin datos: "Por favor, primero haga la consulta"); otro tipo = paquete de PDF (`SRV.ImprimirPaqueteFactura`, parámetros empresa, contrato, subplan, fechas, ZIP, programa especial). También `SRV.FacturasSoloPaquete` (PDF solo del paquete).
  - Color de fila: el campo `ELECTRONICA` trae el color; `#EBFFE1` (verde) = factura electrónica.
  - Menú contextual (`showMenu`): si la fila es electrónica, sin CUV y con fecha de factura >= 2025-04-01, aparece "Validar RIPS"; con CUV se oculta. Si no es electrónica, no tiene CUV y la configuración lo permite, aparece "Validar RIPS sin factura" (`PreValidarRips`). "Nota crédito" solo en facturas electrónicas. Banderas de configuración: `OcultarBotonEnviarDian`, `MostarValidadorRipsSinFacturaElectronica`, `facturar`.
  - SISPRO: el estado de la credencial se consulta por POST a `ReporteFacturasContrato.aspx/VerificarEstado` (responde "autenticado." / "No autenticado."); sin credencial: "Seleccione una credencial para continuar."; `SRV.ConectarSispro`, `SRV.ValidacionFacturaEvento` (FainId, IdToken). Error de login: "Lo sentimos, no se han podido validar las credenciales en este momento..." con detalle. Las respuestas JSON se muestran formateadas con botón "Copiar JSON".
  - `SRV.FacturasElectronicasDian` (FAIN, PROC, PACI), `SRV.CambiarDocumentoClinicos` (con parámetro de factura/resolución de clínicos).

## Generar facturas > Factura global (`/SUROSFacturacion/Vistas/Privado/Facturacion/FacturaGeneral.aspx`)
- **Propósito**: emitir una factura consolidada a una empresa/contrato por un periodo, con ítems libres.
- **Funcionalidades**:
  - El usuario puede buscar y cargar un contrato (grid Datos del contrato; botón Cargar) y ver contacto.
  - El usuario puede agregar ítems al consolidado, con búsqueda de coincidencias de producto/servicio ("Nuevo consolidado", "Seleccionar producto").
  - El usuario puede agregar recibos de pago (ventana "Nuevo recibo de pago").
  - El usuario puede consultar facturas globales por fecha, imprimirlas y facturar electrónicamente; cargar un archivo CUV (TXT o JSON); ver reporte de envío (enviadas/fallidas).
  - Listado de empresas/contratos para seleccionar; documentos de la factura global (grid Opciones).
- **Datos**:
  - Cabecera: Prestador {sedes PRORED}; Resolución; Contrato (lista de códigos de contrato); Empresa; Fecha de facturación; Forma de pago {CONTADO, CREDITO}; Medio de pago {EFECTIVO, TARJETA DEBITO, TARJETA CREDITO, TRANSFERENCIA ELECTRONICA}; Periodo (fecha inicial/final de facturación); Total factura.
  - Ítem consolidado: Código, Concepto, Cantidad, Valor unitario, Valor total, Observación.
  - Recibo de pago: Forma de pago {Efectivo}; Concepto pago {COPAGO, CUOTA MODERADORA, COPAGO REGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS DE SALUD, ANTICIPO, NO APLICA}; Cantidad; Valor unitario; Valor total; Observación.
  - Buscar (contrato); Selecciona una fecha (consulta).
- **Listados**: Consolidado (No, Código, Concepto, Observación, Cantidad, V/U, V/T); Recibo de pago (No, Forma de pago, Concepto, Cantidad, V/U, Observación, V/T); Facturas globales (ID, número, fecha, inicio y fin del periodo facturado); Datos del contrato (NIT, Empresa, Contrato, Tipo contrato, Régimen, Opciones).
- **Flujos y reglas inferidas**: total = suma del consolidado menos recibos de pago (confirmado en código: `AgregarRowGridpanel`: `to = sum - res`; `totalCost`/`totalCostRecibo` suman VALORU x CANTIDAD). El archivo CUV sugiere validación del Ministerio de Salud (CUV = código único de validación RIPS/factura) (inferido).
- **Hallazgos del código**:
  - Validaciones (`ValidaFormulario`/`ValidaGridpaneles`): "EL formulario contiene campos no válidos" y "Al parecer alguna de las tabla no tiene registros." (deben tener filas contrato, consolidado y recibo de pago).
  - Los productos del consolidado se escogen de un catálogo NEOSAGE (`SeleccionarProductoNeosage` copia Código y Nombre; `FiltrarProductosNeosage` filtra en cliente por código o nombre).
  - Servidor: `SRV.FacturaElectronica(grid)`, `SRV.datosFacturaGlobal(FAGO_ID)` (ventana de documentos soporte), `SRV.DescargarSoporte({TIPO, FACTURA, ID})` (responde "OK").

## Generar facturas > Facturador automático (`/SUROSFacturacion/Vistas/Privado/Facturacion/ListaIngresos.aspx`)
- **Propósito**: facturar en lote los ingresos pendientes a una fecha y listar pacientes sin facturar.
- **Funcionalidades**:
  - El usuario puede definir "Fecha a facturar" y una fecha fin, y filtrar el árbol de informes (`TreeMenuInformes`) con un trigger field de texto (corregido según código: `filterTree` filtra los nodos del árbol por texto, no por empresa/contrato).
  - El usuario puede exportar pacientes sin facturar por rango de fechas (panel dedicado; botón Exportar) y elegir ítems de impresión (Descripción, Check).
  - Pestaña "Facturación Surós" y formulario "Listado de servicios".
- **Datos**: Fecha a facturar; Fecha fin; Rango de fechas; Fecha fin ingreso sin facturar.
- **Listados**: Ítems de impresión (Descripción, Check).
- **Flujos y reglas inferidas**: no es un facturador masivo: es un navegador que abre en pestañas los módulos del árbol pasando el rango de fechas (corregido según código: `NodoClic` -> `SRV.GuardarFechas(inicio, fin, sede)` y `CargaTab2` con FECHAINICIO, FECHAFIN y ESPECIALIDAD); no hay llamada de emisión masiva en el cliente.
- **Hallazgos del código**:
  - Validaciones (`NodoClic`): "Por favor seleccione una fecha válida" (sin fecha inicio); "El módulo <b>X</b> está abierto." (evita abrir dos veces la misma pestaña).
  - `ExportarSinFactura` -> `SRV.ExportarIngresosSonFacturar` (filas de `GridItems` + rango de fechas). Filas con `ESCOID` 5 o 6 se pintan con la clase `adult-row`.
  - `recargarPaneles` refresca la pestaña activa con `SRV.CargarGrid()`.

## Generar facturas > Facturador manual V2 (`/SUROSFacturacion/Vistas/Privado/Facturacion/FacturadorV2/FacutradorV2.aspx`)
- **Propósito**: construir una factura de un paciente/ingreso con servicios, medicamentos, insumos, cirugía, estancias, paquetes, recibos de pago y datos especiales (SOAT/FURIPS, APS, gestantes).
- **Funcionalidades**:
  - El usuario puede buscar paciente por documento/nombre ("Buscar paciente"), o registrar uno nuevo (ventana "Registrar Nuevo Paciente").
  - El usuario puede facturar sin ingreso previo y facturar sin estado de cuenta (checkboxes); elegir facturación de larga instancia.
  - El usuario puede ver ingresos sin facturar y facturados (paneles) y listar procedimientos a facturar.
  - El usuario puede buscar la última factura del paciente ("BUSCAR ULTIMA FACTURA").
  - El usuario puede abrir paneles de captura: Datos de ingreso, Consolidado, Asistencial, Recibo de pago, Medicamentos, Insumos, Partos-Paquete, Paquete/Canasta/Grupo de atenciones integrales, Cirugía, Estancias, FURIPS.
  - Asistencial: buscar procedimiento (CUPS), "Traer número de autorización principal", "Replicar info a todos los procedimientos", agregar / agregar y cerrar; elegir homólogo (ISS/SOAT) cuando hay varios; ver lista de "Procedimientos que no se pueden facturar".
  - Medicamentos: búsqueda por CUM/nombre, profesional que formula, fecha/hora de aplicación, días de tratamiento, valor real, MIPRES.
  - Insumos: búsqueda por código/nombre, autorización, MIPRES.
  - Estancias: vía de ingreso, fecha/hora salida, autorización.
  - Paquete partos: código CUPS, buscar facturas a relacionar al paquete (rango de fechas), confirmar.
  - Cirugía: cirujano, anestesiólogo, ayudante, tipo de cirugía, anestesia, fecha, vía de acceso, diagnóstico CIE10 y procedimientos a ejecutar.
  - Recibo de pago: adjuntar recibo; relacionar copagos existentes (ventana "Relacionar copagos": cita + copago) o crear copago nuevo; enviar copago a la DIAN.
  - Diagnósticos de ingreso y egreso (CIE10): buscar, importar el de ingreso al de egreso, subir/bajar prioridad, eliminar.
  - "Agregar número de autorización para todo"; "Ver actividades" (registro de actividades: ID, fecha, profesional); eliminar registros seleccionados.
  - Ingresar credenciales (usuario/contraseña) para agregar un procedimiento ya existente en la lista (override con autorización; confirmado en código: `VP`).
  - Lista de estados de cuenta (póliza, fecha registro) y facturas agregadas (grid).
  - Menús laterales "Facturación" y "Tesorería" (Control de caja, Egresos).
  - Pre-validar / VALIDAR RIPS con credencial WebSisPro y ventana "DESEA FACTURAR ELECTRÓNICAMENTE?"; imprimir con tipo de impresión.
- **Datos**:
  - Paciente/ingreso: Documento/Nombre, No. ingreso, Identificación, Nombre, Fecha de nacimiento, Género, Municipio y zona de residencia; Empresa; No. contrato; Tipo programa especial; Prestador; Grupo Subplan; Subplan; Médico; Especialidad; No autorización; No aprobación; Fecha facturación; Resolución.
  - Factura: Cobertura/Pagador {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE/BENEFICIARIO, PPL FONDO NACIONAL DE SALUD, TOMADOR/AMPARADO ARL, SOAT, PLANES VOLUNTARIOS, PARTICULAR, LEY 352 DE 1997}; Forma de pago {CREDITO, CONTADO}; N.º de póliza (seguros); N.º de SIRAS.
  - Ingreso: Fecha/hora de ingreso; Causa externa (lista de ~27 valores: accidente de trabajo, enfermedad general, violencia, IVE, etc.); Fecha/hora egreso; Incapacidad {SI, NO}; Destino {SALIDA, MORGUE, REFERENCIA Y CONTRAREFERENCIA, RETIRO VOLUNTARIO, FUGA, EN TRATAMIENTO, INICIAR TRATAMIENTO, TERAPIA FÍSICA, CANCELAR CIRUGÍA, SALA DE ADMISIÓN}; Estado de salida {PACIENTE MUERTO, A DOMICILIO, DERIVADO A OTRO SERVICIO, REFERIDO, CONTRAREFERIDO, HOSPITALIZACIÓN DOMICILIARIA, SERVICIO SOCIAL, CONTINÚA EN EL SERVICIO (CORTE FACTURACIÓN)}; Causa básica de muerte CIE10.
  - Gestante: Es gestante {SI, NO}; Trabajo de parto {NO, NACIDO EN LA INSTITUCIÓN, REMITIDO}; Datos recién nacido (tipo/número de identificación, sexo {M,F}, edad gestacional, # controles, fecha/hora de nacimiento, peso, diagnóstico principal).
  - APS: Categoría {JORNADA DE SALUD, VISITA DOMICILIARIA, UNIDAD MÓVIL}; Equipo de atención; Zona de atención.
  - Diagnóstico: Tipo {CONFIRMADO NUEVO, CONFIRMADO REPETIDO, IMPRESIÓN DIAGNÓSTICA}; Prioridad; Observación.
  - Asistencial: Unidad funcional {AMBULATORIO, URGENCIAS/OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGÍA, UCI}; Modalidad de atención {INTRAMURAL, EXTRAMURAL (unidad móvil, domiciliaria, jornada de salud), TELEMEDICINA (interactiva, no interactiva, telexperticia, telemonitoreo)}; Grupo de servicios {CONSULTA EXTERNA, APOYO DIAGNÓSTICO Y COMPLEMENTACIÓN TERAPÉUTICA, INTERNACIÓN, QUIRÚRGICO, ATENCIÓN INMEDIATA}; Servicios; Finalidad; Persona que ejecuta; Fecha/hora de ejecución; Cantidad; Valor/U; Valor total; Comisión; Descuento; Autorización; MIPRES; Observación.
  - Estancias: Vía de ingreso {DEMANDA ESPONTÁNEA, DERIVADO DE (consulta externa, urgencias, hospitalización, cirugía, partos, atención/hospitalización domiciliaria, telemedicina, jornada de salud), RECIÉN NACIDO (en la institución / otra), REFERIDO/CONTRAREFERIDO de otra institución}.
  - Cirugía: Tipo {LIMPIA, LIMPIA CONTAMINADA, CONTAMINADA, SUCIA}; Anestesia {LOCAL, REGIONAL, BLOQUEO, GENERAL}; Vía de acceso {BILATERALES, ÚNICA VÍA IGUAL CIRUJANO, DISTINTA VÍA IGUAL CIRUJANO, DIFERENTES ESPECIALISTAS}.
  - FURIPS (accidente de tránsito / evento catastrófico, SOAT): condición del accidentado {CONDUCTOR, PEATÓN, OCUPANTE, CICLISTA}; naturaleza del evento {TRÁNSITO, NATURALES, TERRORISTAS}; tipo de evento; fecha, hora, dirección, departamento, municipio, zona rural/urbana; características; estado de aseguramiento {ASEGURADO, NO ASEGURADO, VEHÍCULO FANTASMA, PÓLIZA FALSA, VEHÍCULO EN FUGA}; vehículo (marca, placa, tipo de servicio {PARTICULAR, PÚBLICO, OFICIAL, EMERGENCIAS, DIPLOMÁTICO/CONSULADO, TRANSPORTE MASIVO, ESCOLAR}, tipo, aseguradora, póliza, vigencia desde/hasta, SIRAS); propietario (persona natural/jurídica con nombre o razón social, tipo y número de documento, dirección, teléfono); conductor (nombre, documento, dirección, teléfono); remisión (fecha remisión/aceptación, IPS que remite y recibe con departamento/municipio, persona, cargo, dirección, teléfono); transporte de la víctima (placa ambulancia, conductor, desde/hasta, tipo {AMBULANCIA BÁSICA, MÉDICA}); atención médica (fechas/horas de ingreso y egreso, diagnósticos ingreso/egreso, médico tratante con registro médico); amparo que reclama (valor facturado y valor reclamado de gastos médico-quirúrgicos y de transporte).
- **Listados**: Consolidado (ID, CUM/Cód, Concepto, Finalidad, Fecha y hora aplicación, Unidad funcional, Num. autorización, Cod MIPRES, Observación, Valor real, %, Cantidad, Valor/U, Descuento, Valor total); Cirugía (ID, CUM/Cód, Concepto, Observación, Valor real, %, Cantidad, Valor/U, Descuento, Valor total); Recibo de pago (Caja, Concepto, Forma de pago, Cantidad, Observación, Valor, Total a pagar, Total pago, Saldo); Facturas agregadas (Número, Fecha factura/ingreso/egreso, Valor total); Diagnósticos (Código, Descripción, Prioridad); coincidencias de medicamentos (Código, Descripción, Forma farmacéutica, Volumen/Peso, Concentración, Existencias) e insumos (Código, Nombre, Presentación, Existencias); Paquete partos (Código, Descripción, Cantidad, Valor unitario, Valor total); homólogos (ISS, Valor ISS, SOAT, Valor SOAT).
- **Flujos y reglas inferidas**:
  - El valor de cada ítem sale del manual tarifario/contrato (homólogo ISS o SOAT con incremento) (confirmado en código: `agregarprocediminetoalconsolidado` envía VALORCOMPRA, INCREMENTO, VALORUNITARIO, VALORDESCUENTO y VALORTOTAL; la fórmula en las notas es `(unitario x cantidad - descuento) x (1 + incremento/100)`; el cálculo inicial del valor es del servidor).
  - Procedimientos sin homólogo o sin cobertura quedan en "Procedimientos que no se pueden facturar" (inferido).
  - Agregar un procedimiento duplicado exige credenciales de usuario autorizado (confirmado en código: `VP` valida "Ingrese usuario." / "Ingrese contraseña." y llama `SRV.HE(procedimiento, {U, P}, consolidado)`).
  - Paquetes de partos relacionan facturas previas (confirmado en código: `ConsultarFacturasRel` -> `SRV.ConsultarFacturasARelacionar`, `CargarFacturasSeleccionadas` -> `SRV.ConsultarDatosRelacionados`; el grid `FacturasRelacionadas` viaja como `FACTRELL` al guardar).
  - Copago puede enviarse como documento electrónico a la DIAN (ventana "Enviar copago a Dian").
  - FURIPS solo aplica cuando la cobertura es SOAT/evento catastrófico (inferido). Panel "Información Soat - Si aplica".
  - Flujo de cierre: pre-validar RIPS, preguntar si se factura electrónicamente, elegir resolución, imprimir (confirmado en código: `CargarValidadorRipsV2` abre la pestaña "GENERADOR RIPSV2" con el FAINID; `GenerarPdfConsoloProcedimiento` (solo PDF), `GenerarPdfConsoloProcedimientoYFacElectro` (PDF y electrónica), `GenerarPdfFacElectro` -> `SRV.FacturasElectronicasDian`; "Esta seguro de cancelar el proceso e imprimir la factura!" en `ImprimirFactura`).
- **Hallazgos del código**:
  - Validaciones al guardar (`GuardarFacturaInterna`, mensaje "Por favor <strong>...!</strong>", en este orden): diagnóstico de ingreso; contrato; diagnóstico de egreso; "Ingrese un procedimiento" (consolidado o cirugía no pueden estar vacíos); tipo de diagnóstico (ingreso y egreso); fecha de ingreso; fecha de egreso; hora de ingreso; hora de egreso (el código vuelve a revisar la hora de ingreso: error de copia); destino; vía de ingreso; atención; prestador del servicio; causa externa; estado de salida (con el mismo texto "Ingrese la causa externa!"); subplan; incapacidad; cobertura. Cada fallo devuelve a la pestaña correspondiente (`setPanel`).
  - Cada procedimiento exige (`agregarprocediminetoalconsolidado`): persona responsable, unidad funcional, modalidad de atención, grupo de servicio, servicios, finalidad, fecha y hora de ejecución; mensajes "Favor diligencie los campos de <b>X</b>." y "Favor diligencie una opcion valida en <b>X</b>." (el valor debe ser numérico, `esNumerico`). Estancias (`agregarEstanciaalconsolidado`) y cirugía (`AgregarCirugia`: cirujano, anestesiólogo, ayudante, tipo de cirugía, tipo de anestesia, fecha, vía de acceso, procedimiento quirúrgico y diagnóstico de la cirugía) tienen validaciones análogas. FURIPS (`GuardarFurips`) exige condición del accidentado, naturaleza del evento, tipo de evento y fecha del evento, entre otros.
  - Edad para RIPS: se toma del texto de nacimiento; unidad 1 = años, 2 = meses, 3 = días (cae a meses si años = 0 y a días si meses = 0). El género se envía como "F"/"M".
  - Guardar (`SRV.GuardarFacturaInterna(datos, contrato)`) envía en un solo objeto: cabecera, diagnósticos ingreso/egreso, consolidado, facturas relacionadas, recibo de pago, cirugía, evoluciones/actividades, FURIPS, datos de recién nacido (FIRN_*), gestante, categoría de programas especiales, equipo y zona de atención, póliza y SIRAS.
  - Programas especiales (`CargarNivelComplejidad`, `CargarEquipoAtencion`): la categoría 1, 2 o 6 habilita "Tipo programa especial"; equipo y zona de atención solo aparecen si el tipo es 1.
  - Larga instancia (`ActivarDateFields`): el check muestra fecha inicial y final y envía bandera "1"/"0".
  - "Facturar sin ingreso previo" (`ActivaTextIngreso`): habilita el número de ingreso manual y limpia fechas, vía, atención, prestador, causa externa y diagnósticos.
  - Autorización masiva (`setAutorizacionMasiva`): "¿Desea aplicar el numero de autorización <b>X</b> a TODOS los registros?". Eliminar selección: "¿Está seguro de eliminar los registros seleccionados?" / "No has seleccionado registros". Quitar factura relacionada: "¿Está seguro de que desea quitar esta factura del consolidado?". Relación de facturas: "Debe seleccionar obligatoriamente una factura con el <b>Check de Datos</b> para continuar.", "Las facturas seleccionadas ya existen en el consolidado.".
  - Paquete de partos: `ConsultarpaqueteParto` -> `SRV.BuscarpaqueteParto(texto, contrato)` (sin texto: "Por favor ingrese un parámetro de búsqueda."); `AgregarItemsPaquetePartos` copia todos los ítems del paquete al consolidado. Con subplan LABORATORIO, VACUNACION, RAYOS X o LABORATORIO SALUD PUBLICA se muestra "Replicar info a todos los procedimientos".
  - Copago a la DIAN: `ConvertirDianCopago` -> `SRV.FacturaElectronicaCopago({copagoId, agenda, agendaId, parametroId})`; el módulo de agenda se fija en el valor '6'. Copagos: `SRV.BuscarCopagosNoRelacionados`, `SRV.AgregarCopagosNoRelacionados`.
  - SISPRO: `VerificarEstado` (POST a `FacutradorV2.aspx/VerificarEstado`), `SRV.ConectarSispro`, `SRV.ValidacionFacturaEvento`; existe también un juego de pruebas (`VerificarEstadoPrueba`, `ConectarSisproPrueba`, `ValidacionFacturaSetPrueba`, `FacturasElectronicasPruebaDian`) para el set de pruebas de la DIAN.
  - Otros métodos de servidor: `SRV.CargarSubplanes(contrato, atención)`, `SRV.EventoValorTotal(consolidado, cirugía, recibo)` (recalcula totales en el servidor), `SRV.Buscarultimafact(identificación)`, `SRV.CambioMeidoc` (especialidad del médico), `SRV.CargarDataActividadesRealizadas`, `SRV.LoadDataFurips`.

## Caja > Apertura de caja (`/SUROSFacturacion/Vistas/Privado/Configuracion/AperturaCaja.aspx`)
- **Propósito**: crear cajas y registrar su apertura con valor inicial.
- **Funcionalidades**:
  - El usuario puede crear una caja (ventana "Caja": nombre; agregar/cancelar).
  - El usuario puede abrir una caja seleccionando caja, funcionario, fecha/hora, valor inicial y observaciones, y guardar la apertura.
  - Ver cajas y aperturas registradas.
- **Datos**: Nombre (caja); Caja (combo con cajas por sede y por cajero/farmacia, nombres de personas omitidos); Funcionario; Fecha/Hora; Valor; Observaciones.
- **Listados**: Cajas (Código, Nombre, Estado); Aperturas (Código, Caja, Responsable, Fecha, Valor, Observaciones, Estado).
- **Flujos y reglas inferidas**: una caja tiene un responsable y estado abierta/cerrada; solo una apertura vigente por caja (inferido). Hay cajas por ciudad, por recepción y por farmacia.
- **Hallazgos del código**:
  - `PrepararDatos` -> `SRV.GuardarApertura`: responsable, fecha, valor, caja y observaciones (en mayúsculas, sin espacios al borde). No hay validación de cliente (la unicidad de apertura vigente es del servidor).

## Caja > Cierre de caja (`/SUROSFacturacion/Vistas/Privado/Configuracion/ArqueoCaja.aspx`)
- **Propósito**: arqueo/cierre de una o varias cajas.
- **Funcionalidades**:
  - El usuario puede consultar cajas por rango de fechas, seleccionar una o varias (ventanas "Selecciona la caja de tu interés" y "Cajas seleccionadas").
  - El usuario puede consultar el arqueo, exportar, imprimir y guardar el arqueo (cierra la caja, inferido).
- **Datos**: Fecha inicia/final; Cajas seleccionadas; Con valor inicial {SI, No}; Elementos a visualizar (multi) {FACTURA, POS, COPAGO, CUOTA MODERADORA, COPAGO RÉGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS, ANTICIPO, NO APLICA}.
- **Listados**: Cajas seleccionables (Caja, Responsable, Fecha apertura); Arqueo: Tipo Fac, Número copago, Número factura, Fecha registro, No documento, Persona, Empresa, No contrato, Procedimientos, Observación, No. nota crédito, Valor nota crédito, T. facturado, C. recuperado, Subsidiado, Recaudado.
- **Flujos y reglas inferidas**: las notas crédito se descuentan del recaudo (confirmado en código: `renderRecaudado` en Imprimir cierres calcula RECAUDADO - NCDC_VALORUNITARIO).
- **Hallazgos del código**:
  - Seleccionar cajas (`EscribeCajasEnCombobox`): sin selección, "Recuerda seleccionar por lo menos una caja."; el cierre se hace sobre aperturas (`APCA_ID`) con su responsable.
  - Imprimir sin datos: "No hay información para el cierre!".
  - `Calcular` suma el campo Valor del grid en `txtTotal`; al editar (`Validar`) el valor se fuerza a `abs(Valor) x Editable`, o sea que `Editable` aporta el signo (0 = no editable, `Validar2`).
  - "Con valor inicial" SI habilita el saldo de apertura (`HabilitaValorInicial`). Servidor: `SRV.Buscar`, `SRV.Guardar(fechaI, fechaF, valorInicial, elementos, cajas, responsables, aperturas, detalle)`, `SRV.IMPR`.

## Caja > Imprimir cierres (`/SUROSFacturacion/Vistas/Privado/Configuracion/ImprimirArqueos.aspx`)
- **Propósito**: consultar e imprimir cierres/arqueos históricos.
- **Funcionalidades**: el usuario puede consultar por mes/año o rango de fechas y por caja; ver el arqueo (ventana "Arqueo"), exportar e imprimir.
- **Datos**: Opción de fecha {MES, RANGO DE FECHAS}; Año; Mes; Fecha I/F; Cierre de caja (combo de cajas).
- **Listados**: Cierres (Caja, Fecha apertura, Responsable, Documento responsable); detalle (mismas columnas que Arqueo, con "No" y "Fecha").
- **Hallazgos del código**:
  - Imprimir y Exportar exigen un cierre guardado: "Por favor, guarde el cierre para imprimirlo" (`SRV.IMPR`, `SRV.ExportarExcel` con el `APCA_ID`).
  - `AccionFecha`: opción 1 (MES) muestra año y mes; opción 2 (RANGO) muestra fechas. Filas con concepto "SALDO APERTURA" se resaltan (`dirty-row`).

## Homologadores > Homologador (`/SUROSFacturacion/Vistas/Privado/Homologador/Homologador.aspx`)
- **Propósito**: homologar cada CUPS con códigos ISS y SOAT y configurar cómo se factura/reporta (concepto, centro de costos, archivo RIPS).
- **Funcionalidades**:
  - El usuario puede crear, editar, eliminar y refrescar homologaciones; buscar por CUPS (nombre o código) con ventana de coincidencias.
  - El usuario puede cargar masivamente un archivo XLS y crear homologaciones.
  - El usuario puede seleccionar códigos de servicio y entidades a las que aplica (ventana "Seleccionar los códigos de servicio"; limpiar selección).
  - Guardar, aceptar y guardar, salir.
- **Datos**: Código CUPS; ISS (código y valor); SOAT (código y valor); Facturar como {RPMS ciclos 1-6, consulta preconcepcional, prenatal, partos, posparto, recién nacido, consulta externa medicina/odontología/enfermería, atención inmediata, internación, procedimientos externos, imágenes, farmacia, laboratorio, vacunación, medicina especializada, terapias, traslado asistencial, otros}; Concepto {CONSULTAS, PROCEDIMIENTOS (diagnósticos, terapéuticos no quirúrgicos, quirúrgicos, P y P), ESTANCIAS, HONORARIOS, DERECHOS DE SALA, MATERIALES E INSUMOS, BANCO DE SANGRE, PRÓTESIS Y ÓRTESIS, MEDICAMENTOS POS/NO POS, TRASLADO DE PACIENTES, VACUNAS}; Centro de costos; Archivo RIPS {PROCEDIMIENTOS, CONSULTA, OTROS SERVICIOS}; Clasificación {POS, NO POS}; Valor finalidad RPMS (PYP); Plan único de cuentas; Observación; Recomendaciones para realizar el procedimiento.
- **Listados**: Homologaciones (Creación, CUPS, ISS, SOAT, Descripción, Facturar como, Concepto, Centro de costos, Archivo RIPS, Clasificación, Estado, Observación, Recomendaciones); Clasificaciones CUPS (Clasificación específica); selección de servicios (Descripción, Código).
- **Flujos y reglas inferidas**: "Archivo RIPS" decide en cuál archivo RIPS cae cada procedimiento; "Plan único de cuentas" enlaza con contabilidad (inferido).
- **Hallazgos del código**:
  - Validaciones (`guardarHomologacion`): "No ha seleccionado un procedimiento", "No ha seleccionado un código ISS", "No ha seleccionado un código SOAT", "Por favor complete todos los campos". Es decir, CUPS, ISS y SOAT son obligatorios.
  - El grid muestra ISS como "código -(UVR: valor)" y SOAT como "código -(G-QX: valor)": el valor ISS es una UVR y el SOAT un grupo quirúrgico. Estado: "Activo"/"Inactivo".
  - Al elegir el CUPS (`eventoSelecCups`) se cargan sus clasificaciones (`SRV.CargarClasificacionesCups`) y el archivo RIPS y la finalidad PyP (`SRV.FinalidaPyP`). Guardar: `SRV.Guardar` (procedimiento, ISS, SOAT, servicio, concepto, centro de costos, RIPS, clasificación, códigos de servicio, estado, observación, recomendaciones, finalidad PyP, PUC). Carga masiva: `SRV.CargarXLS("PROCEDIMIENTOS QUIRÚRGICOS")`.

## Homologadores > Homologador procedimientos quirúrgicos (`/SUROSFacturacion/Vistas/Privado/Homologador/HomologadorProcedimientosQuirurgicos.aspx`)
- **Propósito**: calcular y guardar el valor de procedimientos quirúrgicos por UVR y manual tarifario, con desglose de honorarios.
- **Funcionalidades**: el usuario puede buscar CUPS, elegir manual y tipo de intervención, calcular valores, aceptar y guardar; crear homologación, refrescar y listar.
- **Datos**: Código CUPS; Tipo intervención {CRUENTOS, INCRUENTOS}; Manual tarifario {ISS 2001, SOAT 2017, 2018, 2019, 2020}; Descripción; UVR; Grupo qx.
- **Listados**: Desglose (Id, Descripción, Código, Nombre del honorario, Valor); Homologaciones (ID, CUPS, Descripción, Manual tarifario, Valor total).
- **Flujos y reglas inferidas**: valor = UVR x valor UVR del manual según grupo quirúrgico, descompuesto en honorarios (cirujano, anestesia, ayudante, sala, materiales) (corregido según código: `iss`/`soat` muestran UVR para ISS y grupo quirúrgico G-QX para SOAT, o sea que cada manual usa una unidad distinta; `PrepararDatos` guarda el desglose del grid `GridManuales`; la fórmula se calcula en el servidor).
- **Hallazgos del código**:
  - Guardar sin filas: "No hay registros para guardar". `SRV.GuardarHomologo(json, manual, procedimiento, mosaId)` guarda la cabecera (HOMOID, PRQUID, MOSAID) y el DETALLE de honorarios.

## Notas crédito > Nota crédito (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCredito.aspx`)
- **Propósito**: emitir nota crédito sobre una factura de un paciente (anulación o ajuste).
- **Funcionalidades**:
  - El usuario puede buscar paciente y su factura (coincidencias; ventana "Soportes factura").
  - El usuario puede ver los datos de la factura electrónica de venta, cliente y paciente.
  - El usuario puede elegir ítems del consolidado/cirugía a acreditar (columna Acción), relacionar copagos y ver el recibo de pago.
  - Guardar la nota; luego enviar (Enviar/Cancelar).
- **Datos**: Documento/Nombre; checkbox Factura; Motivo DIAN {Devolución de parte de los bienes / no aceptación de partes del servicio, Anulación de factura electrónica, Rebaja total aplicada, Descuento total aplicado, Rescisión: nulidad por falta de requisitos, Otros}; Forma de pago {EFECTIVO, TARJETA DE CRÉDITO, TARJETA DÉBITO, CHEQUE, CRÉDITO, CONTADO}; Plazo; Observación; Fecha facturación; Valor total.
- **Listados**: Consolidado (ID, CUM/Cód, Concepto, Observación, Valor real, %, Cantidad, Valor/U, Descuento, Valor total, Acción); Cirugía; Recibo de pago (Caja, Concepto, Forma de pago, Cantidad, Valor a pagar, Total a pagar, Total pago, Saldo); copagos (ID, cita, copago).
- **Flujos y reglas inferidas**: el motivo DIAN sigue la tabla de conceptos de corrección de nota crédito (confirmado en código: `validarComboMotivoDian`; norma: anexo técnico de factura electrónica de la DIAN, concepto 2 = anulación); la forma de pago/plazo aplica al crédito (confirmado en código: `GuardarNotaCredito` exige forma de pago y plazo, aunque la semántica de crédito es del servidor).
- **Hallazgos del código**:
  - Validaciones (`GuardarNotaCredito`): "Por favor <strong>Ingrese el MOTIVO!</strong>", "...Ingrese la forma de pago!", "...Ingrese la fecha del la nota!", "...Ingreseel plazo!". `SRV.GuardarNotacredito` recibe FAINID, fecha, motivo, observación, plazo, forma de pago y los detalles de consolidado, cirugía, copago y copago nuevo.
  - Con motivo 2 (anulación) se cargan todos los ítems de la factura con sus valores (`actualizarInputsDesdeStore`); con otro motivo se limpian y el usuario acredita ítem por ítem (`limpiarInputs`).
  - Cálculo por línea (`calculartotaldetalle`, `calcularvalorciruj`): `(valor unitario x cantidad - descuento) x (1 + incremento/100)`. Recibo (`calcularvalortotalcopago`): total a pagar = cantidad x valor; saldo = total a pagar - total pagado. Total de la nota (`calcularvalortotalfact`) = consolidado + cirugía + total a pagar de copagos; usa `parseInt`, o sea que trunca decimales.
  - Envío: `enviarnotadian` -> `SRV.EnviarNotaDian({FAIN_ID, NOCDID})`. El progreso del envío a NEOSAGE se muestra por SignalR (hub `NEO_NOTIFICACIONES`; estados ENVIANDO, ENVIADO/EXITOSO, ERROR/NOVEDAD; mensajes "✓ Nota enviada a NEOSAGE exitosamente" / "✗ Error NEOSAGE: ...").
  - Búsqueda: `SRV.Buscar(texto, porFactura)`.

## Notas crédito > Listado notas crédito (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCredito.aspx`)
- **Propósito**: consultar, enviar a la DIAN e imprimir notas crédito.
- **Funcionalidades**: consultar por número de factura, número de nota o rango de fechas; generar Nota Crédito Electrónica (envío a la DIAN con reporte de enviadas/fallidas); exportar a Excel; imprimir nota y factura relacionada; "Validar al Ministerio" (ventana Validar RIPS con credencial WebSisPro, JSON de la nota).
- **Datos**: Consultar por {Numero Factura, Numero Nota, Rango de Fechas}; Número factura; Número nota; Fecha inicio/fin.
- **Listados**: Reporte Notas Crédito: CUV, Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota. Grid de impresión (Descripción, Carta).
- **Flujos y reglas inferidas**: la nota recibe CUV tras validación del Ministerio (confirmado en código: `ValidarRipsSispro` -> `SRV.ValidacionNotaCreditoEvento` y `ValidadaRips` sobre `FAIN_CUV`).
- **Hallazgos del código**:
  - Enviar: "Está seguro de enviar esta nota credito?" -> `SRV.EnviarNotaDian`; imprimir nota `SRV.ImprUnaNota`; factura `SRV.ImprUnaFactura`; Excel `SRV.Exportar`. Validar al Ministerio: `SRV.ValidacionNotaCreditoEvento` con las mismas credenciales SISPRO y `VerificarEstado`. Color de fila por `ELECTRONICA`.

## Notas crédito > Nota crédito global (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCreditoGlobal.aspx`)
- **Propósito**: nota crédito sobre una factura global.
- **Funcionalidades**: buscar por número de factura global; ver datos de factura y cliente; agregar recibo de pago a la nota; relacionar copago; guardar; enviar.
- **Datos**: Número de factura global; Factura; Motivo DIAN (mismos valores que nota crédito); Forma de pago; Plazo; Recibo: Forma de pago {Efectivo}, Concepto pago {COPAGO, CUOTA MODERADORA, COPAGO RÉGIMEN SUBSIDIADO, PAGOS COMPARTIDOS, ANTICIPO, NO APLICA}, Cantidad, Valor unitario, Valor total, Observación; Fecha facturación; Observación; Valor total.
- **Listados**: Consolidado (ID, Cód, Concepto, Observación, Cantidad, Valor/U, Valor total); Recibo de pago (Concepto, Forma de pago, Cantidad, Valor unitario, Valor total).
- **Hallazgos del código**:
  - Mismas validaciones y cálculos que la nota individual (motivo, forma de pago, fecha, plazo; total = consolidado + recibos). Búsqueda `SRV.Buscar(texto)`, `SRV.GuardarNotacredito`, `SRV.EnviarNotaDian` y listener NEOSAGE por SignalR.

## Notas crédito > Listado nota crédito global (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCreditoGlobal.aspx`)
- **Propósito**: igual que el listado de notas crédito, para globales.
- **Funcionalidades**: consultar por factura/nota/fechas; nota crédito electrónica (reporte enviadas/fallidas); imprimir nota y factura relacionada; validar al Ministerio (ventana Validar RIPS).
- **Datos**: Consultar por {Numero Factura, Numero Nota, Rango de Fechas}; números; fechas.
- **Listados**: Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota (sin columna CUV, a diferencia del individual).
- **Hallazgos del código**:
  - Enviar: "Está seguro de enviar esta nota credito?"; abre la nota global con `abrirNotaGlobalEnVentana(fagoId, ncdgId, numNota)`; mismo manejo de credenciales SISPRO.

## Notas débito > Notas débito (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaDebito.aspx`)
- **Propósito**: emitir nota débito sobre una factura para sumar valores (intereses, gastos, cambio de valor).
- **Funcionalidades**:
  - El usuario puede buscar paciente y factura, ver soportes.
  - El usuario puede agregar ítems: Asistencial (procedimientos con homólogo), Recibo de pago, Medicamentos, Insumos, Cirugía, RPMS; con credenciales para duplicados.
  - Cirugía con equipo (cirujano, anestesiólogo, ayudante), tipo de cirugía y anestesia, vía de acceso, CIE10 y procedimientos.
  - Relacionar/crear copago; guardar y enviar.
- **Datos**: Motivo DIAN {Intereses, Gastos por cobrar, Cambio del valor, Otro}; Forma de pago {EFECTIVO, TARJETA DE CRÉDITO, TARJETA DÉBITO, CHEQUE, CRÉDITO, CONTADO}; Plazo; No autorización; Cantidad, Valor/U, Valor total, Comisión, Descuento, Observación; datos de medicamento (Cum, valor real), insumo (código); cirugía con tipos como en facturador V2; Fecha facturación; Valor total.
- **Listados**: Consolidado, Cirugía, Recibo de pago (Caja, Concepto, Forma de pago, Cantidad, Valor, Total a pagar, Total pago, Saldo), homólogos ISS/SOAT.
- **Hallazgos del código**:
  - Validaciones de guardado idénticas a la nota crédito ("Ingrese el MOTIVO!", forma de pago, fecha, plazo) vía `SRV.GuardarNotaDebito`; la cirugía exige cirujano, anestesiólogo, ayudante, tipo de cirugía, anestesia, fecha, vía de acceso, procedimiento y diagnóstico. CIE10 duplicado: "El diagnostico con código CIE10 <b>X</b> ya está en la lista.".
  - Total (`calcularvalortotalfact`) = consolidado + cirugía + total pagado de recibos (`TOTALPAGO`), a diferencia de la nota crédito que suma `TOTALPAGAR`.
  - Envío `SRV.EnviarNotaDian` con progreso NEOSAGE por SignalR; `SRV.Buscarultimafact` para la última factura del paciente.

## Notas débito > Listado notas débito (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasDebito.aspx`)
- **Propósito**: consultar y enviar notas débito.
- **Funcionalidades**: consultar por factura/nota/fechas; Nota Débito Electrónica (reporte enviadas/fallidas a la DIAN); imprimir nota y factura relacionada.
- **Listados**: Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota.
- Nota: no tiene "Validar al Ministerio" ni Excel (a diferencia de crédito).
- **Hallazgos del código**:
  - Enviar: "Está seguro de enviar esta nota Debito?" -> `SRV.EnviarNotaDian`; sin validación SISPRO ni Excel (confirmado: no hay funciones de ese tipo en la pantalla).

## Contratación (`/SUROSFacturacion/Vistas/Privado/Contratos/ListaContratos.aspx`)
- **Propósito**: administrar contratos con empresas (EPS/aseguradoras): servicios, tarifas, sub planes, anexos (otro sí), soportes de factura y reglas de facturación por instancia.
- **Funcionalidades**:
  - El usuario puede listar contratos, filtrar por estado y texto, crear contrato, refrescar.
  - Crear Otro Sí (número, fechas, valor, objeto) y ver el objeto del contrato (ventana "Detalle objeto del contrato").
  - Agregar servicios al contrato ("Asignar servicio a contrato") con tipo de atención, manual tarifario, incremento, valor, definición de ingreso, estado, especialidad; listar y editar servicios del contrato.
  - Cargar archivo de precios: contenido {PROCEDIMIENTOS, MEDICAMENTOS, INSUMOS}, acción {AGREGAR, NO AGREGAR}, grupos del contrato; descargar archivos de ejemplo; resultado con paneles Actualizados / Completos nuevos / No actualizados y exportar.
  - Gestionar grupos de tarifa propia: nuevo, editar, eliminar grupo, ítems del grupo, filtrar por estado.
  - Ítem de tarifa propia: nombre, CUMM, consecutivo, grupo, modalidad de cobro {Paquete, Costo fijo, Manual tarifario, Incremento, Costo fijo externo}, valor fijo; actualizar información; clasificación RIPS.
  - Agregar sub planes al contrato (incluidos, ID único, nombre; seleccionar todos).
  - Configurar archivos de soporte por contrato (ID, nombre, obligatorio, grupo, sigla, activo); agregar archivo soporte (nombre, tipo {COLUMNA, SCRIPT}, columna o script) y configuración de generación de PDF; lista de chequeo de soportes.
  - Configurar tiempo de instancia (facturación de larga instancia): instancia {OBSERVACIÓN, HOSPITALIZACIÓN, AFINAMIENTO}, procedimiento con el que se factura, condición {DURACIÓN, CANTIDAD EVOLUCIONES, ESPECIALIDAD, ORDEN HOSPITALIZACIÓN, ANEXO} con rangos inicial/final, cantidad, especialidades, orden obligatoria.
- **Datos**: Estado de contratos {ACTIVO, CANCELADO, EJECUTADO, EN EJECUCIÓN, INACTIVO, LIQUIDADO}; búsqueda; campos del contrato (campos sin etiqueta en la ventana "Crear Contrato", no identificables); Servicio: nombre, título, tipo de atención, manual tarifario, incremento, valor, definición de ingreso (multi), estado {ACTIVO, INACTIVO}.
- **Listados**: Contratos (información, fechas, valor, Id, empresa contratante, estado, otro sí); Servicios del contrato (Id, fecha creación, nombre, manual tarifario, incremento, valor, definición ingreso, estado); Tiempo instancia (Id, modalidad cobro, condición, valor condición, código, descripción); Grupos (nombre, concepto, estado); Ítems (descripción, clasificación RIPS, estado/clasificación); Soportes (ID, nombre, obligatorio, grupo, sigla, activo); Lista de chequeo (nombre).
- **Flujos y reglas inferidas**: el contrato define qué servicios se pueden facturar y a qué tarifa (manual + incremento o valor fijo o paquete) (confirmado en código: `selectIncremento` — "SIN INCREMENTO" fija el valor en 0 y lo bloquea; con incremento el valor mínimo es 1; `eventoSelect` arma el título del servicio con sus especialidades). Subplanes segmentan la cobertura. Soportes obligatorios por contrato se adjuntan a la factura (confirmado en código parcialmente: `DescargarSoporte`/`ConsultarArchivos` de la factura global descargan soportes por TIPO, FACTURA e ID; el bloqueo por soporte obligatorio faltante no está en el cliente).
- **Hallazgos del código**:
  - Campos del contrato visibles en el listado: CUCON (`CONT_CUCON`), descripción, número, tipo, lugar de ejecución, fecha de creación, inicio y fin, "COBERTURA PLAN BENEFICIOS" (`COPL_NOMBRE`), valor del contrato, valor total, número de afiliados, y contratante(s) con nombre, NIT y régimen (un contrato puede tener varias empresas contratantes). Estados filtrables vía `SRV.BindData`.
  - Servicio: no se repite una especialidad ("La especialidad <b>X</b>, ya se encuentra en la lista"). Subplanes: `EnviarSubPlanesContrato` manda solo los modificados, agregados y eliminados (`SRV.ActualizarSubPlanesContrato`), por servicio.
  - Carga de precios: si la acción es 1 (AGREGAR) se pide el grupo destino (`SRV.ConsultaGruposWinPrecion`); resultado en grids Actualizados, Insertados y Errores (`SRV.ExportarResultado`); ejemplos con `SRV.DescargarArchivosMasivos`.
  - Archivos de soporte: tipo 1 = columna (`SRV.CargarColumnasArchivoSoporte`), tipo 2 = script SQL (`SRV.CargarSQLSArchivoSoporte`); se guarda con `SRV.GuardarParametroSoporteCuenta`.
  - Tiempo de instancia: el tipo de condición JSON, RANGO, CANTIDAD o APLICA (`CargarItemCondicionesTipo`) decide qué campos se muestran.
  - Otro sí y objeto: `SRV.VerObjetoContrato`.

## Parámetros de facturación (`/SUROSFacturacion/Vistas/Privado/Configuracion/ParametroFactura.aspx`)
- **Propósito**: configurar resoluciones de numeración y documentos por prestador.
- **Funcionalidades**: el usuario puede listar, editar y crear parámetros de factura, activar/desactivar, asociar prestadores de servicio (con código de habilitación) y ver resoluciones disponibles; guardar/cancelar.
- **Datos**: Resolución; Descripción de la resolución; Pie de página; Texto anexo; Prefijo inicio/fin; No. inicial/final; No. inicio factura; Estado; Fecha vigencia; Fecha vencimiento; Tipo de factura {POS, FACTURA ELECTRÓNICA DE VENTA, DOCUMENTO DE COTIZACIÓN, PREFACTURA, DOCUMENTO SOPORTE, POS ELECTRÓNICA, NOTA CRÉDITO/DÉBITO FACTURA, NOTA CRÉDITO/DÉBITO DOCUMENTO SOPORTE, NOTA CRÉDITO/DÉBITO DOCUMENTO EQUIVALENTE}.
- **Listados**: Parámetros (ID, Resolución, Prefijo, Numeración, Vigencia); Prestador de servicio de la resolución (Prestador, Código habilitación); Resoluciones disponibles (Resolución, Prefijo).
- **Flujos y reglas inferidas**: cada tipo de documento tiene su resolución/rango; el sistema avanza el consecutivo y bloquea al agotar rango o vencer fecha (inferido).
- **Hallazgos del código**:
  - Validaciones (`GuardarParametro`): "Por favor <strong>Ingrese una resolución de la DIAN!</strong>", "...<strong>Ingrese el número inicial</strong>", "...<strong>Ingrese el número final</strong>". La comparación "El número final no puede ser menor al número inicial" está comentada: no se valida en el cliente.
  - `SRV.GuardarParametro` recibe resolución DIAN, pie de página, anexo, prefijo inicio/fin, rango numérico, vigencia y vencimiento (fechas `Y/m/d`), número de inicio de factura (consecutivo de arranque), estado, tipo de documento (`TIFA`) y descripción.

---

## Ciclo de facturación (inferido)
1. **Contrato**: se crea el contrato con la EPS/aseguradora (Contratación): servicios, manual tarifario/incremento/paquete, subplanes, soportes y reglas de larga instancia. Homologador relaciona CUPS con ISS/SOAT y define concepto, centro de costos y archivo RIPS.
2. **Parámetros**: resoluciones DIAN por prestador y tipo de documento.
3. **Ingreso/atención** (módulos asistenciales, fuera de este archivo): los ingresos quedan sin facturar; el paciente puede pagar copago/cuota moderadora en caja.
4. **Factura**: Facturador manual V2 (paciente), Facturador automático (lote) o Factura global (empresa/periodo). Se capturan servicios, medicamentos, insumos, cirugía, estancias, paquetes, diagnósticos, autorización/MIPRES, recibos de pago y, si aplica, FURIPS.
5. **Validación y envío**: validar RIPS (WebSisPro/Ministerio, CUV), facturar electrónicamente y enviar a la DIAN; ver enviadas/fallidas; XML electrónico; opcionalmente enviar a NEOSAGE.
6. **Ajustes**: nota crédito (anulación, rebaja, devolución) o nota débito (intereses, gastos, cambio de valor), individual o global; también se envían a la DIAN.
7. **RIPS**: Generador RIPS por empresa, contrato, subplan y periodo, con códigos CUPS o SOAT.
8. **Caja**: apertura con valor inicial, recaudo de copagos/cuotas/anticipos/POS, arqueo y cierre, impresión histórica de cierres.

## Entidades y estados
- **Factura**: prefijo + número, resolución, tipo (electrónica, POS, prefactura, cotización, documento soporte); estado visible (valores no listados), "Validada RIPS", enviada/fallida a la DIAN, CUV.
- **Prefactura / cotización / factura global**; **Nota crédito**, **Nota débito** (individuales y globales).
- **Ingreso** (con fechas, causa externa, destino, diagnósticos), **Ítem de factura** (procedimiento, medicamento, insumo, estancia, cirugía, paquete).
- **Recibo de pago / copago**, **Caja**, **Apertura**, **Arqueo/Cierre**.
- **Contrato** (estados: ACTIVO, CANCELADO, EJECUTADO, EN EJECUCIÓN, INACTIVO, LIQUIDADO), **Otro sí**, **Servicio del contrato**, **Grupo de tarifa propia**, **Subplan**, **Archivo de soporte**.
- **Homologación** (CUPS-ISS-SOAT), **Homologación quirúrgica** (UVR, grupo qx, honorarios).
- **Parámetro de factura/resolución**, **Prestador** (sede con código de habilitación), **Empresa/EPS**, **Paciente**, **Médico**.
- Estados simples: Activo/Inactivo (servicios, grupos, parámetros).

## Integraciones externas visibles
- **DIAN**: factura electrónica de venta, notas crédito/débito electrónicas, copago electrónico, documento soporte, POS electrónico; XML electrónico; resoluciones de numeración; motivos DIAN.
- **RIPS / Ministerio de Salud**: generación de archivos RIPS, validación vía WebSisPro con credencial, CUV (carga TXT/JSON), "Validar al Ministerio", archivos RIPS por homologador.
- **NEOSAGE**: sistema externo al que se envían facturas y notas y del que se toma un catálogo de productos para la factura global; el avance del envío llega por SignalR (hub `NEO_NOTIFICACIONES`); su función contable se deduce del nombre `EnviarContable` (confirmado en código).
- **MIPRES** (prescripción de tecnologías no cubiertas), **CIE10**, **CUPS**, **CUM** (medicamentos), **SIRAS**, **FURIPS/SOAT** (ADRES), manuales tarifarios ISS 2001 y SOAT 2017-2020, Res. 1557 (documento).
- Excel (importaciones y exportaciones), PDF/ZIP.

## Preguntas abiertas

### Respondidas
1. **¿Cómo se ejecuta el Facturador automático y qué criterios usa?** No factura en lote: el árbol abre los módulos en pestañas con el rango de fechas (código: `NodoClic`, `SRV.GuardarFechas`); lo único masivo es la exportación de ingresos sin factura (código: `ExportarSinFactura`).
2. **¿Qué es "Convertir a factura" y qué estados tiene una factura?** Cambia el tipo de documento de una factura no electrónica (código: `ConvertirDocumento` -> `SRV.CambiarDocumento`; `showMenu` lo oculta si ya es electrónica). Estados visibles en el cliente: electrónica (fila verde `#EBFFE1`), con o sin CUV ("Validada"/"No Validada", código: `ValidadaRips`), enviada o fallida a la DIAN.
3. **¿Qué es NEOSAGE y qué datos recibe?** Sistema externo, de naturaleza contable según el nombre `EnviarContable`, que recibe facturas y notas con notificación de avance en tiempo real y entrega un catálogo de productos (código: `startNeosageListener`, `SeleccionarProductoNeosage`). El contenido exacto de lo enviado es del servidor.
4. **¿Qué es "Editar documento Res. 1557"?** Abre el editor antiguo `EditorFacturador.aspx` en lugar de `EditorFacturadorV2.aspx` (código: `AbrirEditorFacturas1557`).
5. **¿Cómo se calcula el valor de una línea?** En notas: `(unitario x cantidad - descuento) x (1 + incremento/100)` (código: `calculartotaldetalle`); recibo: saldo = cantidad x valor - total pagado (código: `calcularvalortotalcopago`); factura global: total = consolidado - recibos (código: `AgregarRowGridpanel`).
6. **¿Qué reglas aplican a las credenciales para duplicados y a WebSisPro?** Usuario y contraseña del sistema validados en el servidor (código: `VP` -> `SRV.HE`); para SISPRO se elige una credencial guardada y se consulta si está "autenticado." (código: `verificarEstadoCredenciales`, `SRV.ConectarSispro`). Las reglas de rol quedan en el servidor.
7. **¿Cómo se parametriza el honorario quirúrgico?** El manual ISS usa UVR y el SOAT un grupo quirúrgico (G-QX), con desglose por honorario guardado desde el grid `GridManuales` (código: `iss`, `soat`, `PrepararDatos`).
8. **¿Qué es el CUV y cuándo se valida?** Código Único de Validación devuelto por el Ministerio; la fila se marca "Validada" si `FAIN_CUV` no está vacío (código: `ValidadaRips`). "Validar RIPS" se ofrece solo en facturas electrónicas sin CUV con fecha desde 2025-04-01 (código: `showMenu`). Estructura de RIPS y validación (norma: Res. 2275/2023).
9. **¿Un copago puede ir a la DIAN?** Sí, con un parámetro de resolución propio (código: `ConvertirDianCopago` -> `SRV.FacturaElectronicaCopago`).
10. **¿Los motivos de nota crédito/débito son los de la DIAN?** Sí, los conceptos de corrección del anexo técnico de factura electrónica (norma: Res. DIAN 000165/2023); con motivo 2 (anulación) se carga la factura completa (código: `validarComboMotivoDian`).
11. **¿Qué son copagos y cuotas moderadoras y se calculan en el cliente?** Son pagos del usuario modelados como conceptos del recibo de pago (código: lista de conceptos de `Recibo`); su regulación general es el Acuerdo 260/2004 (norma: Acuerdo 260/2004). Los montos no se calculan en el cliente.
12. **¿Dónde se gestionan glosas y radicación?** Ninguna función de glosa o radicación aparece en los JS de este módulo (código: ausencia en las pantallas revisadas); se asume que viven en otro módulo de cartera (supuesto estándar del sector).

### Sin respuesta por ingeniería inversa
1. ¿Cuál es el listado completo de estados de una factura (borrador, anulada, glosada)? Lógica del servidor.
2. ¿Qué cubre exactamente "Res. 1557" y por qué se conserva un editor separado? Decisión del negocio.
3. ¿Qué campos tiene "Crear Contrato" y cómo se calcula el valor con paquete, costo fijo externo y PGP o capitación? Lógica del servidor (el formulario no está en el JS).
4. ¿Cuándo se cierra definitivamente una caja y qué pasa con la apertura vigente al guardar el arqueo? Lógica del servidor.
5. ¿Qué regla bloquea el consecutivo al agotar el rango o vencer la resolución (el cliente no valida número final menor que inicial)? Lógica del servidor.
6. ¿Cómo se calculan los montos de copago y cuota moderadora según categoría de afiliación? Lógica del servidor y requiere paciente real.
7. ¿Qué condiciona que aparezca el panel SOAT/FURIPS (`AplicaSoat`) y cómo se decide "no se pueden facturar" por homólogo? Lógica del servidor.
8. ¿Qué hace el servidor con el archivo CUV (TXT/JSON) de la factura global? Sin acceso (no hay función en el JS).
9. ¿Qué datos exactos envía "Enviar a NEOSAGE" desde el listado de facturas, que en el cliente no llama al servidor? Sin acceso.
10. ¿La validación de hora de egreso omitida y el mensaje repetido de "causa externa" en estado de salida son errores conocidos o intencionales? Decisión del negocio.
