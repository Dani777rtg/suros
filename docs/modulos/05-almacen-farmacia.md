# Almacén, farmacia e inventarios

Sub-aplicación `/SUROSAlmacen` (entrada `/SUROSAlmacen/Vistas/InicioAlmacen.aspx`) de SURÓS/PRORED. Gestiona catálogos de insumos y medicamentos, el ciclo de compra (plan, orden, recepción), la carga de inventarios en bodega, el traslado a almacenes/farmacia mediante pedidos internos, existencias por lote y vencimiento, la dispensación a pacientes (farmacia) y la solicitud de insumos por enfermería. Incluye terceros (fabricantes, laboratorios, proveedores) y configuración (categorías, presentaciones, centros de costo, estados, almacenes, parámetros). Todo son pantallas Ext.NET con grillas filtrables y ventanas emergentes. Las almacenes observados en combos son "BODEGA PEREIRA" y "FARMACIA PEREIRA" (datos de la instalación).

## Árbol de menú

```
CATALOGOS/
  CATALOGO INSUMOS NUEVO        .../CatalogoBasico/ListarCatalogo.aspx
  CATALOGO MEDICAMENTO NUEVO    .../CatalogoMedicamento/CatalogoMedicamento.aspx
  MEDICAMENTOS                  /SUROSFacturacion/Vistas/Privado/Medicamentos/Medamento.aspx
COMPRAS/
  PLANES DE COMPRA              .../CompraPlan/CompraPlan.aspx
  ORDENES DE COMPRA             .../CompraOrden/CompraOrden.aspx
  SOLICITUDES                   .../InventarioSolicitud/InventarioSolicitudPersonal.aspx
  PEDIDO INTERNO                .../InventarioSolicitud/PedidoInterno.aspx
  DESPACHO PEDIDOS              .../InventarioSolicitud/PedidoInternoDespacho.aspx
INVENTARIOS/
  ACTIVACION DE CARGAS          .../InventarioBodega/ListarOrdenesInventario.aspx
  AJUSTE                        .../InventarioBodega/InventarioAjuste.aspx
  CARGA DE INVENTARIOS          .../InventarioBodega/InventarioBodega.aspx
  INFORMES GASTOS ALMACEN       .../InventarioBodega/InventarioStock.aspx
  OLD/ (carpeta sin hojas listadas)
  EXISTENCIAS EN BODEGA/  INSUMOS | MEDICAMENTOS | SUMINISTROS OFICINA   (.../InventarioBodegaDetalle/InventarioBodega{Insumos,Medicamentos,EquiposOficina}.aspx)
  EXISTENCIAS EN ALMACEN/ INSUMOS | MEDICAMENTOS | SUMINISTROS OFICINA   (.../InventarioDetalle/Inventario{Insumos,Medicamentos,EquiposOficina}.aspx)
TERCEROS/
  FABRICANTES                   .../InventarioItemFabricante/InventarioItemFabricante.aspx
  LABORATORIOS                  .../InventarioItemLaboratorio/InventarioItemLaboratorio.aspx
  PROVEEDORES                   .../InventarioItemProveedor/InventarioItemProveedor.aspx
FARMACIA                        .../SolicitudMedicamentosEInsumos/Farmacia.aspx
ENFERMERIA                      .../InventarioSolicitud/InventarioSolicitudInsumos.aspx
TIENDA EN LINEA                 .../Inventario/TiendaEnLinea.aspx
CONFIGURACION/
  CATEGORIAS                    .../InventarioItemCategoria/InventarioItemCategoria.aspx
  CENTROS DE COSTO              .../ContabilidadCentroCosto/ContabilidadCentroCosto.aspx
  ESTADOS DE PEDIDO             .../InventarioSolicitudEstado/InventarioSolicitudEstado.aspx
  PARAMETROS DE CONFIGURACION   .../ParametroConfiguracion/ParametroConfiguracion.aspx
  PRESENTACIONES                .../InventarioItemPresentacion/InventarioItemPresentacion.aspx
  EMPRESA                       .../Empresa/PanelEmpresas.aspx
  ALMACENES                     .../Almacen/Almacen.aspx
  CANASTAS DE CIRUGIA           .../InventarioSolicitud/CanastasCirugias.aspx
```
(Prefijo `.../` = `/SUROSAlmacen/Vistas/Privado/`.) Todas las hojas fueron extraídas (32 pantallas). Nota: `MEDICAMENTOS` vive en la sub-app Facturación.

---

## Catálogos > Catálogo insumos nuevo (/SUROSAlmacen/Vistas/Privado/CatalogoBasico/ListarCatalogo.aspx)
- **Propósito**: listar el catálogo base de insumos y definir sus mínimos/máximos de stock.
- **Funcionalidades**: El usuario puede filtrar por palabra y por columna; agregar un producto ("Agregar un producto"); abrir "Maximos y minimos" de un producto; editar; recargar.
- **Datos**: ventana *Maximos y minimos*: Minimo, Maximo (numéricos). Alta de producto: campos de texto sin etiqueta en la extracción (no identificables).
- **Listados**: *Listado de productos*: # | CPFR_ID | CODIGO | CATEGORIA | NOMBRE BASE | DATOS ADICIONALES | APLICA PARA | FECHA CREACION | PERSONA (registra) | Valor Minimo | Cantidad Actual | Cantidad Maxima | Opciones. Paginación 1/2/10/20.
- **Flujos y reglas**: mínimo/máximo por producto, comparado con Cantidad Actual (inferido: alertas de reposición). "APLICA PARA" indica a qué tipo de inventario aplica (inferido).

