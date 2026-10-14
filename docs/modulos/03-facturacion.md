# Facturación

Módulo de facturación de SURÓS/PRORED (`/SUROSFacturacion/Vistas/Privado/...`). Cubre: administración y consulta de facturas, generación de facturas (global, automática, manual V2), facturación electrónica ante la DIAN, generación y validación de RIPS, caja (apertura, arqueo, cierres), homologadores de manuales tarifarios con CUPS, notas crédito y débito (individuales y globales), contratación con EPS/aseguradoras y parámetros de resoluciones/numeración. Todo se deriva de una extracción de UI; las reglas de negocio son inferidas. Documentación de 19 pantallas.

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
- **Flujos y reglas inferidas**: los campos visibles dependen del criterio elegido (inferido). Existe el concepto de PREFACTURA previa a la factura (inferido).

## Admón. Facturación > Generador RIPS (`/SUROSFacturacion/Vistas/Privado/Rips/GeneradorRips.aspx`)
- **Propósito**: generar los archivos RIPS por empresa/contrato y periodo.
- **Funcionalidades**:
  - El usuario puede filtrar y consultar los registros a incluir.
  - El usuario puede importar un archivo (`BTN_IMPORTAR`) para acotar la selección (inferido).
  - El usuario puede generar RIPS (ventana "Generar RIPS", botón Aceptar).
- **Datos**: Prestador del servicio (multi, TODOS); Empresa {Particular-Otro, Asmet Salud subsidiado, Asmet Salud contributivo}; Contrato; SubPlan (multi, TODOS); Clasificación {TODOS, POS, NO POS}; Fecha inicial; Fecha final; Generar códigos como {CUPS, SOAT}.
- **Flujos y reglas inferidas**: el contrato depende de la empresa; el subplan del contrato (inferido). La opción CUPS/SOAT decide el manual de codificación que sale en el archivo.

## Admón. Facturación > Listado facturas (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteFacturasContrato.aspx`)
- **Propósito**: reporte central de facturas por contrato con acciones de facturación electrónica, RIPS y notas.
- **Funcionalidades**:
  - El usuario puede consultar facturas por prestador, empresa, estado del contrato, contrato, subplan, rango de fechas y tipo de programa especial.
  - El usuario puede exportar el listado a Excel o las facturas a PDF (`drpTipoExporte`), y elegir formato: un solo PDF, ZIP por paciente o ZIP por factura; con selección de archivos a imprimir (Ítems del archivo: Descripción, Adjuntar; "Todo carta").
  - El usuario puede obtener el XML electrónico.
  - Sobre facturas seleccionadas: Facturar electrónicamente, Imprimir factura, Convertir a factura, Editar documento, Editar documento Res. 1557, Enviar a la DIAN, Enviar a NEOSAGE, Validar RIPS, Validar RIPS sin factura, Generar nota crédito.
  - Ventana "Seleccione resolución" para escoger la resolución con la que se emite.
  - Ventana "Reporte Envío Factura Electrónica": resultado con facturas enviadas a la DIAN y facturas fallidas (número).
  - Ventana "Validar RIPS": elegir credencial WebSisPro y VALIDAR (validación contra servicio externo del Ministerio, inferido); campos ocultos con ids de factura/procedimiento/paciente para "solo procedimiento" (JSON y N).
- **Datos**: Prestador (multi); Empresa; Estado contrato {ACTIVOS, INACTIVOS, TODOS}; Contrato; Subplan (multi); Fecha inicio/fin; Tipo programa especial {TODAS, NO APLICA, APS, BRIGADAS, PIC, SUBSIDIO A LA OFERTA, OTROS, BAJA COMPLEJIDAD, MEDIANA COMPLEJIDAD}; Tipo exporte; Tipo (PDF/ZIP).
- **Listados**: Reporte Facturas: Validada RIPS, Prefijo, Número, Tipo doc., Documento, Nombre, Empresa, Tipo afiliación, Prestador, Contrato, Fecha facturado, Fecha ingreso, Fecha egreso, Copago, Cuota moderadora, Pagos compartidos en planes voluntarios, Anticipo, No aplica, Valor total, Subplan, Realizado por, Cod. Diag, Descripción, Médico.
- **Flujos y reglas inferidas**: "Convertir a factura" transforma una prefactura/cotización en factura (inferido). "Enviar a NEOSAGE" sugiere integración con un sistema contable/ERP externo (inferido). Marca "Validada RIPS" por factura. Res. 1557 (inferido: formato de documento por esa resolución).

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
- **Flujos y reglas inferidas**: total = suma del consolidado menos recibos de pago (inferido). El archivo CUV sugiere validación del Ministerio de Salud (CUV = código único de validación RIPS/factura) (inferido).

