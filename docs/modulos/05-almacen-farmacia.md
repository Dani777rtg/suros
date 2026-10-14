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

## Inicio de almacén (/SUROSAlmacen/Vistas/InicioAlmacen.aspx)
- **Propósito**: página contenedora (menú lateral + pestañas) y tablero de alertas de inventario de medicamentos e insumos.
- **Hallazgos del código**:
  - `CelClic`/`CargaTab` abren cada hoja del menú como pestaña del panel central; al abrir `Farmacia.aspx`, `InventarioItemMedicamento.aspx`, `InventarioItemInsumo.aspx` o `TiendaEnLinea.aspx` se colapsa el menú lateral. `InventarioItemMedicamento.aspx` e `InventarioItemInsumo.aspx` se nombran en el código pero no figuran en el árbol de menú extraído.
  - `recargarPaneles` refresca la pestaña activa (p. ej. FARMACIA) llamando `RefrescarLayout` en su iframe.
  - Tablero: consultas por mes/año o por rango de fechas (`SRV.GCM` medicamentos, `SRV.GCI` insumos); las filas con cantidad actual 0 se pintan en ámbar (`getRowClassDSIM`, `getRowClassDSII`); las listas de productos por vencer usan `getRowClassMPV`/`getRowClassIPV`.
  - `CrearPedidoAutomatico(data)` abre PEDIDO INTERNO con datos precargados (existe un flujo de pedido automático de reposición).
  - Cambio de contraseña (`CP`): 'Ingrese usuario.', 'Ingrese contraseña.', 'La contraseña no coincide.', 'La contraseña debe tener minimo 6 caracteres.'; salir: "Esta seguro de salir de la Sesión?" (`cierraNavegador`).

## Catálogos > Catálogo insumos nuevo (/SUROSAlmacen/Vistas/Privado/CatalogoBasico/ListarCatalogo.aspx)
- **Propósito**: listar el catálogo base de insumos y definir sus mínimos/máximos de stock.
- **Funcionalidades**: El usuario puede filtrar por palabra y por columna; agregar un producto ("Agregar un producto"); abrir "Maximos y minimos" de un producto; editar; recargar.
- **Datos**: ventana *Maximos y minimos*: Minimo, Maximo (numéricos). Alta de producto: campos de texto sin etiqueta en la extracción (no identificables).
- **Listados**: *Listado de productos*: # | CPFR_ID | CODIGO | CATEGORIA | NOMBRE BASE | DATOS ADICIONALES | APLICA PARA | FECHA CREACION | PERSONA (registra) | Valor Minimo | Cantidad Actual | Cantidad Maxima | Opciones. Paginación 1/2/10/20.
- **Flujos y reglas**: mínimo/máximo por producto, comparado con Cantidad Actual (inferido: alertas de reposición). "APLICA PARA" indica a qué tipo de inventario aplica (inferido).
- **Hallazgos del código**:
  - Eliminar: confirmación Sí/No "¿Esta seguro de eliminar el catalogo?" -> `SRV.EliminarCatalogo`. "VerPdf" -> `SRV.AgregarCargaProducto({option:1})`.
  - Máximos y mínimos se guardan con `SRV.GuardarMinimosMaximos({MINIMO, MAXIMO, CATA, TIPO:'2'})` (TIPO '2' = insumos; el catálogo de medicamentos usa TIPO '1'). El cliente no valida mínimo <= máximo ni compara con la cantidad actual.
  - Filtro de texto único sobre el campo `GRUPOBUSQUEDA` (coincidencia parcial, sin distinguir mayúsculas).

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
- **Hallazgos del código**:
  - Alta/edición (`guardarnuevocatalogomedicamento`): si el id oculto está vacío llama `SRV.GCMN` (CATA_ID '-1'), si no `SRV.ECMN`. Envía además dos casillas no documentadas arriba: Activo (CATA_ESTADO 1/0) y Controlado (CATA_CONTROLADO 1/0), y un UUID (código único, `generateUUID`, generado en el navegador) que se muestra como Código único.
  - Principios activos se envían como JSON (MEDA_ID, UNME_ID, CANTIDAD); sin selección se envía '-1'. Con más de 5 principios el resumen se trunca a 30 caracteres + '...'.
  - Editar -> `SRV.PEDCMN`; Eliminar -> `SRV.ELCMN` tras "Esta seguro de eliminar este registro?".
  - Homologación: `SRV.CargarDatosHomologacion`; eliminar un homologado ya guardado pide "¿Está seguro de eliminar este registro homologado?" y responde 'Registro eliminado correctamente.' o 'No se pudo eliminar el registro.' (también `CatalogoMedicamento.aspx/EliminarHomologacion`); si aún no se guardó solo se quita de la grilla. El botón de homologación solo se muestra si HOMOLOGADO > 0 (`preparaBarraPR`) y esas filas llevan clase `homolog-row`.
  - Filas con ESTADO = INACTIVO usan la clase `fact-row` (`getRowClass`). El buscador general filtra por nombre, forma, concentración, presentación, volumen, estado, controlado, categoría, principio activo, código único y clasificación de riesgo (`FiltrarResultados`).
  - Concentración: valor A + unidad A, operador y valor B + unidad B (`GuardarConcentracion`); unidades vacías se envían como -1. Volumen: `SRV.GuardarVolumen`; presentación: `SRV.GuardarPresentacion`; forma: `SRV.GuardarFormaFarmaceutica`.
  - Máximos y mínimos: `SRV.GuardarMinimosMaximos` con TIPO '1'; la columna muestra Mínimos, Máximo y Cantidad actual (CANTIDADEXISTENCIA).

## Catálogos > Medicamentos (/SUROSFacturacion/Vistas/Privado/Medicamentos/Medamento.aspx)
- **Propósito**: lista simple de nombres de medicamento y su principio activo (catálogo de Facturación).
- **Funcionalidades**: El usuario puede agregar medicamento, editar, eliminar, refrescar, buscar.
- **Datos**: ventana *Agregar nombre medicamento*: Nombre medicamento, Es principioActivo {SI, NO}, Código DCI, Clave, Activo {SI, NO}.
- **Listados**: Nombre | Principio Activo.
- **Flujos y reglas**: "Es principioActivo" permite que un registro sea a la vez nombre y principio activo (inferido). Guardar vs "Aceptar y guardar" (inferido: guardar y continuar).
- **Hallazgos del código**:
  - `guardarHomologacion` (nombre de función heredado de otra pantalla): si el formulario no es válido muestra 'Por favor complete todos los campos'; si lo es, `SRV.Guardar` con CODIGO, PRINCIPIOACTIVO, DCI, CODUGOUNICO (UUID generado en el navegador), ESTADO y NOMBRE en mayúsculas y sin espacios sobrantes.
  - Al cerrar la ventana (`eventoCerrarWinCatalogo`) se reinicia el formulario.

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
- **Flujos y reglas**: plan -> aprobación -> una o más órdenes de compra (confirmado en código: `ejecutarAccionesEnLinea`, `prepararAccionesEnLinea`: el botón Aprobar se bloquea con "Plan Aprobado" y "Ver Ordenes" solo se habilita con el plan aprobado; si no, tooltip "Plan no aprobado"). Cotización por correo a varios proveedores (inferido: el cliente solo carga `Cotizacion.aspx?IdPlanCompra` en un iframe). Cada línea guarda su orden generada y estado (inferido por columnas). Costo total = cantidad x costo unitario (corregido según código: `costoTotal`: la columna COSTOTOTAL llega calculada del servidor; el cliente solo la suma en el pie con `parseInt`, es decir en enteros).
- **Hallazgos del código**:
  - Mensajes: "Esta seguro de aprobar este plan de compra para generar una orden?"; "Esta seguro de eliminar este plan de compra?"; "Esta seguro de eliminar este detalle de plan de compra?"; "Esta seguro de aprobar el detalle de pedido para generar una orden de compra?"; sin proveedor al imprimir: "La orden no tiene un proveedor relacionado, por favor asigne uno a la orden!".
  - Aprobar un detalle abre una pestaña (`addTab`) para generar la orden; "Generar orden con seleccionados" solo se habilita si hay filas marcadas y la barra muestra "N Seleccionados." (`SelectCount`).
  - Color de fila: plan sin aprobar #f3f7d4, aprobado #d7e9ef (`getRowClassCompraPlan`); el detalle usa COMP_COLOR del servidor.
  - Servidor: `SRV.AprobarAID`, `SRV.Eliminar`, `SRV.EliminarDetalle`, `SRV.ExportarOrdenAExcel(id,"0")`, `SRV.GetToolbarOrdenes` (DirectMethod por componente).