## Catálogos > Catálogo medicamento nuevo (/SUROSAlmacen/Vistas/Privado/CatalogoMedicamento/CatalogoMedicamento.aspx)
- **Propósito**: catálogo maestro de medicamentos con forma farmacéutica, concentración, presentación, volumen, clasificación y principios activos.
- **Funcionalidades**: El usuario puede crear (Nuevo Item), editar, eliminar medicamento; definir máximos y mínimos; gestionar homologaciones; crear en línea formas farmacéuticas, volúmenes, presentaciones y concentraciones; asociar principios activos; buscar por texto.
- **Datos**:
  - *Crear médicamento*: Nombre del medicamento (nombre comercial)*, Concentración*, Forma farmacéutica*, Presentación*, Volumen; Categoría {BIOLOGICO, BIOTECNOLOGICO, SINTESIS QUIMICA, VACUNA, RADIOFARMACO, GAS MEDICINAL, FITOFARMACO}; Clasificación de riesgo {CLASE I, CLASE II A, CLASE II B, CLASE III}; Clasificación ATC {16 grupos: tracto alimentario y metabolismo, sangre, cardiovascular, dermatológicos, genitourinario y hormonas sexuales, preparados hormonales sistémicos, antiinfecciosos, antineoplásicos e inmunomoduladores, musculoesquelético, sistema nervioso, antiparasitarios/insecticidas/repelentes, respiratorio, órganos de los sentidos, varios, cosméticos, alimentos y dietéticos}; Códigos; Principio activo (con botones limpiar/seleccionar); Código IUM primer nivel; Clasificación de reactivos de diagnóstico; Clave.
  - *Nueva Forma Farmacéutica*: Id, Forma, Descripción.
  - *Nuevo Volumen*: Valor, Unidad/medida*.
  - *Nueva Presentación*: Id, Presentación.
  - *Nueva Concentración* (ej. 10GR/25CC): U.M., Operador {+, /, -, *}.
  - *Seleccionar Principios activos*: Ingrese concentración, unidad de medida; grilla Principio Activo | Cantidad | Unidad Medida.
  - *Homologar Medicamento*: medicamento base, "Agregar medicamento homologado", Cantidad, Unidad, Cantidad Excedente; grilla Medicamentos Homologados: Medicamento | Cantidad | Unidad | Cantidad Excedente | Unidad Excedente.
  - *Maximos y minimos*: Minimo, Maximo.
- **Listados**: Id | Nombre del medicamento | forma farmacéutica | Adicionales | Maximos y minimos | Principio Activo (paginación hasta 1000); grilla Clasificación de Reactivos de Diagnóstico: CATEGORIA | DESCRIPCION.
- **Flujos y reglas**: un medicamento se define por nombre + concentración + forma + presentación (+ volumen). La homologación equipara medicamentos con equivalencia en cantidad/unidad y excedente (inferido: sustitución en dispensación). Botón "Guardar y Aplicar" tras crear catálogos auxiliares (inferido: el nuevo valor queda disponible en el combo).

## Catálogos > Medicamentos (/SUROSFacturacion/Vistas/Privado/Medicamentos/Medamento.aspx)
- **Propósito**: lista simple de nombres de medicamento y su principio activo (catálogo de Facturación).
- **Funcionalidades**: El usuario puede agregar medicamento, editar, eliminar, refrescar, buscar.
- **Datos**: ventana *Agregar nombre medicamento*: Nombre medicamento, Es principioActivo {SI, NO}, Código DCI, Clave, Activo {SI, NO}.
- **Listados**: Nombre | Principio Activo.
- **Flujos y reglas**: "Es principioActivo" permite que un registro sea a la vez nombre y principio activo (inferido). Guardar vs "Aceptar y guardar" (inferido: guardar y continuar).

## Compras > Planes de compra (/SUROSAlmacen/Vistas/Privado/CompraPlan/CompraPlan.aspx)
- **Propósito**: planificar compras de insumos/medicamentos y derivar cotizaciones y órdenes.
- **Funcionalidades**: El usuario puede crear un plan; agregar detalles; generar solicitud de cotización a proveedores; generar orden con seleccionados/todos; "Aprobar y Ordenar"; ver las órdenes generadas; eliminar el plan y sus detalles; imprimir; crear presentaciones nuevas desde el detalle.
- **Datos**:
  - Cabecera (*Plan de Compra*): No. plan, Fecha Planeación, Fecha Posible Compra, Encargado de Compra, serial, Aprobado, Órdenes generadas.
  - *Detalle del pedido*: Tipo de Suministro {Insumos, Medicamentos}, Suministro, Concentración, Forma farmacéutica, Presentación, Cantidad, Costo Unitario, Observación.
  - *Presentaciones*: Nombre, Cant. U., Tipo, Ancho, Alto, Espesor, Peso, U.M., Descripción.
  - *Generación de Cotizaciones*: Asunto, Proveedores (selección múltiple, ventana *Proveedores*: Nombre | Contacto).
  - *Ordenando Detalles*: Ordenar Detalle / Todo / Seleccionados.
- **Listados**: planes: No. Plan | Fecha Planeación | Planeó | Fecha Posible Compra | Encargado de Compra | Aprobado | Aprobó | Órdenes Generadas. Detalle: Tipo de Suministro | Suministros | Presentación | Cantidad | Costo Unitario | Costo Total | Aprobado | Orden | Estado.
- **Flujos y reglas (inferido)**: plan -> (opcional) cotización por correo a varios proveedores -> aprobación -> una o más órdenes de compra. Cada línea guarda su orden generada y estado. Costo total = cantidad x costo unitario.