## Generar facturas > Facturador automático (`/SUROSFacturacion/Vistas/Privado/Facturacion/ListaIngresos.aspx`)
- **Propósito**: facturar en lote los ingresos pendientes a una fecha y listar pacientes sin facturar.
- **Funcionalidades**:
  - El usuario puede definir "Fecha a facturar" y una fecha fin, y filtrar con un trigger field (empresa/contrato, inferido) y un árbol de informes (`TreeMenuInformes`).
  - El usuario puede exportar pacientes sin facturar por rango de fechas (panel dedicado; botón Exportar) y elegir ítems de impresión (Descripción, Check).
  - Pestaña "Facturación Surós" y formulario "Listado de servicios".
- **Datos**: Fecha a facturar; Fecha fin; Rango de fechas; Fecha fin ingreso sin facturar.
- **Listados**: Ítems de impresión (Descripción, Check).
- **Flujos y reglas inferidas**: el proceso toma ingresos cerrados no facturados y emite facturas masivas (inferido; la extracción no muestra botón explícito de ejecución).

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
  - Ingresar credenciales (usuario/contraseña) para agregar un procedimiento ya existente en la lista (override con autorización, inferido).
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
  - El valor de cada ítem sale del manual tarifario/contrato (homólogo ISS o SOAT con incremento) (inferido).
  - Procedimientos sin homólogo o sin cobertura quedan en "Procedimientos que no se pueden facturar" (inferido).
  - Agregar un procedimiento duplicado exige credenciales de usuario autorizado (inferido).
  - Paquetes de partos relacionan facturas previas (inferido).
  - Copago puede enviarse como documento electrónico a la DIAN (ventana "Enviar copago a Dian").
  - FURIPS solo aplica cuando la cobertura es SOAT/evento catastrófico (inferido). Panel "Información Soat - Si aplica".
  - Flujo de cierre: pre-validar RIPS, preguntar si se factura electrónicamente, elegir resolución, imprimir (inferido).

## Caja > Apertura de caja (`/SUROSFacturacion/Vistas/Privado/Configuracion/AperturaCaja.aspx`)
- **Propósito**: crear cajas y registrar su apertura con valor inicial.
- **Funcionalidades**:
  - El usuario puede crear una caja (ventana "Caja": nombre; agregar/cancelar).
  - El usuario puede abrir una caja seleccionando caja, funcionario, fecha/hora, valor inicial y observaciones, y guardar la apertura.
  - Ver cajas y aperturas registradas.
- **Datos**: Nombre (caja); Caja (combo con cajas por sede y por cajero/farmacia, nombres de personas omitidos); Funcionario; Fecha/Hora; Valor; Observaciones.
- **Listados**: Cajas (Código, Nombre, Estado); Aperturas (Código, Caja, Responsable, Fecha, Valor, Observaciones, Estado).
- **Flujos y reglas inferidas**: una caja tiene un responsable y estado abierta/cerrada; solo una apertura vigente por caja (inferido). Hay cajas por ciudad, por recepción y por farmacia.

## Caja > Cierre de caja (`/SUROSFacturacion/Vistas/Privado/Configuracion/ArqueoCaja.aspx`)
- **Propósito**: arqueo/cierre de una o varias cajas.
- **Funcionalidades**:
  - El usuario puede consultar cajas por rango de fechas, seleccionar una o varias (ventanas "Selecciona la caja de tu interés" y "Cajas seleccionadas").
  - El usuario puede consultar el arqueo, exportar, imprimir y guardar el arqueo (cierra la caja, inferido).