## Compras > Órdenes de compra (/SUROSAlmacen/Vistas/Privado/CompraOrden/CompraOrden.aspx)
- **Propósito**: gestionar la orden de compra a proveedor y su recepción.
- **Funcionalidades**: El usuario puede crear/editar la orden; ordenar la compra; imprimir cotización y orden; adjuntar evidencia de pago y anexo de factura física; actualizar números de factura; "Recibir Compra" registrando novedades; eliminar.
- **Datos** (*Orden de Compra*): No. orden, Fecha Orden, Actividad, Impuesto, Fecha Vencimiento, Jefe de Compra, Almacén Compra, Estado {Planeado, Ordenado, Anulado, En Compra, Enviado, Recibido, Almacenado, Cotizado, Rechazado, Aplazado}, Aprobado, Aprobó, Observación, Proveedor, Método de pago {CONTADO, CREDITO}, Forma de pago {EFECTIVO, TARJETA DE CREDITO, TARJETA DÉBITO, CHEQUE}, Aplica Retención + Valor, Descuento, Dirección Despacho, Teléfono y correo de contacto (del proveedor), Dirección Entrega, Fecha Entrega, Persona que entregó, No. guía de embarque, Nota al proveedor. *Recibiendo Compra*: Observación de recibido, confirmación.
- **Listados**: No. | Fecha Orden | Proveedor | Método Pago | Estado | Encargado | Aprobado | Aprobó | Fecha Entrega. *Novedades en la Orden*: Tipo | Item | Presentación | Cant. Ordenada | Cant. Recibida | Cant. Faltante | Observación.
- **Flujos y reglas**: orden lineal de estados Planeado/Cotizado -> Ordenado -> En Compra -> Enviado -> Recibido -> Almacenado; Anulado/Rechazado/Aplazado como salidas (inferido; el cliente no conoce la secuencia). Lo que sí se ve en el cliente (corregido según código: `prepararAccionesEnLinea`): la interfaz solo distingue COMP_ID_ESTADO = 1 (se puede imprimir la cotización y "Ordenar"), = 2 (imprimir orden; "Recibir Compra" solo si COMP_APROBADO) y cualquier otro (solo imprimir orden y Kardex). La recepción compara ordenado vs recibido y registra faltantes (inferido por las columnas de *Novedades*). Al "Almacenado" se espera carga a inventario (inferido; ver Carga de inventarios, tipo FACTURA COMPRA).
- **Hallazgos del código**:
  - Ordenar: si el formulario no es válido, alert "Por favor diligencie todos los campos del formulario para continuar!"; si es válido, confirma "Esta seguro de ordenar esta compra?" -> `SRV.AprobarAID`. Imprimir orden sin proveedor: "La orden no tiene un proveedor relacionado, por favor asigne uno a la orden!".
  - Impresiones: orden (`SRV.ExportarOrdenAExcel(id,"0")`), cotización (`"1"`) y Kardex (`SRV.ExportarKardex` con los títulos "FORMATO DE RECEPCIÓN DE MEDICAMENTOS Y DISPOSITIVOS MEDICOS" y "KARDEX DE MEDICAMENTOS Y DISPOSITIVOS MEDICOS"), este último solo en estados distintos de 1 y 2.
  - Recibir: `compraOrden.PrepararRecibirCompraDesdeRegistro`. El anexo de factura se muestra en un iframe desde la carpeta temporal de facturas; si la orden no tiene archivo muestra un PDF tutorial por defecto. La evidencia de pago se abre en otra pestaña con IdOrdenCompra.
  - Notificación en tiempo real (`ActualizaListaOrdenes`): "Ha llegado un nuevo mensaje!" / "El usuario X ha generado una nueva orden de compra" (30 s) y refresco con `SRV.RefrescarDatosDesdeClienteExterno`.
  - Color de fila por estado: COMP_COLOR / COMP_COLOR_TEXT definidos en el servidor; las novedades se pintan #D9BBA9.

## Compras > Solicitudes (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/InventarioSolicitudPersonal.aspx)
- **Propósito**: solicitudes de suministros del funcionario a un área/almacén y control de lo recibido ("Mis solicitudes pendientes por recibir").
- **Funcionalidades**: El usuario puede crear solicitud, agregar detalles, cargar plantilla, guardar como plantilla, enviar, recibir seleccionados o todo, eliminar; filtrar por estado.
- **Datos** (*Solicitud de Suministros*): Fecha Solicitud, Solicitar al Área, Tipo, Suministro, Cantidad, Presentación; check "Es plantilla". Estados de solicitud {Solicitado, Pedido, Pendiente, Entregado, Entregado Parcialmente, Pendiente por Entregar, Anulado, Borrador, Consolidado, Rechazado, Entregado-Aprobado}. Estados de detalle {Solicitado, Pedido a almacen, No Disponible, Entregado, Rechazado, Recibido, Entrega Parcial}.
- **Listados**: Fecha Solicitud | Usuario Solicitó | Almacén Despacho | Usuario Despachó | Usuario Recibió | Estado; detalle: ID | Tipo | Suministro | Cant. Solicitada | Presentación | Cant. Entregada | Estado; paneles "Pendiente Por Pedir" y "Recibidos"; ventanas *Recibiendo*, *Aplicar Plantilla*, *Ayuda*.
- **Flujos y reglas**: borrador -> Enviar -> despacho (otra pantalla) -> confirmación de recibido por el solicitante (confirmado en código: `prepararAccionesEnLinea`, `ejecutarAccionesEnLinea`: con estado 1 a 4 la solicitud queda bloqueada, "Solicitud enviada!"; el detalle en estado 5 no se edita/elimina; con estado 9 se habilita recibir, "Entregado y listo para recibir!"). Alerta visual "Nuevos suministros entregados!" (inferido).
- **Hallazgos del código**:
  - Mensajes: "Esta seguro de enviar esta solicitud?" (`SRV.Enviar`), "Esta seguro de eliminar esta solicitud?", "Esta seguro de eliminar este detalle de la solicitud?". Tooltips: "Solicitud enviada. No se puede guardar cambios en el formulario!", "No se puede editar el detalle, ya se ha pedido!".
  - Recibir detalle: `SRV.PrepararReciboDetalle(id, item, cantidad solicitada)`.