## Compras > Órdenes de compra (/SUROSAlmacen/Vistas/Privado/CompraOrden/CompraOrden.aspx)
- **Propósito**: gestionar la orden de compra a proveedor y su recepción.
- **Funcionalidades**: El usuario puede crear/editar la orden; ordenar la compra; imprimir cotización y orden; adjuntar evidencia de pago y anexo de factura física; actualizar números de factura; "Recibir Compra" registrando novedades; eliminar.
- **Datos** (*Orden de Compra*): No. orden, Fecha Orden, Actividad, Impuesto, Fecha Vencimiento, Jefe de Compra, Almacén Compra, Estado {Planeado, Ordenado, Anulado, En Compra, Enviado, Recibido, Almacenado, Cotizado, Rechazado, Aplazado}, Aprobado, Aprobó, Observación, Proveedor, Método de pago {CONTADO, CREDITO}, Forma de pago {EFECTIVO, TARJETA DE CREDITO, TARJETA DÉBITO, CHEQUE}, Aplica Retención + Valor, Descuento, Dirección Despacho, Teléfono y correo de contacto (del proveedor), Dirección Entrega, Fecha Entrega, Persona que entregó, No. guía de embarque, Nota al proveedor. *Recibiendo Compra*: Observación de recibido, confirmación.
- **Listados**: No. | Fecha Orden | Proveedor | Método Pago | Estado | Encargado | Aprobado | Aprobó | Fecha Entrega. *Novedades en la Orden*: Tipo | Item | Presentación | Cant. Ordenada | Cant. Recibida | Cant. Faltante | Observación.
- **Flujos y reglas (inferido)**: estados lineales Planeado/Cotizado -> Ordenado -> En Compra -> Enviado -> Recibido -> Almacenado; Anulado/Rechazado/Aplazado son salidas. La recepción compara ordenado vs recibido y registra faltantes. Al "Almacenado" se espera carga a inventario (ver Carga de inventarios, tipo FACTURA COMPRA).

## Compras > Solicitudes (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/InventarioSolicitudPersonal.aspx)
- **Propósito**: solicitudes de suministros del funcionario a un área/almacén y control de lo recibido ("Mis solicitudes pendientes por recibir").
- **Funcionalidades**: El usuario puede crear solicitud, agregar detalles, cargar plantilla, guardar como plantilla, enviar, recibir seleccionados o todo, eliminar; filtrar por estado.
- **Datos** (*Solicitud de Suministros*): Fecha Solicitud, Solicitar al Área, Tipo, Suministro, Cantidad, Presentación; check "Es plantilla". Estados de solicitud {Solicitado, Pedido, Pendiente, Entregado, Entregado Parcialmente, Pendiente por Entregar, Anulado, Borrador, Consolidado, Rechazado, Entregado-Aprobado}. Estados de detalle {Solicitado, Pedido a almacen, No Disponible, Entregado, Rechazado, Recibido, Entrega Parcial}.
- **Listados**: Fecha Solicitud | Usuario Solicitó | Almacén Despacho | Usuario Despachó | Usuario Recibió | Estado; detalle: ID | Tipo | Suministro | Cant. Solicitada | Presentación | Cant. Entregada | Estado; paneles "Pendiente Por Pedir" y "Recibidos"; ventanas *Recibiendo*, *Aplicar Plantilla*, *Ayuda*.
- **Flujos y reglas (inferido)**: borrador -> Enviar -> despacho (otra pantalla) -> confirmación de recibido por el solicitante. Alerta visual "Nuevos suministros entregados!".