- **Datos**: Fecha inicia/final; Cajas seleccionadas; Con valor inicial {SI, No}; Elementos a visualizar (multi) {FACTURA, POS, COPAGO, CUOTA MODERADORA, COPAGO RÉGIMEN SUBSIDIADO, PAGOS COMPARTIDOS EN PLANES VOLUNTARIOS, ANTICIPO, NO APLICA}.
- **Listados**: Cajas seleccionables (Caja, Responsable, Fecha apertura); Arqueo: Tipo Fac, Número copago, Número factura, Fecha registro, No documento, Persona, Empresa, No contrato, Procedimientos, Observación, No. nota crédito, Valor nota crédito, T. facturado, C. recuperado, Subsidiado, Recaudado.
- **Flujos y reglas inferidas**: las notas crédito se descuentan del recaudo (inferido por las columnas).

## Caja > Imprimir cierres (`/SUROSFacturacion/Vistas/Privado/Configuracion/ImprimirArqueos.aspx`)
- **Propósito**: consultar e imprimir cierres/arqueos históricos.
- **Funcionalidades**: el usuario puede consultar por mes/año o rango de fechas y por caja; ver el arqueo (ventana "Arqueo"), exportar e imprimir.
- **Datos**: Opción de fecha {MES, RANGO DE FECHAS}; Año; Mes; Fecha I/F; Cierre de caja (combo de cajas).
- **Listados**: Cierres (Caja, Fecha apertura, Responsable, Documento responsable); detalle (mismas columnas que Arqueo, con "No" y "Fecha").

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

## Homologadores > Homologador procedimientos quirúrgicos (`/SUROSFacturacion/Vistas/Privado/Homologador/HomologadorProcedimientosQuirurgicos.aspx`)
- **Propósito**: calcular y guardar el valor de procedimientos quirúrgicos por UVR y manual tarifario, con desglose de honorarios.
- **Funcionalidades**: el usuario puede buscar CUPS, elegir manual y tipo de intervención, calcular valores, aceptar y guardar; crear homologación, refrescar y listar.
- **Datos**: Código CUPS; Tipo intervención {CRUENTOS, INCRUENTOS}; Manual tarifario {ISS 2001, SOAT 2017, 2018, 2019, 2020}; Descripción; UVR; Grupo qx.
- **Listados**: Desglose (Id, Descripción, Código, Nombre del honorario, Valor); Homologaciones (ID, CUPS, Descripción, Manual tarifario, Valor total).
- **Flujos y reglas inferidas**: valor = UVR x valor UVR del manual según grupo quirúrgico, descompuesto en honorarios (cirujano, anestesia, ayudante, sala, materiales) (inferido).

## Notas crédito > Nota crédito (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCredito.aspx`)
- **Propósito**: emitir nota crédito sobre una factura de un paciente (anulación o ajuste).
- **Funcionalidades**:
  - El usuario puede buscar paciente y su factura (coincidencias; ventana "Soportes factura").
  - El usuario puede ver los datos de la factura electrónica de venta, cliente y paciente.
  - El usuario puede elegir ítems del consolidado/cirugía a acreditar (columna Acción), relacionar copagos y ver el recibo de pago.
  - Guardar la nota; luego enviar (Enviar/Cancelar).
- **Datos**: Documento/Nombre; checkbox Factura; Motivo DIAN {Devolución de parte de los bienes / no aceptación de partes del servicio, Anulación de factura electrónica, Rebaja total aplicada, Descuento total aplicado, Rescisión: nulidad por falta de requisitos, Otros}; Forma de pago {EFECTIVO, TARJETA DE CRÉDITO, TARJETA DÉBITO, CHEQUE, CRÉDITO, CONTADO}; Plazo; Observación; Fecha facturación; Valor total.
- **Listados**: Consolidado (ID, CUM/Cód, Concepto, Observación, Valor real, %, Cantidad, Valor/U, Descuento, Valor total, Acción); Cirugía; Recibo de pago (Caja, Concepto, Forma de pago, Cantidad, Valor a pagar, Total a pagar, Total pago, Saldo); copagos (ID, cita, copago).
- **Flujos y reglas inferidas**: el motivo DIAN sigue la tabla de conceptos de corrección de nota crédito; la forma de pago/plazo aplica al crédito (inferido).