## Compras > Pedido interno (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/PedidoInterno.aspx)
- **Propósito**: pedido entre almacenes (p. ej. farmacia a bodega).
- **Funcionalidades**: El usuario puede crear pedido, agregar detalle, cargar plantilla/guardar plantilla, enviar pedido, guardar, eliminar, rechazar (pedido o detalle con nota), recibir seleccionados/todo; filtrar por fechas, almacenes y usuarios.
- **Datos** (*Pedido Interno*): Fecha, Usuario Solicitó, Almacén Solicita, Almacén Entrega, Estado, Tipo {INSUMO, MEDICAMENTO}, Suministro, Cantidad, Presentación, Observación, Es plantilla. *Rechazando Pedido*/*Rechazando Detalle*: nota de rechazo.
- **Listados**: Id | Id | Fecha Solicitud | Almacén Solicita | Usuario Solicitó | Almacén Despacha | Usuario Despachó | Usuario Recibió | Estado; detalle: ID | Tipo | Suministro | Presentación | Cant. Solicitada | Entregado | Estado; panel "Pendiente Para Entrega".
- **Flujos y reglas**: el almacén destino despacha en "Despacho pedidos" (confirmado en código: `PedidoInternoDespacho.aspx` consume estos pedidos). Estados (corregido según código: `prepararAccionesEnLinea`): el cliente usa ids distintos a Solicitudes; en Pedido interno el estado 7 habilita "Recibir" ("Se encuentra entregado") y el 11 es Rechazado (botón de nota de rechazo visible, recibir deshabilitado con "Rechazado!"), mientras en Solicitudes el equivalente a entregado es el 9. La correspondencia id-nombre no está en el cliente.
- **Hallazgos del código**:
  - Mensajes: "Esta seguro de recibir este pedido?" (`SRV.RecibirPedido`), "Esta seguro de eliminar este pedido interno?". Impresión: `SRV.ImprimirOrdenFuncionario`. Si el pedido es un traslado a farmacia (INVE_ESTRASLADOAFARMACIA) la edición se prepara con `SRV.PrepararEdicion` hacia otro formulario (solicitud de farmacia).
  - Comentario del código: un pedido entregado y con INVE_APROBADO falso está "sin aprobación por validación de usuario"; en ese caso el botón queda "Entregado y listo para recibir!".
  - En el detalle, editar y eliminar pueden quedar deshabilitados con "No se puede editar!" / "No se puede eliminar".

## Compras > Despacho pedidos (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/PedidoInternoDespacho.aspx)
- **Propósito**: bodega/almacén despacha los pedidos internos contra existencias por lote.
- **Funcionalidades**: El usuario puede ver pedidos pendientes e historial; abrir uno; "Cargar Inventario" (asignar lotes); despachar seleccionado o todo; agregar detalle; guardar/terminar; rechazar pedido o detalle; ver entregas; generar ACTA DE ENTREGA; exportar; cancelar entrega; "RECIBIR Y FIRMAR"; gestionar devoluciones al inventario de farmacia; imprimir devoluciones.
- **Datos**: *Despacho Pedido Interno*: No, Fecha, Usuario Solicitó, Almacén Solicita, Bodega Despacha, Estado, Solicitante, Despacha, Fecha Solicitud. *Despachando Detalles*: Usuario, Contraseña (validación de recibido), check "Dejar en espera de recibido". *Ingresar credenciales*: nombre de usuario, contraseña. *Detalle de Solicitud*: Tipo, Item, Presentación, Cantidad Solicitada. *Rechazando*: nota.
- **Listados**: pedidos: No. Pedido | Fecha Solicitud | Almacén despacha | Usuario Solicitó | Almacén solicita | Usuario Despachó | Usuario Recibió | Estado (pendientes e histórico con filtros de fecha). Detalle: ID | Tipo | Suministro | Presentación | Cant. Solicitada | Cant. Entregada | Cant. a Despachar | Existencias | Estado. Selección de lote: Cant. Entrega | Item | Presentación | Lote | Fecha Venc. | Cant. Actual | Cant. Descargada | Cant. Almacenada. Devoluciones: Cantidad | Item | Paciente | Inventario | Fecha Entrega | Observación | TotalEntregado | TotalGastado.
- **Flujos y reglas**: el despachador elige lotes (corregido según código: `ConsultarItem`, `ejecutarAccionesEnLineaDetalle`: el cliente no ordena ni asigna lotes; consulta existencias por ítem con `SRV.ConsultarMedicamentosInventario`/`ConsultarInsumosInventario` y despacha con `SRV.PrepararDespachoDetalle(almacén, detalle, cantidad escrita en la fila, detalle de inventario, ítem, solicitante, existencias)`; el orden FEFO/FIFO, si existe, está en el servidor); descarga de bodega y carga a almacén destino (inferido); firma de entrega/recibo con usuario y contraseña (confirmado en código: `validarPendienteValidacion`, campos de credenciales y casilla "Dejar en espera de recibido" que las deshabilita); existe devolución desde farmacia a inventario con vínculo a paciente (inferido; el cliente solo tiene `Devolver` -> `SRV.DevolverPedido` y la impresión de devoluciones).
- **Hallazgos del código**:
  - Despachar un detalle se bloquea con "Se ha completado la entrega!" cuando entregada = solicitada; si (solicitada - entregada) > existencias el tooltip dice "No hay existencias suficientes en inventario de bodega para despachar este detalle!" (pero el código vuelve a habilitar el botón: la advertencia no bloquea). Con existencias = 0 aparece "Ir a cargas de inventario", que abre la pestaña CARGAR INVENTARIOS. Existencias se pintan verde (>0) o rojo.
  - Pedido en estado 11 (rechazado): "Pedido Rechazado!" y se deshabilitan despachar y rechazar. Rechazo de pedido o detalle exige nota: "Desea rechazar este pedido? \nPor favor escriba una nota de rechazo!" / "Desea rechazar este detalle de pedido? Por favor escriba una nota de rechazo!". Detalle en estado 12: sin edición ni despacho. Editar y eliminar detalle siempre deshabilitados ("No se permite edición de este detalle!").
  - Entregas canceladas: fila gris y botón deshabilitado con "Esta entrega ha sido cancelada y devuelta al inventario. Observacion: ..." (`prepararAccionesEnLineaLI`); `devolverInsumo` devuelve un insumo entregado. Acta: `SRV.IMPR(id)`.
  - La pantalla carga `md.js`, una implementación de MD5 en JavaScript (`calcMD5`) para credenciales; no se observa su invocación dentro del código de la página.

## Inventarios > Activación de cargas (/SUROSAlmacen/Vistas/Privado/InventarioBodega/ListarOrdenesInventario.aspx)
- **Propósito**: lista de órdenes de inventario (cargas) pendientes de aprobación/resolución entre origen y destino.
- **Funcionalidades**: El usuario puede solicitar productos a bodega, editar una orden si no está aprobada, resolver la orden, ver los suministros.
- **Datos**: ventana *Suministros* (solo lectura).
- **Listados**: ORDEN | FECHA | OBSERVACION | ESTADO | ORIGEN | DESTINO | REGISTRA | MODIFICA | FECHA CAMBIO; detalle: # | Suministro | Tipo | Cantidad | Precio de compra.
- **Flujos y reglas**: una orden nace como solicitud y se "resuelve" para activar la carga en destino. Confirmado en código: `Acciones`, `isvalido` (existen las acciones Editar -> `SRV.CargarOredenCrear`, Resolver -> `SRV.ResolverOrden`, Aprobar -> `SRV.ActivarOrden` con id y nombre de estado, y Ver pedido -> `SRV.CARGARPRODUCTOS`; Editar solo está habilitado mientras ORSO_ESTADO es falso). El efecto sobre el inventario de destino ocurre en el servidor (inferido).
- **Hallazgos del código**:
  - Fila lila (#ECDCF5) = orden pendiente (ORSO_ESTADO falso); verde (#DCF5E0) = orden resuelta. Las acciones Eliminar y MoverInventario están declaradas pero vacías.

## Inventarios > Ajuste (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioAjuste.aspx)
- **Propósito**: ajustes de inventario (conteos, daños, vencimientos, préstamos).
- **Funcionalidades**: El usuario puede buscar ajustes por fechas; crear ajuste; agregar ítems con cantidad nueva; definir datos de medicamento o insumo si no existe; guardar e imprimir.
- **Datos**: *Datos básicos del ajuste*: Fecha, Sede, Almacén, Categoría {AJUSTE PERIODICO, AJUSTE INPREVISTO, AJUSTE INCIAL INVENTARIO, AJUSTE POR OTROS MOTIVOS}, Observación general. *Ítem*: Item, Existente, Cantidad actual, Tipo de ajuste {DAÑOS, APROVECHAMIENTO, DESCUADRE, PRESTAMOS, VENCIMIENTO}, Observación, Und medida, Precio compra und, Cod barra, Fecha vencimiento, Centro de costo, Código referencia, Lote. *Datos específicos medicamentos*: Registro sanitario INVIMA, Estado {Vigente, Vencido, En trámite, No Aplica}, CUM, Expediente INVIMA, IUM, Cod ATC, Laboratorio, Marca, Controlado, Esencial, Institucional. *Insumo*: Marca, Cod referencia, Fecha vencimiento, Centro costo; grilla de características dinámicas (Nombre | Valor | Visible? | Búsqueda?) con subir/bajar fila y "Aplica para los siguientes vehículos" (resto de plantilla genérica).
- **Listados**: ID | NUMERO | FECHA | FECHA REGISTRO | Almacén | Tipo Item | Realizó; detalle: # | ITEM | NUEVA CANTIDAD | CATEGORIA | OBSERVACION; coincidencias: NOMBRE | TIPO | INPR_ID | REGISTRO | LOTE | PRECIO | COMPRADA | CANTIDAD.
- **Flujos y reglas**: el ajuste fija "nueva cantidad" por lote (inferido) y deja trazabilidad por motivo en cada línea (confirmado en código: `AgregarItemAjuste`, `GuardarAjuste`: cada ítem lleva CAOA_ID/CAOA_NOMBRE y observación).
- **Hallazgos del código**:
  - `AgregarItemAjuste`: si el formulario del ítem no es válido muestra 'Complar los espacios' / 'Complete los campos vacios'; si es válido inserta la línea (INPR_ID, ITEM, cantidad, motivo, observación) y limpia el formulario.
  - `GuardarAjuste` -> `SRV.GuardarAjuste` con FECHA, ALMACEN, TIPO, OBSERVACION e ITEMAJUSTE (lista de líneas). El cliente no valida que haya al menos una línea.

## Inventarios > Carga de inventarios (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioBodega.aspx)
- **Propósito**: ingresar existencias a bodega (o directo a almacén) por factura, donación, traslado, etc. Texto de ayuda: los inventarios se ingresan a la bodega y luego se hacen pedidos entre almacenes hacia la bodega.
- **Funcionalidades**: El usuario puede crear carga de insumos o medicamentos; importar por XLS; agregar ítems manualmente; editar el detalle de una carga con motivo de modificación; aprobar carga o "Aprobar y Enviar a Almacén"; guardar en bodega/almacén; crear proveedor, registro sanitario o laboratorio al vuelo; adjuntar archivos/imágenes de factura; registrar préstamos de suministros a entidades y devoluciones; exportar XLS (general por ítem, por almacén, reportes).
- **Datos**:
  - Cabecera: Fecha carga, Tipo cargue {FACTURA COMPRA, APROVECHAMIENTO, DONACIONES, TRASLADO, CARGUE INICIAL}, Tipo {MEDICAMENTO / INSUMO}, Sede, Bodega, Almacén, Fecha factura, No. factura, Proveedor, Observación.
  - Ítem: Item (búsqueda), Cant. und, Precio compra und, Und medida, Cod barra, Lote, Código referencia, Fecha vencimiento, Centro de costo, paneles Precio Venta e Impuesto. Datos específicos de medicamentos (registro INVIMA, estado, CUM, expediente, IUM, ATC, laboratorio, marca, controlado/esencial/institucional) e insumos (marca, fabricante).
  - Préstamo: check Prestamo, quién solicitó, No. documento. Detalle: Serial, Presentación, Costo unitario, Proveedor, Id factura, Ubicación, Cantidad.
  - Ventanas auxiliares: *Crear Proveedor* (prioridad, tipo persona/documento, razón social, nombre comercial, email, dirección, teléfonos, responsabilidades fiscales, municipio), *Nuevo Registro Sanitario* (registro, activo), *Datos del Laboratorio*, *Presentaciones*, *Municipio*, *Archivos*, *Edición de Carga* (motivo de modificación), *Actualizar cantidades en almacén*, *Ingresar credenciales*.
- **Listados**: ID | TIPO CARGUE | NUMERO FACTURA | FECHA FACTURA | FECHA CARGA | Fecha Inventario | Almacén | Tipo Item | Realizó | OBSERVACION | Aprobado en bodega. Detalle: ID | Item | Presentación | Lote | Fecha Venc. | Cant. | Costo Unit. | No. Factura | Ubicación | Total | Proveedor. Edición: ID | Item | Reg. Sanitario | Est. Reg. Sanitario | Centro Cost. | Marca | Laboratorio | Und. Medida | Cod. Barra | Cod. Ref | CUM | Lote | Fecha Venc. | Cant. | Costo Unit. | Total.
- **Flujos y reglas**: carga queda sin aprobar hasta "Aprobar Carga" (entra a existencias de bodega); "Aprobar y Enviar a Almacén" hace envío directo a farmacia (confirmado en código: `ejecutarAccionesEnLinea`, `prepararAccionesEnLinea`: una carga aprobada deshabilita aprobar y eliminar y el botón Editar pasa a "Visualizar Inventario"). Cada línea es un lote con vencimiento y ubicación (inferido por las columnas). La modificación posterior exige credenciales (confirmado en código: `ejecutarAccionesEnLinea`/`GEC`: Editar abre la ventana de credenciales y `SRV.PrepararEdicionCarge` recibe usuario y contraseña); el motivo de modificación no se observa en el cliente (inferido). Medicamentos exigen registro sanitario INVIMA, estado del registro, CUM y expediente (confirmado en código: `GuardarNuevoInventario`; el JS aplica estas validaciones sin distinguir tipo, la visibilidad de campos por tipo depende de `SRV.CambiarFields`).
- **Hallazgos del código**:
  - Validaciones al agregar ítem (`GuardarNuevoInventario`, cada una con foco al campo): 'Por favor Ingrese el ITEM!', 'Por favor Realice una consulta exacta!', 'Por favor Ingrese la(s) UNIDAD(ES)!', 'Por favor Ingrese el PRECIO DE COMPRA!', 'Por favor Ingrese la UNIDAD DE MEDIDA!', 'Por favor Ingrese el CENTRO DE COSTO!', 'Por favor Ingrese el REGISTRO SANITARIO!', 'Por favor Ingrese el ESTADO DEL REGISTRO SANITARIO!', 'Por favor Ingrese el CUM!', 'Por favor Ingrese el EXPEDIENTE INVIMA!'. Las validaciones de fecha, sede, bodega, factura y proveedor están comentadas (no se exigen en cliente).
  - Cálculo: total de la línea = unidades x precio de compra (PRCI_TOT). Precio de venta e impuesto se calculan en sub-paneles (`SRV.CargarInformacionBasica` con CATA_ID, unidad, precio actual y laboratorio) y viajan como JSON (valorinvent, IMPUESTO).
  - `GuardarCargaInventario`: si TICA = 4 (TRASLADO) la observación es obligatoria: "Es necesario ingresar en observacion de donde viene el traslado" (título 'Campo Vacio'). El guardado envía acción (guardar / aprobar / aprobar y enviar), factura, proveedor, sede, bodega, almacén y archivos.
  - Edición de carga: los campos de medicamento (CUM, expediente, IUM, ATC, laboratorio, registro, controlado, esencial, institucional) solo se muestran si TIIN_ID = 2 (medicamento). Al reducir la cantidad: 'La cantidad de inventario no puede ser menor a la que fue entregada.'; la cantidad en almacén nueva se calcula como nueva cantidad - ENTREGADOFARMACIA.
  - Eliminar detalle: confirma "Esta seguro de eliminar este detalle de inventario?", pero solo quita líneas aún no guardadas (INPR_ID vacío o -1); para las ya guardadas la llamada al servidor está comentada.
  - Alta rápida de proveedor (`GU` -> `SRV.RD`): 'Diligencie los campos obligatorios resaltados en rojo por favor.', 'Por favor Complete los datos basicos de una persona como el nombre y apellido ', 'Por favor Complete la razon social', 'Ingrese un numero telefonico', 'Seleccione el tipo de telefono'. Importar XLS: `SRV.CargarXLS("INVENTARIO")`. Ver archivos: `SRV.VerArchivos`; imprimir: `SRV.ImprimirCarga`.

## Inventarios > Informes gastos almacén (/SUROSAlmacen/Vistas/Privado/InventarioBodega/InventarioStock.aspx)
- **Propósito**: informe de consumo/stock por rango de fechas y horas.
- **Funcionalidades**: El usuario puede buscar entregas, visualizar y exportar el informe, guardarlo firmado con credenciales (validar responsable).
- **Datos**: Fecha inicial/final, Hora inicial/final, Tipo suministro {TODO, INSUMO, MEDICAMENTO}, Almacén, check Consumidos, validar responsable (usuario, contraseña).
- **Listados**: *Listado de entregas*: Código | RECIBE | ENTREGA | fecha registro. *Detalle de la entrega*: No | TIPOSUMINISTRO | SUMINISTRO | CANTIDAD INICIAL DEL RANGO | TRASLADO AL STOCK DURANTE EL RANGO | CANTIDADES CONSUMIDAS | VENDIDOS | CANTIDAD DISPONIBLE EN STOCK.
- **Flujos y reglas**: informe de cuadre de stock (inicial + traslados - consumo - ventas = disponible; la fórmula se calcula en el servidor, inferido), firmado por el responsable (confirmado en código: `GuardarCargaInventario` envía Responsable, validaresponsable, usuario y contraseña junto con el listado).
- **Hallazgos del código**:
  - `Consultar` -> `SRV.CargarHistorial_disponible`; `ConsultarExporte` -> `SRV.ExportarPdf`. Si el formulario no es válido: 'Complete los valores'. El indicador Consumidos se envía como '1'/'0'.

## Inventarios > Existencias en bodega > Insumos en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaInsumos.aspx)
- **Propósito**: consultar existencias de insumos por lote en bodega.
- **Funcionalidades**: El usuario puede filtrar (ítem, serial, lote, vencimiento, presentación, ubicación, proveedor, fabricante), ver solo con existencias, ver historial, exportar XLS detallado/por ítems, ver movimientos del lote (cargas y descargas) y dar de baja inventario.
- **Datos** (*Dar de baja*): Cantidad a descargar, Fecha descarga, Observación.
- **Listados**: Item | Serial | Lote | Fecha Vencimiento | Cant. Almacenada | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor | Fabricante. Paneles *Cargas al Lote* / *Descargas del Lote*.
- **Flujos y reglas**: Cant. Actual = almacenada - descargada (inferido).
- **Hallazgos del código**:
  - Cant. Actual la entrega el servidor (INVE_CANTIDAD_ACTUAL); el cliente solo suma los pies de Almacenado, Descargado y Actual (`parseInt`). Dar de baja -> `SRV.PrepararParaDarDeBaja(id, cantidad actual, ítem, lote)`; sin existencias el tooltip dice "No tiene existencias para dar de baja!" (pero el botón no se deshabilita). Movimientos del lote se cargan en iframes (cargas y descargas) por IdInventarioDetalle.

## Inventarios > Existencias en bodega > Medicamentos en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaMedicamentos.aspx)
- **Propósito**: igual que insumos, para medicamentos (con registro INVIMA y laboratorio).
- **Funcionalidades**: filtros, historial, XLS, movimientos del lote, dar de baja, y "Actualizar valores del inventario" (corrige un valor).
- **Datos**: ventana *Actualizando valores* (Valor a actualizar); *Dar de baja* (cantidad, fecha, observación); filtros incluyen Registro sanitario INVIMA, Laboratorio, Almacén, centro de costo.
- **Listados**: Item | Serial | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor | Laboratorio.
- **Hallazgos del código**:
  - "Actualizar valores del inventario" (`editarValores`) abre la ventana con el id del detalle; el guardado usa `SRV.ActualizarDetalleInventario` con INVE_CANTIDAD (valor a actualizar), es decir corrige la cantidad.

## Inventarios > Existencias en bodega > Suministros oficina en bodega (/SUROSAlmacen/Vistas/Privado/InventarioBodegaDetalle/InventarioBodegaEquiposOficina.aspx)
- **Propósito**: existencias de suministros de oficina en bodega.
- **Funcionalidades**: igual que insumos en bodega (filtros, historial, XLS, movimientos, dar de baja).
- **Listados**: Suministro | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor.

## Inventarios > Existencias en almacén > Insumos en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioInsumos.aspx)
- **Propósito**: existencias de insumos en un almacén (bodega/farmacia) con semaforización de vencimientos y descarga de consumo.
- **Funcionalidades**: El usuario puede filtrar por almacén y fechas (mes o rango); ver semáforo ROJO/AMARILLO/VERDE/VENCIDOS/TODOS; descargar, actualizar o cargar cantidades de un lote; entregar stock (recepción y entrega de almacén de stock); ver inventario actual, historial, reportes; generar códigos de barras unidosis.
- **Datos**: *Descargando del inventario*: Id detalle, Lote, Valor a descargar, Centro de costo, Funcionario que realiza descarga, Nota. *Actualizando valores*: valor a actualizar. *Cargando*: valor a cargar. *Creando código de barras Unidosis*: Código original, Cant. a generar, Valor inicial/final, Químico farmacéutico, Generar tarjeta / PDF / PDF rango.
- **Listados**: ID INSUMO | ID INVENTARIO PRODUCTO | Item | Cant. Almacenada | Cant. Desc. | Cant. Actual; *Códigos de barras*: Id | Código Original | Valor Inicial | Valor Final | Cant. Generada | Químico Farmacéutico | Generada | Aplicada.
- **Flujos y reglas**: semáforo por proximidad de vencimiento (confirmado en código: `getRowClassMPV`, `BuscarPorSemaforizacion`, ver Medicamentos en almacén; los umbrales son meses y llegan del servidor, sus valores no figuran en el cliente). Esta pantalla (Insumos en almacén) no tiene JavaScript propio. Unidosis = reempaque con código de barras propio (inferido) y firmado por el químico farmacéutico (corregido según código: `GuardarCodigoBarrasUnidosis`: el químico farmacéutico es opcional en el cliente, se envía '-1' si no se elige).

## Inventarios > Existencias en almacén > Medicamentos en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioMedicamentos.aspx)
- **Propósito**: existencias de medicamentos en almacén/farmacia, con precios y registro sanitario.
- **Funcionalidades**: las de insumos en almacén más precios, "Actualizar el serial del producto" y filtro por centro de costo.
- **Listados**: ID MEDICAMENTO | ID INVENTARIO PRODUCTO | NOMBRE | Código de Barras | LOTE | Fecha Venc. | Cant. Alm. | Precio Compra | Precio Venta | Reg.Inv. | Presentación | Cant. desc | Cant. Actual | Fecha Inventario | Proveedor | Laboratorio | Centro Costo.
- **Datos**: igual que insumos (descarga, actualizar, cargar, unidosis; muestra nombre, forma, concentración y presentación).
- **Hallazgos del código**:
  - Semáforo (`ValoresFechasSemaforo(RojoDesde, RojoHasta, AmarilloDesde, AmarilloHasta, VerdeDesde)` recibe meses desde el servidor): la clase de fila depende de la fecha de vencimiento frente a hoy + N meses: vencido (fecha < hoy) `Vencido-row`; entre Rojo desde/hasta `PorVencido-row` (ROJO); entre Amarillo desde/hasta `Porvencer-row` (AMARILLO); más allá de Verde desde `Bien-row` (VERDE). Los botones del semáforo consultan por rango con `SRV.BuscarPorRangoDeFechas`, VENCIDOS con `SRV.BuscarPorRangoDeFechasVencidos(hoy)`, TODOS con `SRV.RefrescarDatos`.
  - Descarga manual (`descargarDeInventario`): cantidad distinta de 0 -> 'Por favor ingrese una cantidad diferente para descargar!'; cantidad <= cantidad actual -> 'Por favor ingrese una cantidad menor que la cantidad actual para descargar!'; formulario válido -> 'Por favor ingrese todos los datos!'. Envía centro de costo, persona que descarga y nota con INVE_PEDIDO_INTERNO = 0 (descarga no ligada a pedido). Carga manual (`cargarAInventario`): 'Por favor ingrese una cantidad diferente para cargar!'; "Devolver a bodega" reutiliza la ventana de carga.
  - Unidosis: el botón solo aparece si el medicamento tiene dispensación unidosis (MECA_CONDISPENSACIONUNIDOSIS) y queda en solo consulta cuando INVE_UNIDOSIFICADO ("Unidosificacion completa. Solo se permite consultar!"). Valor final = valor inicial + cantidad generada - 1 (`CalcularValorFinal`); debe ser <= cantidad en almacén: "El valor final es mayor a la cantidad de existencias en almacen. Por favor escriba un valor menor para generar."; formulario incompleto: "Por favor complete el formulario?". PDF por rango: prompt 'Digite el rango de la forma "1,2"' con mensajes de rango inicial/final inválido. Tarjeta PDF: código original = lote. "Actualizar serial" solo se habilita si el lote no tiene serial: "Esta seguro de actualizar el codigo de barras del medicamento?". Marcar generación como aplicada: "Esta seguro de actualizar este generación como aplicado exitosamente?"; eliminar: "Esta seguro de eliminar este registro?".
  - Búsqueda por fecha de vencimiento: opción mes/año o rango; mensajes 'Seleccione una opcion fecha.', 'Seleccione el año', 'Seleccione el mes', 'Seleccione la fecha inicial', 'Seleccione la fecha final'. El botón de descarga rápida se oculta si la cantidad actual es 0.

## Inventarios > Existencias en almacén > Suministros oficina en almacén (/SUROSAlmacen/Vistas/Privado/InventarioDetalle/InventarioEquiposOficina.aspx)
- **Propósito**: existencias de suministros de oficina en almacén.
- **Funcionalidades**: filtros por fecha, descarga a centro de costo, actualizar/cargar, historial, XLS.
- **Listados**: Id | Item | Serial | Lote | Fecha Venc. | Cant. Alm. | Presentación | Cant. Desc. | Cant. Actual | Ubicación | Fecha Inventario | Proveedor.
- **Hallazgos del código**:
  - Variante simplificada: la descarga y la carga solo validan cantidad distinta de 0 y formulario válido; no comparan con la cantidad actual ni piden persona/nota. Sin semáforo propio.

## Terceros > Fabricantes (/SUROSAlmacen/Vistas/Privado/InventarioItemFabricante/InventarioItemFabricante.aspx)
- **Propósito**: maestro de fabricantes de productos.
- **Funcionalidades**: El usuario puede crear, editar, eliminar, filtrar.
- **Datos**: Fabricante, NIT, Teléfono contacto, Correo contacto, Observación.
- **Listados**: Fabricante | Nit | Teléfono Contacto | Correo Contacto | Observación.
- **Hallazgos del código**:
  - Activar: "Esta seguro de activar el fabricante?" (`SRV.AprobarAID`); eliminar: "Esta seguro de eliminar este fabricante?".

## Terceros > Laboratorios (/SUROSAlmacen/Vistas/Privado/InventarioItemLaboratorio/InventarioItemLaboratorio.aspx)
- **Propósito**: maestro de laboratorios (instituciones que diseñan y elaboran medicamentos e insumos).
- **Funcionalidades**: crear, editar, eliminar, filtrar.
- **Datos**: Nombre, NIT, Teléfono, Correo, Observación, Dirección.
- **Listados**: Nombre | Nit | Correo Contacto | Teléfono | Observación | Dirección.
- **Hallazgos del código**:
  - Eliminar: "Esta seguro de eliminar este laboratorio?".

## Terceros > Proveedores (/SUROSAlmacen/Vistas/Privado/InventarioItemProveedor/InventarioItemProveedor.aspx)
- **Propósito**: maestro de proveedores con datos fiscales, de contacto y bancarios.
- **Funcionalidades**: El usuario puede crear/editar/eliminar proveedor; asociar tipos de inventario que suministra; buscar municipio; adjuntar cuentas bancarias; marcar "Enviar Precios".
- **Datos**: Tipo de documento (13 tipos: cédula, NIT, pasaporte, registro civil, TI, extranjería, PEP, PPT, etc.), Documento, Representante, Empresa, Contribuyente {Persona Natural, Persona Jurídica}, Régimen (lista de ~18 valores: común, simplificado, especial, contributivo, subsidiado, vinculado, particular, etc.), Sitio web, Tipos de inventario; *Empresarial*: teléfono, correo, fax, municipio, dirección; Enviar precios; *Bancaria*: cuentas (número, titular, tipo {Corrientes, Remunerada o Ahorros, Nómina, Vivienda}, banco); Observación.
- **Listados**: Representante | NIT | Teléfono | Correo | Empresa | Tipo Contribuyente | Régimen | Dirección | Enviar Precios; cuentas: Cuenta | Titular | Tipo de Cuenta | Banco.
- **Flujos y reglas (inferido)**: "Enviar Precios" probablemente incluye al proveedor en las solicitudes de cotización.
- **Hallazgos del código**:
  - Mensajes: "Esta seguro de aprobar el proveedor?", "Esta seguro de eliminar este proveedor?", 'Seleccione un municipio para continuar.', 'El tipo X ya está en la lista.', 'Es necesario que escriba un parámetro de búsqueda.'. Consulta por documento: `SRV.consultarDocumento`. No hay lógica de cliente para "Enviar Precios" (su uso en cotizaciones sigue sin evidencia).

## Farmacia (/SUROSAlmacen/Vistas/Privado/SolicitudMedicamentosEInsumos/Farmacia.aspx)
- **Propósito**: panel del regente de farmacia: recibe solicitudes de medicamentos e insumos por paciente, dispensa con acta de entrega, controla aplicación y devoluciones.
- **Funcionalidades**: El usuario puede buscar paciente (por tipo y dato de documento, búsqueda general); crear solicitud (medicamentos + insumos, estancia, profesional que solicita, observación) y "Guardar y Enviar"; ver historial del paciente; abrir panel de solicitudes y filtrar por fecha; generar ACTA DE ENTREGA (No. entrega, ciudad, fecha); ENTREGAR Y FIRMAR / CANCELAR ENTREGA; ENTREGAR TODO; ver tratamientos (último o todos) con posología, suministrado, aplicado y última aplicación; ver insumos usados; registrar aplicación de medicamentos; cargar inventario; descarga masiva; cargar y consultar devoluciones (incluir aceptadas) e historial; nueva entrega anticipada; reportes (aplicación de medicamentos, controlados, entrega de controlados) por mes o rango; accesos por área (OBSERVACIÓN, HOSPITALIZACIÓN, CIRUGIA); botón App. HD.
- **Datos**: Solicitud: Estancia, Profesional solicita, Observación. Paciente: nombre, documento, EPS de afiliación/ingreso (solo lectura). Acta de entrega: tipo, No. de entrega, ciudad (municipio), fecha. Estados de solicitud {Formulada, Recibida, Entrega Parcial, Entrega Total, Cancelada}. Tipo de documento abreviado {AS, CC, CE, MS, NT, PA, RC, TI, TE, NV, PEP, PPT, PT}. Almacén {BODEGA, FARMACIA}.
- **Listados**: *SOLICITUDES A LA FARMACIA*: Fecha Solicitud | T.D. | Documento | Paciente | Regente | Médico | Estancia | Estado | T. Insumos | T. Medicamentos. *MEDICAMENTOS* de solicitud: ID | Descripción | Forma | Concentración | Presentación | Cantidad | Und/Med | Observaciones. *INSUMOS*: Insumo | Presentación | Cantidad Solicitada | Observación. Acta: # | Registro INVIMA | CUM | Lote | F. Vencimiento | Medicamento | Forma | Concentración | C/Formulada | C/Entregada. Tratamientos: Posología | Total Suministrado | Aplicados | Total a aplicar | Última aplicación. *HISTORIAL DE DEVOLUCIONES* (mismas columnas que solicitudes). Coincidencias de medicamentos/insumos con existencias.
- **Flujos y reglas**: Formulada (por médico en HC) -> Recibida -> Entrega Parcial/Total (inferido); el acta registra registro INVIMA, CUM y lote entregado (trazabilidad, inferido por las columnas); control especial de medicamentos controlados (inferido); descarga de existencias por lote al entregar (confirmado en código: `consultarExistencias`, `consultarExistenciasInsumos`: al elegir un ítem de la solicitud se carga la lista de lotes de ese ítem con CantidadADescargar = cantidad pedida - cantidad entregada; el lote se escoge en esa lista, sin orden automático en el cliente); las devoluciones regresan al inventario de farmacia (inferido); "entrega anticipada" permite dispensar sin fórmula previa (inferido; en el cliente solo se confirma que existe como pestaña `pnlEntregaAnticipada`, ver `recargarPaneles`).
- **Hallazgos del código**:
  - Cancelar solicitud (de canasta): si PORCENTAJE > 0 -> 'Esta solicitud ya tiene medicamentos o insumos entregados, es necesario devolverlos para cancelar esta solicitud.'; si no -> "Esta seguro de cancelar esta solicitud de canasta?" -> `SRV.CancelarSolicitud`. Eliminar detalle: "Esta seguro de eliminar este detalle?".
  - Buscar paciente: 'Por favor, ingrese un número de documento valido!'. Cantidad a descargar: 'La cantidad a descargar no debe ser un número negativo!' (`validarEntero`, solo dígitos).
  - Acta de entrega (`CrearActaEntregaDb`): tipo 0 -> `SRV.GuardarActa` (ciudad-departamento, número de acta, fecha, solicitud); otro tipo -> acta descentralizada `SRV.GuardarActaDescentralizada` con la cantidad por lote (DTAE_CANTIDAD) de cada medicamento. Municipio obligatorio: 'Seleccione un municipio para continuar.'
  - Pestañas de dispensación recargables: Observación, Hospitalización, Cirugía, Entrega anticipada, Stock canastas y Salida (mensaje 'Paneles actualizados!'). Las canastas de cirugía alimentan la pestaña Stock canastas.
  - Filas del tratamiento: suspendido (ESTR_ID = 2) `suspende-row`; aplicados = total formulado `new-row`; aplicados > total `supera-row` (se aplicó más de lo formulado). 'SIN APLICAR' se pinta en rojo (`CantidadF`).
  - Tiempo real: al llegar un pedido se muestra 'Ha llegado un nuevo pedido!' / 'El usuario X ha realizado un pedido', se reproduce un audio y se avisa al panel del enfermero (`AccionSGR` TIPO 11 al preparar la entrega, TIPO 19 al refrescar la lista externa). Los datos de la solicitud viajan con paciente, EPS de ingreso, área asistencial y fecha (`SRV.PrepararDetalles`, `SRV.PrepararDetallesADevolver`).

## Enfermería (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/InventarioSolicitudInsumos.aspx)
- **Propósito**: enfermería solicita insumos a un almacén, normalmente asociados a un paciente.
- **Funcionalidades**: El usuario puede crear pedido, usar "Mis Plantillas", cargar plantilla, buscar insumos (coincidencias con existencias), enviar/guardar/eliminar pedido, recibir seleccionados/todo, ver todos los pedidos, ver videotutorial.
- **Datos**: Solicitar a almacén, check Es plantilla; filtros por paciente, fecha, usuario, almacén, estado (mismos catálogos de estados).
- **Listados**: pedido: Código | Insumo | Presentación | Solicitada | Entregada | Estado | Observación; pedidos: ID | Paciente | Fecha Solicitud | Usuario Solicitó | Farmacia Despachó | Regente Despachó | Enfermero | Estado; coincidencias: ID | Código | Nombre | Presentación | Existencias.
- **Hallazgos del código**:
  - Enviar (`ejecutarAccionesEnLinea`): si el paciente no tiene destino: '<br>El paciente no presenta un destino!</br>'; si lo tiene, "Esta seguro de enviar esta solicitud de pedido?" -> `SRV.EnviarPedido(solicitud, PACIID, DEPCID, INGRID, HISTID)`, tomando paciente, destino, ingreso e historia del contexto de la historia clínica (`parent.ID`).
  - Estados 1 a 4 = enviada (se deshabilitan enviar y eliminar); estado 9 en detalle = entregado y listo para recibir. `GuardarSolicitud` solo envía si la grilla tiene al menos un insumo. Eliminar: "Esta seguro de eliminar esta solicitud?".

## Tienda en línea (/SUROSAlmacen/Vistas/Privado/Inventario/TiendaEnLinea.aspx)
- **Propósito**: no determinado; presumiblemente venta en línea de productos del inventario (inferido por el nombre y la columna "VENDIDOS" del informe de gastos).
- **Hallazgos del código**: la página no tiene JavaScript propio ("sin funciones propias"); el menú de inicio colapsa el panel lateral al abrirla (`CelClic`), igual que Farmacia.
- **Funcionalidades**: no extraíble: la página devolvió error de servidor ("Index was outside the bounds of the array") al extraer. Defecto de la instalación original, no una funcionalidad.

## Configuración > Categorías (/SUROSAlmacen/Vistas/Privado/InventarioItemCategoria/InventarioItemCategoria.aspx)
- **Propósito**: categorías de ítems de inventario.
- **Funcionalidades**: crear, editar, eliminar, filtrar.
- **Datos**: Categoría, Descripción, Tipo (de inventario), Requiere mantenimiento.
- **Listados**: Categoría | Descripción | Tipo | Req. Manten.
- **Hallazgos del código**:
  - Eliminar: "Esta seguro de eliminar esta categoria?".

## Configuración > Centros de costo (/SUROSAlmacen/Vistas/Privado/ContabilidadCentroCosto/ContabilidadCentroCosto.aspx)
- **Propósito**: centros de costo contables a los que se imputan cargas y descargas.
- **Datos**: Centro costo, Descripción. **Listados**: Id | Centro Costo | Descripción.
- **Funcionalidades**: crear, guardar, eliminar, filtrar.
- **Hallazgos del código**:
  - Un centro aprobado queda de solo lectura: se deshabilitan aprobar, guardar y eliminar (tooltip "Aprobado"). Mensajes: "Esta seguro de aprobar este centro de costo?", "Esta seguro de eliminar este centro costo?".

## Configuración > Estados de pedido (/SUROSAlmacen/Vistas/Privado/InventarioSolicitudEstado/InventarioSolicitudEstado.aspx)
- **Propósito**: catálogo de estados de solicitud/pedido con color para la UI.
- **Datos**: Estado, Descripción, Color. **Listados**: Id | Estado | Descripción | Color.
- **Funcionalidades**: editar, guardar, eliminar, aprobar (botón presente en ventana).
- **Hallazgos del código**:
  - Aprobar: "Esta seguro de aprobar la InventarioSolicitudEstado?" (texto genérico heredado).

## Configuración > Parámetros de configuración (/SUROSAlmacen/Vistas/Privado/ParametroConfiguracion/ParametroConfiguracion.aspx)
- **Propósito**: parámetros clave-valor del módulo, restringidos por rol.
- **Datos** (*Detalle del parámetro*): Configuración, Valor, Tipo de dato, Descripción, Roles, Activo.
- **Listados**: ID | Configuración | Valor | Tipo Dato | Roles | Registrado Por | Fecha Creación.
- **Funcionalidades**: nuevo, guardar, cancelar, eliminar, imprimir, aprobar.
- **Hallazgos del código**:
  - Activar: "Esta seguro de activar el parametro de configuración ?" (`SRV.AprobarAID`).

## Configuración > Presentaciones (/SUROSAlmacen/Vistas/Privado/InventarioItemPresentacion/InventarioItemPresentacion.aspx)
- **Propósito**: presentaciones/empaques de los ítems (caja, frasco, etc.) con dimensiones.
- **Datos**: Tipo de empaque, Unidades, Ancho/Alto/Espesor (cm), Volumen|Peso (ML, CC, GR), Unidad de medida, Activo, Descripción, Tipos de inventario a los que aplica, foto (ventana *Actualizando Foto*).
- **Listados**: ID | Imagen | Nombre | Dimensiones | Tipo | Cant. de Unidades | Alto | Ancho | Espesor | Volumen/Peso | Aplica a Tipos | Activo.
- **Funcionalidades**: crear, editar, activar/desactivar, eliminar.
- **Hallazgos del código**:
  - Activar/desactivar: "Esta seguro de activar la presentación?" / "Esta seguro de desactivar la presentación?"; eliminar: "Esta seguro de eliminar esta presentación? <br> <b>Se desvinculara de las listas relacionadas. </b>" (`SRV.EliminarPresentacion`). Foto: `SRV.CargarImagen`. Tipos de inventario: 'El tipo X ya está en la lista.'.

## Configuración > Empresa (/SUROSAlmacen/Vistas/Privado/Empresa/PanelEmpresas.aspx)
- **Propósito**: panel de empresas; solo se observan accesos de alta.
- **Funcionalidades**: El usuario puede crear "Nueva Empresa Proveedora" y "Nueva EPS" y refrescar la lista. Sin campos extraídos (confirmado en código: `nuevaEmpresa`: el formulario vive en sub-paneles `pnlProveedoras` y `pnlEps` que exponen `empresa.Nuevo()`; no es JavaScript de esta página).

## Configuración > Almacenes (/SUROSAlmacen/Vistas/Privado/Almacen/Almacen.aspx)
- **Propósito**: maestro de almacenes/bodegas/farmacias por sede.
- **Datos** (*Detalle del Almacén*): Imagen, Área (m), Nombre, Descripción, Sede, Observaciones, Encargado, Tipo {Bodega, Almacén, Almacén Virtual, Farmacia}, Teléfono, Correo contacto, Estado {Activo, En Mantenimiento, Inactivo, Clausurado}, Último inventario, Fecha último mantenimiento.
- **Listados**: Nombre | Sede | Observaciones | Tel. | Estado | Tipo.
- **Funcionalidades**: nuevo, guardar, eliminar, filtrar.
- **Hallazgos del código**:
  - Activar: "Esta seguro de aprobar la Almacen?" (`SRV.AprobarAID`). Los accesos Ver existencias, Entradas y salidas, Pedidos internos, Planes de compra y Ubicaciones están siempre deshabilitados (`prepararAccionesEnLinea`, funciones no implementadas). La imagen se muestra en base64 (40x20) y se sube con `SRV.CargarImagen`.

## Configuración > Canastas de cirugía (/SUROSAlmacen/Vistas/Privado/InventarioSolicitud/CanastasCirugias.aspx)
- **Propósito**: plantillas de suministros por procedimiento quirúrgico y médico.
- **Funcionalidades**: El usuario puede crear una canasta, elegir el procedimiento (ventana de selección), farmacia y médico, agregar detalle (tipo, suministro, cantidad, presentación), guardar, eliminar.
- **Listados**: Procedimiento Quirúrgico | Médico | Fecha Creación | Usuario Diseño; detalle: Tipo de suministro | Suministro | Presentación | Cant. Solicitada; procedimientos: Código | Descripción.
- **Flujos y reglas**: la canasta se usa para solicitar/dispensar de una vez los insumos de una cirugía (confirmado en código: `prepararEliminacion` y `recargarPaneles` de Farmacia manejan "solicitud de canasta" y la pestaña Stock canastas).
- **Hallazgos del código**:
  - Además de eliminar ("Esta seguro de eliminar esta solicitud?") permite clonar: "Esta seguro de clonar esta Canasta de cirugia?" (`SRV.ClonarCanasta`). Buscar procedimiento con Enter (`SRV.BuscarProcedimiento`); el indicador de contratación de medicamentos del panel Stock canastas viaja a `Eliminar`/`ClonarCanasta`.

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

Verificación en código: los pasos 1 y 3 (aprobación de plan y orden), 4 (aprobar carga / enviar a almacén con credenciales), 5 (despacho con credenciales y rechazo con nota) y 6 (descarga por lote en Farmacia, solicitud de enfermería con contexto de historia clínica) están respaldados por las funciones citadas en cada pantalla. El paso 2 (cotización por correo) y la conciliación del paso 7 en el servidor no son visibles en el cliente.

## Entidades y estados

Entidades (inferidas de campos y IDs): Plan de compra (+ detalle), Orden de compra (+ novedades), Solicitud/Pedido interno (+ detalle, plantilla), Orden de inventario/Carga (+ detalle por lote, archivos adjuntos), Ajuste (+ detalle), Inventario detalle (lote por ubicación), Ítem de inventario (insumo, medicamento, suministro de oficina), Medicamento catálogo (forma, concentración, presentación, volumen, principio activo, homologación), Categoría, Presentación, Tipo de inventario, Registro sanitario INVIMA, Fabricante, Laboratorio, Proveedor (+ cuentas bancarias), Empresa (proveedora/EPS), Almacén, Sede, Centro de costo, Código de barras unidosis, Solicitud de farmacia (+ acta de entrega, devolución), Canasta de cirugía, Parámetro de configuración.

Estados:
- Orden de compra: Planeado, Ordenado, Anulado, En Compra, Enviado, Recibido, Almacenado, Cotizado, Rechazado, Aplazado.
- Solicitud/pedido: Solicitado, Pedido, Pendiente, Entregado, Entregado Parcialmente, Pendiente por Entregar, Anulado, Borrador, Consolidado, Rechazado, Entregado-Aprobado.
- Detalle de solicitud: Solicitado, Pedido a almacén, No Disponible, Entregado, Rechazado, Recibido, Entrega Parcial.
- Solicitud de farmacia: Formulada, Recibida, Entrega Parcial, Entrega Total, Cancelada.
- Registro sanitario: Vigente, Vencido, En trámite, No Aplica.
- Almacén: Activo, En Mantenimiento, Inactivo, Clausurado; tipos Bodega, Almacén, Almacén Virtual, Farmacia.
- Ids de estado usados por el cliente: Solicitud 1-4 enviada, 5 detalle entregado, 9 entregado/listo para recibir; Pedido interno 7 entregado y 11 rechazado; Despacho de detalle 12 bloqueado; Orden de compra 1 cotización/por ordenar, 2 ordenada. El nombre asociado a cada id está en el catálogo de estados del servidor.
- Carga: aprobada / no aprobada en bodega. Presentación: activa/inactiva.
- Tipos de cargue: FACTURA COMPRA, APROVECHAMIENTO, DONACIONES, TRASLADO, CARGUE INICIAL. Tipos de ajuste: DAÑOS, APROVECHAMIENTO, DESCUADRE, PRESTAMOS, VENCIMIENTO. Categorías de ajuste: PERIODICO, IMPREVISTO, INICIAL, OTROS MOTIVOS.
- Pago: CONTADO/CREDITO; forma EFECTIVO, TARJETA DE CREDITO, TARJETA DEBITO, CHEQUE.

## Página web (CMS)

Sub-app `/SUROSPaginaWeb` (entrada `/SUROSPaginaWeb/Vistas/InicioPaginaWeb.aspx`). El árbol de menú no mostró hojas y las pantallas no fueron extraídas. Se sabe solo que existe la entrada de inicio de un CMS del sitio web de la institución (inferido por el nombre). No hay funcionalidades confirmadas.
- **Hallazgos del código**: el JavaScript de `InicioPaginaWeb.aspx` es la misma carcasa que usan los otros módulos (`CargaTab`, `CelClic`, cambio de contraseña `CP` con mínimo 6 caracteres, salir de sesión "Esta seguro de salir de la Sesión?", contador de mensajes de chat pendientes `cargarMensajesPendientes` hacia la pizarra de chat y aviso sonoro). No contiene código de edición de contenido web, por lo que el carácter de CMS sigue sin evidencia.

## Preguntas abiertas

### Respondidas

1. **Semáforo de vencimientos**: ¿umbrales? Respuesta: se miden en meses contados desde hoy y llegan del servidor (`ValoresFechasSemaforo`); VENCIDO = fecha < hoy, ROJO entre Rojo desde/hasta, AMARILLO entre Amarillo desde/hasta, VERDE más allá de Verde desde; el cliente no bloquea el uso de lotes vencidos. Fuente: código: `getRowClassMPV`, `BuscarPorSemaforizacion`. Solo existe lógica propia en Medicamentos en almacén; Insumos en almacén no tiene JS.
2. **Selección de lote al dispensar/despachar**: el cliente no aplica FEFO/FIFO; en Farmacia carga la lista de lotes del ítem con la cantidad pendiente y el usuario elige (código: `consultarExistencias`); en Despacho consulta existencias por ítem y despacha con la cantidad escrita (código: `ConsultarItem`, `PrepararDespachoDetalle`). Práctica esperada: FEFO, primero en vencer primero en salir (supuesto estándar del sector).
3. **Qué habilita cada estado en pantalla**: Orden de compra 1 permite ordenar e imprimir cotización, 2 permite recibir solo si está aprobada, otros solo imprimen/Kardex (código: `prepararAccionesEnLinea` de CompraOrden). Solicitud: 1-4 bloquea edición, detalle 5 no se edita, 9 habilita recibir (código: `prepararAccionesEnLinea` de Solicitudes y Enfermería). Pedido interno: 7 habilita recibir, 11 rechazado con nota (código: `prepararAccionesEnLinea` de PedidoInterno). Despacho: detalle 12 bloqueado, pedido 11 sin despacho (código: `prepararAccionesEnLineaDetalle`).
4. **Entregado-Aprobado**: según el comentario del código, un pedido entregado con INVE_APROBADO falso está sin aprobación por validación de usuario; "aprobado" equivale a recibido y validado con las credenciales del receptor (código: `prepararAccionesEnLinea` de PedidoInterno).
5. **Vínculo con Historia Clínica (solicitud de insumos)**: Enfermería envía el pedido con paciente, destino, ingreso e historia tomados del contexto de la HC (`parent.ID`) y exige que el paciente tenga destino (código: `ejecutarAccionesEnLinea` de InventarioSolicitudInsumos). Farmacia se entera en tiempo real y a su vez avisa al panel del enfermero (código: `AccionSGR` TIPO 11/19 en `prepararEntrega`).
6. **Medicamentos (Facturación) vs catálogo nuevo**: el catálogo nuevo referencia los nombres de Facturación por MEDA_ID (nombre del medicamento y lista de principios activos) y ambos manejan un código único UUID generado en el navegador (código: `guardarnuevocatalogomedicamento`, `AgignarPrincipioActivo`, `guardarHomologacion` de Medamento).
7. **Validaciones regulatorias en la carga de medicamentos**: el cliente exige registro sanitario INVIMA, estado del registro, CUM y expediente INVIMA, y guarda los indicadores Controlado, Esencial e Institucional por lote; el catálogo tiene la marca Controlado (código: `GuardarNuevoInventario`, `guardarnuevocatalogomedicamento`). Marco: registro sanitario INVIMA (norma: Decreto 677/1995), control de medicamentos de control especial (norma: Res. 1478/2006) y condiciones del servicio farmacéutico y almacenamiento (norma: Res. 1403/2007).
8. **Unidosis**: se genera una secuencia de códigos de barras (valor inicial, cantidad, valor final = inicial + cantidad - 1) limitada a las existencias del almacén, con PDF por tarjeta o por rango y opción de marcar la generación como aplicada; el químico farmacéutico es opcional en el cliente y la función solo aplica a medicamentos con dispensación unidosis (código: `CalcularValorFinal`, `GuardarCodigoBarrasUnidosis`, `prepararAccionesEnLinea`).
9. **Activación de cargas**: existen las acciones Editar, Resolver, Aprobar (activar) y Ver pedido; solo se edita mientras la orden no está resuelta, ORSO_ESTADO falso (código: `Acciones`, `isvalido`).

### Sin respuesta por ingeniería inversa

1. **Tienda en línea**: ¿qué vende, con qué precios, impuestos y pasarela? La página falla en origen y no tiene JavaScript propio. Motivo: sin acceso.
2. **Valores de los umbrales del semáforo, orden real de los lotes (FEFO/FIFO) y comportamiento al vencer**: los meses de cada color y el orden de la lista de lotes los define el servidor. Motivo: lógica del servidor.
3. **Quién puede aprobar cada paso y qué dispara el estado Consolidado**: los roles y las transiciones no están en el cliente. Motivo: lógica del servidor.
4. **Creación de la solicitud "Formulada" desde la HC y facturación de lo dispensado**: no hay llamadas de ese tipo en estas pantallas. Motivo: lógica del servidor (y requiere paciente real para observarlo).
5. **Contenido exacto de los reportes de controlados y entrega de controlados**: solo se conoce que existen en Farmacia. Motivo: lógica del servidor.
6. **Préstamos de suministros entre entidades**: el cliente solo referencia el indicador INVE_VIENE_DE_PRESTAMO. Motivo: lógica del servidor.
7. **Carpeta OLD del menú de inventarios**: sin hojas listadas. Motivo: sin acceso.