## Compras > Pedido interno (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/PedidoInterno.aspx)
- **Propósito**: pedido entre almacenes (p. ej. farmacia a bodega).
- **Funcionalidades**: El usuario puede crear pedido, agregar detalle, cargar plantilla/guardar plantilla, enviar pedido, guardar, eliminar, rechazar (pedido o detalle con nota), recibir seleccionados/todo; filtrar por fechas, almacenes y usuarios.
- **Datos** (*Pedido Interno*): Fecha, Usuario Solicitó, Almacén Solicita, Almacén Entrega, Estado, Tipo {INSUMO, MEDICAMENTO}, Suministro, Cantidad, Presentación, Observación, Es plantilla. *Rechazando Pedido*/*Rechazando Detalle*: nota de rechazo.
- **Listados**: Id | Id | Fecha Solicitud | Almacén Solicita | Usuario Solicitó | Almacén Despacha | Usuario Despachó | Usuario Recibió | Estado; detalle: ID | Tipo | Suministro | Presentación | Cant. Solicitada | Entregado | Estado; panel "Pendiente Para Entrega".
- **Flujos y reglas (inferido)**: mismo catálogo de estados que Solicitudes; el almacén destino despacha en "Despacho pedidos".

## Compras > Despacho pedidos (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/PedidoInternoDespacho.aspx)
- **Propósito**: bodega/almacén despacha los pedidos internos contra existencias por lote.
- **Funcionalidades**: El usuario puede ver pedidos pendientes e historial; abrir uno; "Cargar Inventario" (asignar lotes); despachar seleccionado o todo; agregar detalle; guardar/terminar; rechazar pedido o detalle; ver entregas; generar ACTA DE ENTREGA; exportar; cancelar entrega; "RECIBIR Y FIRMAR"; gestionar devoluciones al inventario de farmacia; imprimir devoluciones.
- **Datos**: *Despacho Pedido Interno*: No, Fecha, Usuario Solicitó, Almacén Solicita, Bodega Despacha, Estado, Solicitante, Despacha, Fecha Solicitud. *Despachando Detalles*: Usuario, Contraseña (validación de recibido), check "Dejar en espera de recibido". *Ingresar credenciales*: nombre de usuario, contraseña. *Detalle de Solicitud*: Tipo, Item, Presentación, Cantidad Solicitada. *Rechazando*: nota.
- **Listados**: pedidos: No. Pedido | Fecha Solicitud | Almacén despacha | Usuario Solicitó | Almacén solicita | Usuario Despachó | Usuario Recibió | Estado (pendientes e histórico con filtros de fecha). Detalle: ID | Tipo | Suministro | Presentación | Cant. Solicitada | Cant. Entregada | Cant. a Despachar | Existencias | Estado. Selección de lote: Cant. Entrega | Item | Presentación | Lote | Fecha Venc. | Cant. Actual | Cant. Descargada | Cant. Almacenada. Devoluciones: Cantidad | Item | Paciente | Inventario | Fecha Entrega | Observación | TotalEntregado | TotalGastado.
- **Flujos y reglas (inferido)**: el despachador elige lotes (probablemente FEFO por vencimiento); descarga de bodega y carga a almacén destino; firma electrónica de entrega/recibo con usuario y contraseña; existe devolución desde farmacia a inventario con vínculo a paciente.

## Inventarios > Activación de cargas (/SUROSAlmacen/Vistas/Privado/InventarioBodega/ListarOrdenesInventario.aspx)
- **Propósito**: lista de órdenes de inventario (cargas) pendientes de aprobación/resolución entre origen y destino.
- **Funcionalidades**: El usuario puede solicitar productos a bodega, editar una orden si no está aprobada, resolver la orden, ver los suministros.
- **Datos**: ventana *Suministros* (solo lectura).
- **Listados**: ORDEN | FECHA | OBSERVACION | ESTADO | ORIGEN | DESTINO | REGISTRA | MODIFICA | FECHA CAMBIO; detalle: # | Suministro | Tipo | Cantidad | Precio de compra.
- **Flujos y reglas (inferido)**: una orden nace como solicitud y se "resuelve" para activar la carga en destino.

## Inventarios > Ajuste (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioAjuste.aspx)
- **Propósito**: ajustes de inventario (conteos, daños, vencimientos, préstamos).
- **Funcionalidades**: El usuario puede buscar ajustes por fechas; crear ajuste; agregar ítems con cantidad nueva; definir datos de medicamento o insumo si no existe; guardar e imprimir.
- **Datos**: *Datos básicos del ajuste*: Fecha, Sede, Almacén, Categoría {AJUSTE PERIODICO, AJUSTE INPREVISTO, AJUSTE INCIAL INVENTARIO, AJUSTE POR OTROS MOTIVOS}, Observación general. *Ítem*: Item, Existente, Cantidad actual, Tipo de ajuste {DAÑOS, APROVECHAMIENTO, DESCUADRE, PRESTAMOS, VENCIMIENTO}, Observación, Und medida, Precio compra und, Cod barra, Fecha vencimiento, Centro de costo, Código referencia, Lote. *Datos específicos medicamentos*: Registro sanitario INVIMA, Estado {Vigente, Vencido, En trámite, No Aplica}, CUM, Expediente INVIMA, IUM, Cod ATC, Laboratorio, Marca, Controlado, Esencial, Institucional. *Insumo*: Marca, Cod referencia, Fecha vencimiento, Centro costo; grilla de características dinámicas (Nombre | Valor | Visible? | Búsqueda?) con subir/bajar fila y "Aplica para los siguientes vehículos" (resto de plantilla genérica).
- **Listados**: ID | NUMERO | FECHA | FECHA REGISTRO | Almacén | Tipo Item | Realizó; detalle: # | ITEM | NUEVA CANTIDAD | CATEGORIA | OBSERVACION; coincidencias: NOMBRE | TIPO | INPR_ID | REGISTRO | LOTE | PRECIO | COMPRADA | CANTIDAD.
- **Flujos y reglas (inferido)**: el ajuste fija "nueva cantidad" por lote y deja trazabilidad por motivo.

## Inventarios > Carga de inventarios (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioBodega.aspx)
- **Propósito**: ingresar existencias a bodega (o directo a almacén) por factura, donación, traslado, etc. Texto de ayuda: los inventarios se ingresan a la bodega y luego se hacen pedidos entre almacenes hacia la bodega.
- **Funcionalidades**: El usuario puede crear carga de insumos o medicamentos; importar por XLS; agregar ítems manualmente; editar el detalle de una carga con motivo de modificación; aprobar carga o "Aprobar y Enviar a Almacén"; guardar en bodega/almacén; crear proveedor, registro sanitario o laboratorio al vuelo; adjuntar archivos/imágenes de factura; registrar préstamos de suministros a entidades y devoluciones; exportar XLS (general por ítem, por almacén, reportes).
- **Datos**:
  - Cabecera: Fecha carga, Tipo cargue {FACTURA COMPRA, APROVECHAMIENTO, DONACIONES, TRASLADO, CARGUE INICIAL}, Tipo {MEDICAMENTO / INSUMO}, Sede, Bodega, Almacén, Fecha factura, No. factura, Proveedor, Observación.
  - Ítem: Item (búsqueda), Cant. und, Precio compra und, Und medida, Cod barra, Lote, Código referencia, Fecha vencimiento, Centro de costo, paneles Precio Venta e Impuesto. Datos específicos de medicamentos (registro INVIMA, estado, CUM, expediente, IUM, ATC, laboratorio, marca, controlado/esencial/institucional) e insumos (marca, fabricante).
  - Préstamo: check Prestamo, quién solicitó, No. documento. Detalle: Serial, Presentación, Costo unitario, Proveedor, Id factura, Ubicación, Cantidad.
  - Ventanas auxiliares: *Crear Proveedor* (prioridad, tipo persona/documento, razón social, nombre comercial, email, dirección, teléfonos, responsabilidades fiscales, municipio), *Nuevo Registro Sanitario* (registro, activo), *Datos del Laboratorio*, *Presentaciones*, *Municipio*, *Archivos*, *Edición de Carga* (motivo de modificación), *Actualizar cantidades en almacén*, *Ingresar credenciales*.
- **Listados**: ID | TIPO CARGUE | NUMERO FACTURA | FECHA FACTURA | FECHA CARGA | Fecha Inventario | Almacén | Tipo Item | Realizó | OBSERVACION | Aprobado en bodega. Detalle: ID | Item | Presentación | Lote | Fecha Venc. | Cant. | Costo Unit. | No. Factura | Ubicación | Total | Proveedor. Edición: ID | Item | Reg. Sanitario | Est. Reg. Sanitario | Centro Cost. | Marca | Laboratorio | Und. Medida | Cod. Barra | Cod. Ref | CUM | Lote | Fecha Venc. | Cant. | Costo Unit. | Total.
- **Flujos y reglas (inferido)**: carga queda sin aprobar hasta "Aprobar Carga" (entra a existencias de bodega); "Aprobar y Enviar a Almacén" hace envío directo a farmacia. Cada línea es un lote con vencimiento y ubicación; la modificación posterior exige motivo y credenciales. Medicamentos exigen registro sanitario INVIMA/CUM.

## Inventarios > Informes gastos almacén (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioStock.aspx)
- **Propósito**: informe de consumo/stock por rango de fechas y horas.
- **Funcionalidades**: El usuario puede buscar entregas, visualizar y exportar el informe, guardarlo firmado con credenciales (validar responsable).
- **Datos**: Fecha inicial/final, Hora inicial/final, Tipo suministro {TODO, INSUMO, MEDICAMENTO}, Almacén, check Consumidos, validar responsable (usuario, contraseña).
- **Listados**: *Listado de entregas*: Código | RECIBE | ENTREGA | fecha registro. *Detalle de la entrega*: No | TIPOSUMINISTRO | SUMINISTRO | CANTIDAD INICIAL DEL RANGO | TRASLADO AL STOCK DURANTE EL RANGO | CANTIDADES CONSUMIDAS | VENDIDOS | CANTIDAD DISPONIBLE EN STOCK.
- **Flujos y reglas (inferido)**: informe de cuadre de stock (inicial + traslados - consumo - ventas = disponible), firmado por el responsable.

## Inventarios > Existencias en bodega > Insumos en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaInsumos.aspx)
- **Propósito**: consultar existencias de insumos por lote en bodega.
- **Funcionalidades**: El usuario puede filtrar (ítem, serial, lote, vencimiento, presentación, ubicación, proveedor, fabricante), ver solo con existencias, ver historial, exportar XLS detallado/por ítems, ver movimientos del lote (cargas y descargas) y dar de baja inventario.
- **Datos** (*Dar de baja*): Cantidad a descargar, Fecha descarga, Observación.
- **Listados**: Item | Serial | Lote | Fecha Vencimiento | Cant. Almacenada | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor | Fabricante. Paneles *Cargas al Lote* / *Descargas del Lote*.
- **Flujos y reglas**: Cant. Actual = almacenada - descargada (inferido).

## Inventarios > Existencias en bodega > Medicamentos en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaMedicamentos.aspx)
- **Propósito**: igual que insumos, para medicamentos (con registro INVIMA y laboratorio).
- **Funcionalidades**: filtros, historial, XLS, movimientos del lote, dar de baja, y "Actualizar valores del inventario" (corrige un valor).
- **Datos**: ventana *Actualizando valores* (Valor a actualizar); *Dar de baja* (cantidad, fecha, observación); filtros incluyen Registro sanitario INVIMA, Laboratorio, Almacén, centro de costo.
- **Listados**: Item | Serial | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor | Laboratorio.

## Inventarios > Existencias en bodega > Suministros oficina en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaEquiposOficina.aspx)
- **Propósito**: existencias de suministros de oficina en bodega.
- **Funcionalidades**: igual que insumos en bodega (filtros, historial, XLS, movimientos, dar de baja).
- **Listados**: Suministro | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor.

## Inventarios > Existencias en almacén > Insumos en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioInsumos.aspx)
- **Propósito**: existencias de insumos en un almacén (bodega/farmacia) con semaforización de vencimientos y descarga de consumo.
- **Funcionalidades**: El usuario puede filtrar por almacén y fechas (mes o rango); ver semáforo ROJO/AMARILLO/VERDE/VENCIDOS/TODOS; descargar, actualizar o cargar cantidades de un lote; entregar stock (recepción y entrega de almacén de stock); ver inventario actual, historial, reportes; generar códigos de barras unidosis.
- **Datos**: *Descargando del inventario*: Id detalle, Lote, Valor a descargar, Centro de costo, Funcionario que realiza descarga, Nota. *Actualizando valores*: valor a actualizar. *Cargando*: valor a cargar. *Creando código de barras Unidosis*: Código original, Cant. a generar, Valor inicial/final, Químico farmacéutico, Generar tarjeta / PDF / PDF rango.
- **Listados**: ID INSUMO | ID INVENTARIO PRODUCTO | Item | Cant. Almacenada | Cant. Desc. | Cant. Actual; *Códigos de barras*: Id | Código Original | Valor Inicial | Valor Final | Cant. Generada | Químico Farmacéutico | Generada | Aplicada.
- **Flujos y reglas (inferido)**: semáforo por proximidad de vencimiento (umbrales sin evidenciar); unidosis = reempaque con código de barras propio, firmado por el químico farmacéutico.

## Inventarios > Existencias en almacén > Medicamentos en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioMedicamentos.aspx)
- **Propósito**: existencias de medicamentos en almacén/farmacia, con precios y registro sanitario.
- **Funcionalidades**: las de insumos en almacén más precios, "Actualizar el serial del producto" y filtro por centro de costo.
- **Listados**: ID MEDICAMENTO | ID INVENTARIO PRODUCTO | NOMBRE | Código de Barras | LOTE | Fecha Venc. | Cant. Alm. | Precio Compra | Precio Venta | Reg.Inv. | Presentación | Cant. desc | Cant. Actual | Fecha Inventario | Proveedor | Laboratorio | Centro Costo.
- **Datos**: igual que insumos (descarga, actualizar, cargar, unidosis; muestra nombre, forma, concentración y presentación).

## Inventarios > Existencias en almacén > Suministros oficina en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioEquiposOficina.aspx)
- **Propósito**: existencias de suministros de oficina en almacén.
- **Funcionalidades**: filtros por fecha, descarga a centro de costo, actualizar/cargar, historial, XLS.
- **Listados**: Id | Item | Serial | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor.

## Terceros > Fabricantes (/SUROSAlmacen/Vistas/Privado/InventarioItemFabricante/InventarioItemFabricante.aspx)
- **Propósito**: maestro de fabricantes de productos.
- **Funcionalidades**: El usuario puede crear, editar, eliminar, filtrar.
- **Datos**: Fabricante, NIT, Teléfono contacto, Correo contacto, Observación.
- **Listados**: Fabricante | Nit | Teléfono Contacto | Correo Contacto | Observación.

## Terceros > Laboratorios (/SUROSAlmacen/Vistas/Privado/InventarioItemLaboratorio/InventarioItemLaboratorio.aspx)
- **Propósito**: maestro de laboratorios (instituciones que diseñan y elaboran medicamentos e insumos).
- **Funcionalidades**: crear, editar, eliminar, filtrar.
- **Datos**: Nombre, NIT, Teléfono, Correo, Observación, Dirección.
- **Listados**: Nombre | Nit | Correo Contacto | Teléfono | Observación | Dirección.

## Terceros > Proveedores (/SUROSAlmacen/Vistas/Privado/InventarioItemProveedor/InventarioItemProveedor.aspx)
- **Propósito**: maestro de proveedores con datos fiscales, de contacto y bancarios.
- **Funcionalidades**: El usuario puede crear/editar/eliminar proveedor; asociar tipos de inventario que suministra; buscar municipio; adjuntar cuentas bancarias; marcar "Enviar Precios".
- **Datos**: Tipo de documento (13 tipos: cédula, NIT, pasaporte, registro civil, TI, extranjería, PEP, PPT, etc.), Documento, Representante, Empresa, Contribuyente {Persona Natural, Persona Jurídica}, Régimen (lista de ~18 valores: común, simplificado, especial, contributivo, subsidiado, vinculado, particular, etc.), Sitio web, Tipos de inventario; *Empresarial*: teléfono, correo, fax, municipio, dirección; Enviar precios; *Bancaria*: cuentas (número, titular, tipo {Corrientes, Remunerada o Ahorros, Nómina, Vivienda}, banco); Observación.
- **Listados**: Representante | NIT | Teléfono | Correo | Empresa | Tipo Contribuyente | Régimen | Dirección | Enviar Precios; cuentas: Cuenta | Titular | Tipo de Cuenta | Banco.
- **Flujos y reglas (inferido)**: "Enviar Precios" probablemente incluye al proveedor en las solicitudes de cotización.

## Farmacia (/SUROSAlmacen/Vistas/Privado/SolicitudMedicamentosEInsumos/Farmacia.aspx)
- **Propósito**: panel del regente de farmacia: recibe solicitudes de medicamentos e insumos por paciente, dispensa con acta de entrega, controla aplicación y devoluciones.
- **Funcionalidades**: El usuario puede buscar paciente (por tipo y dato de documento, búsqueda general); crear solicitud (medicamentos + insumos, estancia, profesional que solicita, observación) y "Guardar y Enviar"; ver historial del paciente; abrir panel de solicitudes y filtrar por fecha; generar ACTA DE ENTREGA (No. entrega, ciudad, fecha); ENTREGAR Y FIRMAR / CANCELAR ENTREGA; ENTREGAR TODO; ver tratamientos (último o todos) con posología, suministrado, aplicado y última aplicación; ver insumos usados; registrar aplicación de medicamentos; cargar inventario; descarga masiva; cargar y consultar devoluciones (incluir aceptadas) e historial; nueva entrega anticipada; reportes (aplicación de medicamentos, controlados, entrega de controlados) por mes o rango; accesos por área (OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA); botón App. HD.
- **Datos**: Solicitud: Estancia, Profesional solicita, Observación. Paciente: nombre, documento, EPS de afiliación/ingreso (solo lectura). Acta de entrega: tipo, No. de entrega, ciudad (municipio), fecha. Estados de solicitud {Formulada, Recibida, Entrega Parcial, Entrega Total, Cancelada}. Tipo de documento abreviado {AS, CC, CE, MS, NT, PA, RC, TI, TE, NV, PEP, PPT, PT}. Almacén {BODEGA, FARMACIA}.
- **Listados**: *SOLICITUDES A LA FARMACIA*: Fecha Solicitud | T.D. | Documento | Paciente | Regente | Médico | Estancia | Estado | T. Insumos | T. Medicamentos. *MEDICAMENTOS* de solicitud: ID | Descripción | Forma | Concentración | Presentación | Cantidad | Und/Med | Observaciones. *INSUMOS*: Insumo | Presentación | Cantidad Solicitada | Observación. Acta: # | Registro INVIMA | CUM | Lote | F. Vencimiento | Medicamento | Forma | Concentración | C/Formulada | C/Entregada. Tratamientos: Posología | Total Suministrado | Aplicados | Total a aplicar | Última aplicación. *HISTORIAL DE DEVOLUCIONES* (mismas columnas que solicitudes). Coincidencias de medicamentos/insumos con existencias.
- **Flujos y reglas (inferido)**: Formulada (por médico en HC) -> Recibida -> Entrega Parcial/Total; el acta registra registro INVIMA, CUM y lote entregado (trazabilidad); control especial de medicamentos controlados; descarga de existencias por lote al entregar; las devoluciones regresan al inventario de farmacia; "entrega anticipada" permite dispensar sin fórmula previa (inferido).

## Enfermería (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/InventarioSolicitudInsumos.aspx)
- **Propósito**: enfermería solicita insumos a un almacén, normalmente asociados a un paciente.
- **Funcionalidades**: El usuario puede crear pedido, usar "Mis Plantillas", cargar plantilla, buscar insumos (coincidencias con existencias), enviar/guardar/eliminar pedido, recibir seleccionados/todo, ver todos los pedidos, ver videotutorial.
- **Datos**: Solicitar a almacén, check Es plantilla; filtros por paciente, fecha, usuario, almacén, estado (mismos catálogos de estados).
- **Listados**: pedido: Código | Insumo | Presentación | Solicitada | Entregada | Estado | Observación; pedidos: ID | Paciente | Fecha Solicitud | Usuario Solicitó | Farmacia Despachó | Regente Despachó | Enfermero | Estado; coincidencias: ID | Código | Nombre | Presentación | Existencias.

## Tienda en línea (/SUROSAlmacen/Vistas/Privado/Inventario/TiendaEnLinea.aspx)
- **Propósito**: no determinado; presumiblemente venta en línea de productos del inventario (inferido por el nombre y la columna "VENDIDOS" del informe de gastos).
- **Funcionalidades**: no extraíble: la página devolvió error de servidor ("Index was outside the bounds of the array") al extraer. Defecto de la instalación original, no una funcionalidad.

## Configuración > Categorías (/SUROSAlmacen/Vistas/Privado/InventarioItemCategoria/InventarioItemCategoria.aspx)
- **Propósito**: categorías de ítems de inventario.
- **Funcionalidades**: crear, editar, eliminar, filtrar.
- **Datos**: Categoría, Descripción, Tipo (de inventario), Requiere mantenimiento.
- **Listados**: Categoría | Descripción | Tipo | Req. Manten.

## Configuración > Centros de costo (/SUROSAlmacen/Vistas/Privado/ContabilidadCentroCosto/ContabilidadCentroCosto.aspx)
- **Propósito**: centros de costo contables a los que se imputan cargas y descargas.
- **Datos**: Centro costo, Descripción. **Listados**: Id | Centro Costo | Descripción.
- **Funcionalidades**: crear, guardar, eliminar, filtrar.

## Configuración > Estados de pedido (/SUROSAlmacen/Vistas/Privado/InventarioSolicitudEstado/InventarioSolicitudEstado.aspx)
- **Propósito**: catálogo de estados de solicitud/pedido con color para la UI.
- **Datos**: Estado, Descripción, Color. **Listados**: Id | Estado | Descripción | Color.
- **Funcionalidades**: editar, guardar, eliminar, aprobar (botón presente en ventana).

## Configuración > Parámetros de configuración (/SUROSAlmacen/Vistas/Privado/ParametroConfiguracion/ParametroConfiguracion.aspx)
- **Propósito**: parámetros clave-valor del módulo, restringidos por rol.
- **Datos** (*Detalle del parámetro*): Configuración, Valor, Tipo de dato, Descripción, Roles, Activo.
- **Listados**: ID | Configuración | Valor | Tipo Dato | Roles | Registrado Por | Fecha Creación.
- **Funcionalidades**: nuevo, guardar, cancelar, eliminar, imprimir, aprobar.

## Configuración > Presentaciones (/SUROSAlmacen/Vistas/Privado/InventarioItemPresentacion/InventarioItemPresentacion.aspx)
- **Propósito**: presentaciones/empaques de los ítems (caja, frasco, etc.) con dimensiones.
- **Datos**: Tipo de empaque, Unidades, Ancho/Alto/Espesor (cm), Volumen|Peso (ML, CC, GR), Unidad de medida, Activo, Descripción, Tipos de inventario a los que aplica, foto (ventana *Actualizando Foto*).
- **Listados**: ID | Imagen | Nombre | Dimensiones | Tipo | Cant. de Unidades | Alto | Ancho | Espesor | Volumen/Peso | Aplica a Tipos | Activo.
- **Funcionalidades**: crear, editar, activar/desactivar, eliminar.

## Configuración > Empresa (/SUROSAlmacen/Vistas/Privado/Empresa/PanelEmpresas.aspx)
- **Propósito**: panel de empresas; solo se observan accesos de alta.
- **Funcionalidades**: El usuario puede crear "Nueva Empresa Proveedora" y "Nueva EPS" y refrescar la lista. Sin campos extraídos (inferido: formularios en otra página/ventana no cargada).

## Configuración > Almacenes (/SUROSAlmacen/Vistas/Privado/Almacen/Almacen.aspx)
- **Propósito**: maestro de almacenes/bodegas/farmacias por sede.
- **Datos** (*Detalle del Almacén*): Imagen, Área (m), Nombre, Descripción, Sede, Observaciones, Encargado, Tipo {Bodega, Almacén, Almacén Virtual, Farmacia}, Teléfono, Correo contacto, Estado {Activo, En Mantenimiento, Inactivo, Clausurado}, Último inventario, Fecha último mantenimiento.
- **Listados**: Nombre | Sede | Observaciones | Tel. | Estado | Tipo.
- **Funcionalidades**: nuevo, guardar, eliminar, filtrar.

## Configuración > Canastas de cirugía (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/CanastasCirugias.aspx)
- **Propósito**: plantillas de suministros por procedimiento quirúrgico y médico.
- **Funcionalidades**: El usuario puede crear una canasta, elegir el procedimiento (ventana de selección), farmacia y médico, agregar detalle (tipo, suministro, cantidad, presentación), guardar, eliminar.
- **Listados**: Procedimiento Quirúrgico | Médico | Fecha Creación | Usuario Diseño; detalle: Tipo de suministro | Suministro | Presentación | Cant. Solicitada; procedimientos: Código | Descripción.
- **Flujos y reglas (inferido)**: la canasta se usa para solicitar/dispensar de una vez los insumos de una cirugía.

---

## Ciclo de abastecimiento (inferido)

1. **Plan de compra**: se define qué comprar (insumos/medicamentos, cantidad, costo), encargado y fecha. Se aprueba.
2. **Solicitud de cotización** (opcional): correo a proveedores seleccionados desde el plan.
3. **Orden de compra**: generada desde el plan (seleccionados/todo); estados Planeado -> Ordenado -> En Compra -> Enviado -> Recibido -> Almacenado (Anulado/Rechazado/Aplazado como salidas). Se adjuntan evidencia de pago y factura; la recepción registra novedades (ordenado vs recibido vs faltante).
4. **Carga/entrada**: "Carga de inventarios" (FACTURA COMPRA, APROVECHAMIENTO, DONACIONES, TRASLADO, CARGUE INICIAL); cada línea es un lote con vencimiento, registro INVIMA/CUM, costo y ubicación. "Aprobar carga" lo hace visible en bodega; "Aprobar y enviar a almacén" lo envía directo a farmacia. "Activación de cargas" resuelve órdenes de inventario pendientes.
5. **Bodega -> almacén**: cada almacén (farmacia, etc.) crea un **pedido interno** (o solicitud/plantilla); la bodega lo **despacha** eligiendo lotes, con firma de entrega/recibo y rechazo parcial. Descarga de bodega, carga en almacén.
6. **Dispensación**: **Farmacia** atiende solicitudes por paciente con acta de entrega (lote, INVIMA, CUM), controla aplicaciones y devoluciones; **Enfermería** solicita insumos (por paciente) a farmacia/almacén; canastas de cirugía agilizan pedidos quirúrgicos. Descargas manuales asignan centro de costo y funcionario.
7. **Ajustes**: por conteo periódico, daño, vencimiento, préstamo, aprovechamiento o descuadre; actualización de valores y "dar de baja" por lote.
8. **Lotes y vencimientos**: toda existencia es por lote (lote, fecha vencimiento, cantidad almacenada, descargada, actual); semáforo ROJO/AMARILLO/VERDE/VENCIDOS en almacén; movimientos del lote (cargas y descargas) consultables; máximos y mínimos por ítem en catálogo; informe de gastos concilia stock.

## Entidades y estados

Entidades (inferidas de campos y IDs): Plan de compra (+ detalle), Orden de compra (+ novedades), Solicitud/Pedido interno (+ detalle, plantilla), Orden de inventario/Carga (+ detalle por lote, archivos adjuntos), Ajuste (+ detalle), Inventario detalle (lote por ubicación), Ítem de inventario (insumo, medicamento, suministro de oficina), Medicamento catálogo (forma, concentración, presentación, volumen, principio activo, homologación), Categoría, Presentación, Tipo de inventario, Registro sanitario INVIMA, Fabricante, Laboratorio, Proveedor (+ cuentas bancarias), Empresa (proveedora/EPS), Almacén, Sede, Centro de costo, Código de barras unidosis, Solicitud de farmacia (+ acta de entrega, devolución), Canasta de cirugía, Parámetro de configuración.

Estados:
- Orden de compra: Planeado, Ordenado, Anulado, En Compra, Enviado, Recibido, Almacenado, Cotizado, Rechazado, Aplazado.
- Solicitud/pedido: Solicitado, Pedido, Pendiente, Entregado, Entregado Parcialmente, Pendiente por Entregar, Anulado, Borrador, Consolidado, Rechazado, Entregado-Aprobado.
- Detalle de solicitud: Solicitado, Pedido a almacén, No Disponible, Entregado, Rechazado, Recibido, Entrega Parcial.
- Solicitud de farmacia: Formulada, Recibida, Entrega Parcial, Entrega Total, Cancelada.
- Registro sanitario: Vigente, Vencido, En trámite, No Aplica.
- Almacén: Activo, En Mantenimiento, Inactivo, Clausurado; tipos Bodega, Almacén, Almacén Virtual, Farmacia.
- Carga: aprobada / no aprobada en bodega. Presentación: activa/inactiva.
- Tipos de cargue: FACTURA COMPRA, APROVECHAMIENTO, DONACIONES, TRASLADO, CARGUE INICIAL. Tipos de ajuste: DAÑOS, APROVECHAMIENTO, DESCUADRE, PRESTAMOS, VENCIMIENTO. Categorías de ajuste: PERIODICO, IMPREVISTO, INICIAL, OTROS MOTIVOS.
- Pago: CONTADO/CREDITO; forma EFECTIVO, TARJETA DE CREDITO, TARJETA DEBITO, CHEQUE.

## Página web (CMS)

Sub-app `/SUROSPaginaWeb` (entrada `/SUROSPaginaWeb/Vistas/InicioPaginaWeb.aspx`). El árbol de menú no mostró hojas y las pantallas no fueron extraídas. Se sabe solo que existe la entrada de inicio de un CMS del sitio web de la institución (inferido por el nombre). No hay funcionalidades confirmadas.

## Preguntas abiertas

1. **Pantalla Tienda en línea**: falla en origen; ¿qué vende, con qué precios, impuestos y pasarela, y cómo se relaciona con la columna "VENDIDOS" y el "Precio Venta"?
2. **Reglas de descarga de lotes**: ¿FEFO/FIFO automático o manual? ¿Umbrales del semáforo ROJO/AMARILLO/VERDE y comportamiento al vencer?
3. **Transiciones de estado**: ¿qué acción dispara cada estado de orden de compra, solicitud y detalle (p. ej. Consolidado, Entregado-Aprobado), y qué roles pueden aprobar?
4. **Integración con Historia Clínica y Facturación**: ¿cómo se crea la solicitud "Formulada" de farmacia desde la HC, cómo se factura lo dispensado y cómo se vincula Medicamentos (Facturación) con el catálogo nuevo?
5. **Medicamentos controlados y trazabilidad regulatoria**: ¿qué reportes y validaciones exige el sistema (libro de controlados, INVIMA/CUM, unidosis) y cómo funcionan "Activación de cargas", préstamos entre entidades y la carpeta OLD?