## Notas crédito > Listado notas crédito (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCredito.aspx`)
- **Propósito**: consultar, enviar a la DIAN e imprimir notas crédito.
- **Funcionalidades**: consultar por número de factura, número de nota o rango de fechas; generar Nota Crédito Electrónica (envío a la DIAN con reporte de enviadas/fallidas); exportar a Excel; imprimir nota y factura relacionada; "Validar al Ministerio" (ventana Validar RIPS con credencial WebSisPro, JSON de la nota).
- **Datos**: Consultar por {Numero Factura, Numero Nota, Rango de Fechas}; Número factura; Número nota; Fecha inicio/fin.
- **Listados**: Reporte Notas Crédito: CUV, Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota. Grid de impresión (Descripción, Carta).
- **Flujos y reglas inferidas**: la nota recibe CUV tras validación del Ministerio (inferido por la columna).

## Notas crédito > Nota crédito global (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaCreditoGlobal.aspx`)
- **Propósito**: nota crédito sobre una factura global.
- **Funcionalidades**: buscar por número de factura global; ver datos de factura y cliente; agregar recibo de pago a la nota; relacionar copago; guardar; enviar.
- **Datos**: Número de factura global; Factura; Motivo DIAN (mismos valores que nota crédito); Forma de pago; Plazo; Recibo: Forma de pago {Efectivo}, Concepto pago {COPAGO, CUOTA MODERADORA, COPAGO RÉGIMEN SUBSIDIADO, PAGOS COMPARTIDOS, ANTICIPO, NO APLICA}, Cantidad, Valor unitario, Valor total, Observación; Fecha facturación; Observación; Valor total.
- **Listados**: Consolidado (ID, Cód, Concepto, Observación, Cantidad, Valor/U, Valor total); Recibo de pago (Concepto, Forma de pago, Cantidad, Valor unitario, Valor total).

## Notas crédito > Listado nota crédito global (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasCreditoGlobal.aspx`)
- **Propósito**: igual que el listado de notas crédito, para globales.
- **Funcionalidades**: consultar por factura/nota/fechas; nota crédito electrónica (reporte enviadas/fallidas); imprimir nota y factura relacionada; validar al Ministerio (ventana Validar RIPS).
- **Datos**: Consultar por {Numero Factura, Numero Nota, Rango de Fechas}; números; fechas.
- **Listados**: Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota (sin columna CUV, a diferencia del individual).

## Notas débito > Notas débito (`/SUROSFacturacion/Vistas/Privado/NotaCredito/AgregarNotaDebito.aspx`)
- **Propósito**: emitir nota débito sobre una factura para sumar valores (intereses, gastos, cambio de valor).
- **Funcionalidades**:
  - El usuario puede buscar paciente y factura, ver soportes.
  - El usuario puede agregar ítems: Asistencial (procedimientos con homólogo), Recibo de pago, Medicamentos, Insumos, Cirugía, RPMS; con credenciales para duplicados.
  - Cirugía con equipo (cirujano, anestesiólogo, ayudante), tipo de cirugía y anestesia, vía de acceso, CIE10 y procedimientos.
  - Relacionar/crear copago; guardar y enviar.
- **Datos**: Motivo DIAN {Intereses, Gastos por cobrar, Cambio del valor, Otro}; Forma de pago {EFECTIVO, TARJETA DE CRÉDITO, TARJETA DÉBITO, CHEQUE, CRÉDITO, CONTADO}; Plazo; No autorización; Cantidad, Valor/U, Valor total, Comisión, Descuento, Observación; datos de medicamento (Cum, valor real), insumo (código); cirugía con tipos como en facturador V2; Fecha facturación; Valor total.
- **Listados**: Consolidado, Cirugía, Recibo de pago (Caja, Concepto, Forma de pago, Cantidad, Valor, Total a pagar, Total pago, Saldo), homólogos ISS/SOAT.

## Notas débito > Listado notas débito (`/SUROSFacturacion/Vistas/Privado/Reportes/ReporteNotasDebito.aspx`)
- **Propósito**: consultar y enviar notas débito.
- **Funcionalidades**: consultar por factura/nota/fechas; Nota Débito Electrónica (reporte enviadas/fallidas a la DIAN); imprimir nota y factura relacionada.
- **Listados**: Prefijo nota, Número nota, Prefijo factura, Número factura, Documento, Nombre, Empresa, Régimen, Contrato, Fecha facturado, Fecha nota, Valor total factura, Valor total nota.
- Nota: no tiene "Validar al Ministerio" ni Excel (a diferencia de crédito).

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
- **Flujos y reglas inferidas**: el contrato define qué servicios se pueden facturar y a qué tarifa (manual + incremento o valor fijo o paquete) (inferido). Subplanes segmentan la cobertura. Soportes obligatorios por contrato se adjuntan a la factura (inferido).

## Parámetros de facturación (`/SUROSFacturacion/Vistas/Privado/Configuracion/ParametroFactura.aspx`)
- **Propósito**: configurar resoluciones de numeración y documentos por prestador.
- **Funcionalidades**: el usuario puede listar, editar y crear parámetros de factura, activar/desactivar, asociar prestadores de servicio (con código de habilitación) y ver resoluciones disponibles; guardar/cancelar.
- **Datos**: Resolución; Descripción de la resolución; Pie de página; Texto anexo; Prefijo inicio/fin; No. inicial/final; No. inicio factura; Estado; Fecha vigencia; Fecha vencimiento; Tipo de factura {POS, FACTURA ELECTRÓNICA DE VENTA, DOCUMENTO DE COTIZACIÓN, PREFACTURA, DOCUMENTO SOPORTE, POS ELECTRÓNICA, NOTA CRÉDITO/DÉBITO FACTURA, NOTA CRÉDITO/DÉBITO DOCUMENTO SOPORTE, NOTA CRÉDITO/DÉBITO DOCUMENTO EQUIVALENTE}.
- **Listados**: Parámetros (ID, Resolución, Prefijo, Numeración, Vigencia); Prestador de servicio de la resolución (Prestador, Código habilitación); Resoluciones disponibles (Resolución, Prefijo).
- **Flujos y reglas inferidas**: cada tipo de documento tiene su resolución/rango; el sistema avanza el consecutivo y bloquea al agotar rango o vencer fecha (inferido).

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
- **NEOSAGE**: envío de facturas (sistema externo, naturaleza no explícita).
- **MIPRES** (prescripción de tecnologías no cubiertas), **CIE10**, **CUPS**, **CUM** (medicamentos), **SIRAS**, **FURIPS/SOAT** (ADRES), manuales tarifarios ISS 2001 y SOAT 2017-2020, Res. 1557 (documento).
- Excel (importaciones y exportaciones), PDF/ZIP.

## Preguntas abiertas
1. ¿Cómo se ejecuta realmente el Facturador automático (no hay botón de ejecución visible) y qué criterios usa para agrupar ingresos?
2. ¿Qué es exactamente "Convertir a factura" y qué estados tiene una factura (borrador, prefactura, emitida, anulada, glosada)? El estado del grid no muestra valores.
3. ¿Qué es NEOSAGE y qué datos recibe? ¿Y qué es "Editar documento Res. 1557"?
4. ¿Dónde se gestionan glosas y radicación a la EPS? No aparecen en este módulo (¿módulo de cartera?).
5. ¿Qué campos tiene "Crear Contrato" y cómo se calcula el valor de una línea con incremento/paquete/costo fijo externo y la modalidad PGP (los códigos de contrato sugieren PGP, capitación, evento)?
6. ¿Cómo se relacionan caja, copago y factura (el arqueo mezcla copagos y facturas) y cuándo se cierra definitivamente una caja?
7. ¿Qué rol y reglas de seguridad aplican a las credenciales exigidas para agregar procedimientos duplicados y a la credencial WebSisPro?
8. ¿Cómo se parametriza el cálculo del valor de honorarios quirúrgicos (valor UVR por manual)?
