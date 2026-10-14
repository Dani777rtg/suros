# Configuración, seguridad, herramientas y pacientes

Resumen: este bloque cubre la parametrización del sistema (entidad, especialidades, laboratorio, subplanes, páginas), la seguridad (funcionarios, usuarios, roles, módulos, informes por usuario, sesiones activas), las herramientas (unificación de historias, consentimientos), la cuenta propia y el maestro de pacientes. 21 pantallas. Empresas y Datos personales venían sin extracción de UI y Configuración General casi vacía; el código JS de cliente permitió reconstruir su comportamiento. Fuente: extracción de UI (Ext.NET) y código JavaScript de cliente (`pantallas/_codigo-js.md`); lo no verificable sigue marcado "(inferido)". Marcas: "(confirmado en código: `funcion`)" y "(corregido según código: `funcion`)". Lo que ocurre en el servidor (reglas, tablas) no es visible desde el cliente.

Ruidos globales omitidos: messagebox, OK/Yes/No/Cancel, paginación, ordenar/columnas.

---

## CONFIGURACION GENERAL > CONFIGURACIÓN GENERAL (/SUROS/Vistas/Privado/General/ConfiguracionGeneral.aspx)
- **Propósito**: editar parámetros generales del sistema; cada configuración es un registro (`COGE_ID`) cuya descripción se edita como texto estructurado en un editor de JSON, no como clave/valor simple (corregido según código: `GD`, `editor.getText()`).
- **Funcionalidades**: el usuario puede ver la lista de configuraciones, editar una configuración seleccionada ("Editar esta configuración") y guardar ("Guardar Configuracion").
- **Datos**: sin campos extraídos en la UI; la edición se abre desde la acción de fila "Editar", que carga el registro en un editor de texto (confirmado en código: `ejecutarAccionesEnLinea` -> `CargaInformacionPorId`).
- **Listados**: grid con Id, Configuración.
- **Flujos y reglas**: seleccionar fila, editar, guardar (confirmado en código: `GD` envía `COGE_ID` y `COGE_DESCRIPCION` a `GCG`). Pantalla casi vacía en la extracción.
- **Hallazgos del código**:
  - Servidor: `CargaInformacionPorId(id)`, `GCG({COGE_ID, COGE_DESCRIPCION})`.
  - No hay validación de cliente antes de guardar; el contenido es el texto del editor (JSONEditor) y su validez la decide el servidor.

## CONFIGURACION GENERAL > FUNCIONARIO > GESTIONAR DATOS FUNCIONARIO (/SUROSHistoriaClinica/Vistas/Privado/Funcionario/FormularioFuncionario.aspx)
- **Propósito**: crear y editar la ficha de funcionarios (personal asistencial/administrativo) incluida su información médica.
- **Funcionalidades**: el usuario puede buscar funcionario por documento/nombre ("Buscar funcionario"; ventana "Coincidencia encontrada" con lista de resultados); guardar cambios; cancelar; limpiar formulario; buscar municipio de nacimiento/residencia (ventana "Municipio" con País/Departamento/Municipio); subir archivo (firma; ventanas "Seleccionar firma" y "Asignar firma"); adicionar especialidad (ventana "Especialidad medica") y adicionar convenio (ventana "Convenios", lista de empresas); seleccionar programas PyP asociados (ventana "Seleccionar los programas asociados"); cambiar estado.
- **Datos**:
  - Identificación: tipo documento {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}, documento, primer/segundo nombre, primer/segundo apellido.
  - Demografía: género {MASCULINO, FEMENINO, INDETERMINADO O INTERSEXUAL}, fecha de nacimiento, etnia {OTRAS ETNIAS, INDIGENA, RAIZAL, GITANO, PALENQUERO DE SAN BASILIO, NEGRO/MULATO/AFROCOLOMBIANO/AFRODESCENDIENTE, AFROCOLOMBIANO}, estado civil {ESTADO NO SUMINISTRADO, CASADO(A), DIVORCIADO(A), MENOR DE EDAD, SOLTERO(A), UNION LIBRE, VIUDO}, discapacidad {FÍSICA, VISUAL, AUDITIVA, INTELECTUAL, SICOSOCIAL, SORDOCEGUERA, MÚLTIPLE, SIN DISCAPACIDAD}, nivel educativo {NO DEFINIDO, PRESCOLAR, BASICA PRIMARIA, BASICA SECUNDARIA, MEDIA ACADEMICA O CLASICA, MEDIA TECNICA, NORMALISTA, TECNICA PROFESIONAL, TECNOLOGICA, PROFESIONAL, ESPECIALIZACION, MAESTRIA, DOCTORADO}.
  - Contacto/ubicación: municipio de nacimiento, municipio de residencia, dirección/barrio, celular, teléfono, email.
  - Laboral: ocupación, cargo, empresa, estado {ACTIVO, INACTIVO}, "Es medico" {SI, NO}.
  - Información general del médico (fieldset): registro profesional, licencia de salud ocupacional.
  - Ventana de especialidad: estado {ACTIVO, INACTIVO}, cirugía {SI, NO}, PyP {SI, NO} (confirmado en código: `change`, `changeCirugia`, `changeAplicaProgramaPYP`).
  - Ventana Convenios: empresa.
- **Listados**: especialidades del funcionario (Especialidad, Estado, Cirugia, PyP); convenios (Convenio); programas PyP (PROGRAMA PYP); coincidencias (DOCUMENTO, NOMBRE FUNCIONARIO); empresas; descripciones.
- **Flujos y reglas**: buscar existente -> cargar -> editar -> guardar; si no existe, se crea (confirmado en código: `GU`, pregunta "Está seguro de crear un nuevo registro?" cuando no hay persona cargada y "Está seguro de modificar el registro?" si la hay). El bloque médico aplica sólo si "Es medico" = SI (confirmado en código: `GU` exige registro médico sólo cuando `ComboMedico` = 1; `LimpiaF` oculta el contenedor médico). Sólo funcionarios con firma cargada podrían firmar documentos clínicos (inferido, por "Seleccionar firma"; el cliente sólo la sube con `showFile` -> `CF` y no valida su presencia).
- **Hallazgos del código**:
  - Mensajes: "Diligencie los campos obligatorios resaltados en rojo por favor."; "Ingrese el registro médico para continuar"; "Ingrese un parametro de busqueda." (Enter en el buscador); "La especialidad X ya se encuentra en la lista"; "El convenio X ya se encuentra en la lista"; confirmación "Está seguro de limpiar el formulario?".
  - La validación de especialidad médica obligatoria está comentada en el código (no se exige).
  - Una especialidad nueva entra a la lista con estado activo y cirugía SI por defecto; al marcar PyP se abre la ventana de programas (`validarAplicaPrograma`, `cargarProgramas`).
  - Servidor: `RD(datos, especialidades, convenios)`, `BP(texto,'0')`, `CF`, `CargarProgramasSeleccionados`. Existe un modo académico (`GESTIONACADEMICA`) que añade tipo de funcionario y grupo.
  - La misma pantalla sirve a "Datos personales": `DesabilitaC` oculta el buscador y cambia el título.

## CONFIGURACION GENERAL > FUNCIONARIO > USUARIO Y CONTRASEÑA (/SUROS/Vistas/Privado/Usuario/UsuarioCredenciales.aspx)
- **Propósito**: administrar los usuarios de acceso de los funcionarios.
- **Funcionalidades**: el usuario puede filtrar por estado y nombre de persona, actualizar la lista, crear usuario, eliminar usuario y asignar contraseña a un usuario (ventana "Asignar contraseña a usuario").
- **Datos**: filtro estado {ACTIVO, INACTIVO}, filtro Nombre persona; ventana de credenciales: Usuario, Contraseña, Confirmar contraseña.
- **Listados**: Usuarios (Tipo Docum, Documento, Nombre persona, Nombre usuario, Estado usuario).
- **Flujos y reglas**: un usuario se vincula a un funcionario existente: la grilla lista personas y las filas sin usuario ("SIN USUARIO") tienen deshabilitados asignar contraseña y eliminar (confirmado en código: `prepare`); contraseña con confirmación; la eliminación puede ser lógica (inferido).
- **Hallazgos del código**:
  - El estado ACTIVO/INACTIVO se cambia editando la celda en la grilla y se envía de inmediato a `CE(USSO_ID, estado)` (`edit`); una celda sin usuario no es editable (`Vedit`).
  - Filtro de texto por nombre en el cliente (`Filtro`, ESC limpia).
  - Las reglas de contraseña de esta ventana no están en el JS de la página (se validan en el servidor o en el control).

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN ROL A USUARIO (/SUROS/Vistas/Privado/Usuario/Roles/RolUsuario.aspx)
- **Propósito**: asignar roles a usuarios y conceder permisos sobre módulos indirectos.
- **Funcionalidades**: el usuario puede buscar usuario por nombre; ver los roles asignados y los disponibles; asignar o quitar un rol; abrir "Otros Permisos" (ventana "Gestionar otros permisos", combo {INICIO HISTORIA}); gestionar permisos a módulos indirectos (ventana) con búsqueda por especialidad y permisos Ver (Todos/Propios) e Imprimir (Todos/Propios); actualizar lista de permisos; aceptar/cancelar.
- **Datos**: combo de módulos indirectos {ACTIVACION DE CITA, ACTIVIDADES DE ENFERMERIA, AGENDA MEDICA, CARGAR INVENTARIOS, CATALOGOMEDICAMENTO.ASPX, CONSULTA EXTERNA, HISTORIA CRONICOS, HISTORIA URGENCIA, INICIO, INICIO HISTORIA, PEDIDOS INTERNOS, REPORTE CITAS MEDICAS}; checkboxes VerTodos, VerPropios, ImprimirTodos, ImprimirPropios.
- **Listados**: Usuarios (Documento, Nombre persona, Nombre usuario, Estado usuario); Rol asignado (Rol); Rol disponible (Rol); permisos (Descripción, Permiso; por especialidad: Descripción, Todos, Propios, Todos, Propios).
- **Flujos y reglas**: un usuario puede tener varios roles (inferido por grids asignado/disponible). Permisos "Propios" vs "Todos": restringen a los registros del propio profesional o a todos (inferido). Los permisos por especialidad se dan por módulo indirecto.
- **Hallazgos del código**:
  - Servidor: `GPI(permisos, PERS_ID, módulo indirecto)` y `GuardarOtrosPermisos(permisos, PERS_ID, otro permiso)`: los permisos se guardan por persona (PERS_ID), no por rol.
  - Estado de usuario con tercer valor "NO CREADO" (rojo) cuando la persona no tiene usuario (`change`).
  - Filtro local de usuarios por nombre y de otros permisos por descripción.

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN INFORMES USUARIO (/SUROS/Vistas/Privado/Usuario/AsignacionInformeUsuario.aspx)
- **Propósito**: definir qué informes puede ver cada usuario y registrar nuevos informes.
- **Funcionalidades**: el usuario puede buscar funcionario; ver árbol de informes disponibles; asignar o quitar un informe al usuario; "Agregar Nuevo Reporte" (ventana "Agregar Reporte": grupo, carpeta, nombre del reporte, página) y elegir página de la lista "Paginas disponibles" (nombre, nombre página, URL); guardar/salir.
- **Datos**: Nombre Grupo, Nombre Carpeta, Nombre Reporte, Página; filtros nombre/URL de páginas.
- **Listados**: FUNCIONARIOS (Documento, Nombre persona, Nombre usuario, Estado usuario); INFORMES ASIGNADOS (ID, CODIGO, INDICADOR, DOMINIO, RESOLUCION); páginas disponibles (Nombre, Nombre página, Url página); árbol INFORMES DISPONIBLES.
- **Flujos y reglas**: un reporte = grupo > carpeta > nombre, enlazado a una página del sistema. Las columnas INDICADOR/DOMINIO/RESOLUCION sugieren informes regulatorios (inferido, p. ej. resoluciones de indicadores). Hay una ventana "Request Failure" de error AJAX.
- **Hallazgos del código**: la página no tiene funciones JS propias; toda la lógica (árbol, asignar, agregar reporte) corre en el servidor.

## CONFIGURACION GENERAL > CONFIGURACION ENTIDAD HOSPITALARIA (/SUROS/Vistas/Privado/General/InformacionEntidad.aspx)
- **Propósito**: datos de la institución y parámetros globales.
- **Funcionalidades**: el usuario puede editar datos generales de la entidad, editar el valor de cada parámetro (combo ComboValor) y guardar.
- **Datos**: nombre, NIT, correo, dirección, teléfono, ciudad, nivel (numérico).
- **Listados**: Configuración general (Item, Nombre, Descripción, Valor).
- **Flujos y reglas**: el valor de cada parámetro se elige de un combo según el ítem (confirmado en código: `RenderValor` busca el valor en `StoreValor` y, si no está, lo toma de la lista `ESTADOS` (JSON) que trae cada fila); confirmación de guardado (messagebox "Notificación").
- **Hallazgos del código**:
  - Mensaje: "El formulario esta incorrecto." si el formulario no es válido.
  - Servidor: `GD({DATA: {NOMBRE, NIT, CORREO, DIRECCION, TELEFONO, CIUDAD, NIVEL}, KEYS, CONFIGURACION: filas de la grilla})`; datos de la entidad y parámetros se guardan en una sola llamada.

## CONFIGURACION GENERAL > GESTIONAR ESPECIALIDAD (/SUROSHistoriaClinica/Vistas/Privado/Medico/Especialidad.aspx)
- **Propósito**: catálogo de especialidades médicas y tipos de especialidad, con su comportamiento en agenda e historia.
- **Funcionalidades**: el usuario puede crear, editar y eliminar tipos de especialidad (Nuevo/Editar/Eliminar); crear/editar especialidades (Aceptar/Cancelar); asociar módulos (recurso) principal y secundario que se usan al atender desde la agenda médica; "Transferir a" (mover especialidades a otro tipo, inferido).
- **Datos**: Nombre; "Multiple cita" {SI, NO}; Recurso 1, Recurso 2; checks: Otras Evoluciones, Permite Remontar Agenda, Fórmula Médica Otras Evoluciones, Mostrar Panel Escala detección riesgo suicida en otras evoluciones; tipo de especialidad (TIES_NOMBRE, TIES_MULTIPLECITA {SI, NO}); campo fecha.
- **Listados**: Tipo especialidad (Descripción, Multiple cita); Especialidad (Módulo/Recurso principal, secundario, Otras Evoluciones); Modulo(Recurso) (Nombre).
- **Flujos y reglas**: el recurso define qué módulo abre el médico al atender desde la agenda. "Multiple cita" permite más de una cita por paciente en esa especialidad (inferido). "Remontar agenda" habilita reabrir/ampliar agenda (inferido).
- **Hallazgos del código**: al marcar "Otras Evoluciones" se habilitan "Fórmula Médica Otras Evoluciones" y el panel de escala de riesgo suicida; al desmarcarlas se deshabilitan y se ponen en falso (`CambiarEstado`). Los recursos sin definir se pintan "SIN DEFINIR" en rojo y "NO APLICA" en otras evoluciones en rojo (`RenderRecurso`, `RenderOtras`).

## CONFIGURACION GENERAL > PAGINAS DEL SISTEMA (/SUROS/Vistas/Privado/General/Paginas.aspx)
- **Propósito**: registro de las páginas (URLs) disponibles para armar módulos y roles.
- **Funcionalidades**: el usuario puede ver el árbol de recursos disponibles, actualizar el árbol, crear una nueva página (ventana "Adicionar pagina al sistema"), eliminarla y actualizar la lista.
- **Datos**: Nombre página, Url, Estado {ACTIVO, INACTIVO}; filtros por ID, nombre, URL, página.
- **Listados**: Paginas disponibles (ID, Nombre, Url página, Nombre página, Estado); árbol de recursos.
- **Flujos y reglas**: el árbol de recursos (cargado por demanda con `NodeLoad`) refleja los archivos del servidor y las páginas se registran eligiendo un nodo hoja: se precarga nombre = texto del nodo, URL = id del nodo y estado ACTIVO, y la ventana se titula "Crear una nueva pagina" (confirmado en código: `createNewPageFromResource`). Estas páginas alimentan Roles y Módulos e Informes.
- **Hallazgos del código**:
  - Mensaje: "Seleccione un recurso para crear una página." (título "Aviso") si el nodo no es hoja.
  - Servidor: `RP({NOMBRE, URL, NOMBREP, ID, ESTADO})` (ID -1 = nueva), `NodeLoad(id)`; tras guardar se recarga la carpeta del nodo (`ActLista`).
  - Filtros en el cliente por ID, nombre, URL y nombre de página.

## CONFIGURACION GENERAL > ROLES Y MODULOS (/SUROS/Vistas/Privado/Usuario/Roles/RolModulos.aspx)
- **Propósito**: definir roles y la estructura de menú (grupos y módulos) con permisos.
- **Funcionalidades**: el usuario puede crear/editar/eliminar roles; ver usuarios asociados al rol; gestionar módulos indirectos; armar el árbol de módulos: adicionar grupo, adicionar módulo, insertar en un grupo, editar nombre, editar módulo, eliminar módulo, subir/bajar orden, copiar módulos a otro rol (ventana); elegir ícono (ventana "Iconos disponibles"); elegir página; habilitar permisos del módulo y guardarlos.
- **Datos**:
  - Rol (ventana "Nuevo rol"): estado {ACTIVO, INACTIVO}, tipo rol, nombre rol, observación, check "Programa Agenda".
  - Módulo (ventana "Adicionar Modulo"): nombre módulo, orden (numérico), página, ícono, especialidad.
  - Tipo de módulo {INICIO, HISTORIA CLINICA, PAGINA WEB, ALMACEN}.
- **Listados**: Roles del sistema (Usuario, Programa Agenda, Estado); usuarios asociados (Tipo doc, Número documento, Nombre usuario; Usuario, Programa Agenda); árbol de configuración de módulos; Asignar permisos al módulo (Descripción, Permiso); permisos de módulos indirectos (Descripción, Permiso); páginas disponibles (Nombre, Nombre página, URL).
- **Flujos y reglas**: rol -> árbol de grupos/módulos (orden) -> cada módulo apunta a una página; los permisos por módulo se asignan por descripción de permiso: grilla de permisos con casilla SI/NO por fila que se envía completa al guardar (confirmado en código: `renderpermiso`, `GP`). "Programa Agenda" marca el rol como programable en la agenda (inferido). Los módulos pueden asociarse a una especialidad.
- **Hallazgos del código**:
  - Confirmaciones: "Realmente desea crear un nuevo módulo?"; "Realmente desea modificar la información del modulo?"; "Esta seguro de copiar los modulos a los roles seleccionados?".
  - Mensajes: "Seleccione minimo un rol para continuar."; "lo sentimos, no fue posible modificar la información del modulo, intentelo mas tarde." (si el servidor no responde SI).
  - Los nombres de módulo se guardan en MAYÚSCULAS (`AddModulo`, `EditModulo`). Los botones editar/eliminar/ver usuarios/módulos indirectos se habilitan sólo con un rol seleccionado (`EnabledBoton`).
  - El árbol de módulos se carga por tipo de módulo y rol (`NodeLoad(nodo, ROL_ID, tipo)`). El ID del nodo codifica `tipo|MODUID|PAGIID` y el nodo guarda `ESPEID`, `PAGIID`, `ORDEN`.
  - Servidor: `RR` (rol: ID -1 = nuevo, TIPO, NOMBRE, DESC, ESTADO, PROGRAMAAGENDA), `NodoEdita`, `CMR` (copiar a roles), `CP` (permisos del módulo), `GP`, `GPI` (permisos indirectos por rol y módulo indirecto).

## CONFIGURACION GENERAL > USUARIOS ACTIVOS EN SUROS (/SUROS/Vistas/Privado/SignalR/UsuariosActivos.aspx)
- **Propósito**: monitorear sesiones conectadas y comunicarse con ellas (SignalR).
- **Funcionalidades**: el usuario puede ver usuarios conectados, enviar mensaje a uno, cerrar la sesión de un usuario, iniciar chat, preparar y enviar mensaje masivo (ventana "Envio Masivo").
- **Datos**: Mensaje (texto).
- **Listados**: Id usuario, Nombre usuario, Conectado desde, Ip, Rol, Especialidad, Fecha y hora conexión, Id Signal.
- **Flujos y reglas**: comunicación en tiempo real por conexión SignalR (Id Signal). Cerrar sesión fuerza logout remoto (inferido); la ventana "Sesión finalizada" global lo respaldaría.
- **Hallazgos del código**:
  - La página no habla con SignalR directamente: delega en la ventana madre (`parent.AccionSGR({TIPO, ...})`). Tipos usados: 1 = cerrar sesión y también iniciar chat (ambas funciones envían el mismo tipo; el JS no distingue la acción), 3 = actualizar lista, 22 = mensaje masivo. Las funciones de conexión propias están comentadas.
  - Sólo actúa si hay una fila seleccionada.

## CONFIGURACION GENERAL > CONFIGURACIÓN LABORATORIO (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/Laboratorios/LaboratorioClinico.aspx)
- **Propósito**: catálogo de estudios de laboratorio, analitos y unidades de medida.
- **Funcionalidades**: el usuario puede crear/modificar estudios (ventana "Agregar estudio de laboratorio"); buscar el procedimiento por código CUPS o descripción (coincidencias); agregar, ordenar (subir/bajar) y quitar analitos del estudio; gestionar el catálogo de analitos (ventana "Gestionar análitos": crear, eliminar); gestionar unidades de medida (ventana "Unidad medida": registrar, guardar, eliminar, filtro estado {TODOS, ACTIVO, INACTIVO}); registrar opciones de respuesta (ventana, lista de texto).
- **Datos**:
  - Estudio: código CUPS, descripción, estado {ACTIVO, INACTIVO}; sección {BANCO DE SANGRE, CITOPATOLOGIA, COAGULACION, COPROANALISIS, HEMATOLOGIA, INMUNOLOGIA, ESPECIAL, INMUNOLOGIA I-V, LIQUIDOS, MICROBIOLOGIA, QUIMICA, HORMONAS, MICROSCOPIA}; técnica {AGLUTINACION, COAGULOMETRICO, COLORIMETRICO, COLORIMETRICO DE PUNTO FINAL, COLORIMETRICO ENZIMATICO, ELECTRODO DE ION SELECTIVO, ELISA, ENZIMATICO, INMUNOENSAYO DE CROMATOGRAFIA DE FLUJO, INMUNOENSAYO ENZIMATICO EIA, INMUNOFLUORESCENCIA, INMUNOTURBIDIMETRIA, LECTURA MICROSCOPICA, MICROELISA, NO DEFINIDA, QUIMICA SECA, QUIMIOLUMINISCENCIA, TURBIDIMETRIA}; tipo muestra {NO DEFINIDA, ESPUTO, MATERIA FECAL, ORINA, ORINA 24 HORAS + SUERO, SECRECIONES VARIAS, PLASMA, SUERO, SANGRE TOTAL}; nivel {I a V NIVEL}; días almacenamiento; tipo almacenamiento {NO APLICA, CONGELACION, TEMPERATURA AMBIENTE, REFRIGERADA}; sexo {AMBOS, HOMBRE, MUJER}; prefijo código de barras; confidencial {SI, NO}; valor mín/máx; alerta mín/máx.
  - Analito: código, descripción, abreviatura, unidad de medida, fórmula, valor mín/máx, alarma mín/máx, valor de referencia (texto).
  - Unidad de medida: descripción (y estado).
- **Listados**: estudios (Procedimiento, Abreviatura, Unid/Med, Sección, Técnica, Tipo muestra, Nivel complejidad, Días almacenamiento, Almacenamiento, Sexo, Pref. código barra, Valor min/max, Alarma min/max, Estado); analitos del estudio (LEXAID, LAANID, Pos, Descripción, Abreviatura, Unid/Med, Valor min/max, Alarma max/min); catálogo de analitos (Id, Descripción, Abreviatura, Unid/Med, Valor min/max, Alarma max/min, Estado); unidades (Id, Descripción, Estado); códigos y descripciones.
- **Flujos y reglas**: estudio (procedimiento CUPS) 1..N analitos ordenados; rangos y alarmas por analito, y por estudio; analito con fórmula = calculado (inferido); "Registrar opciones de respuesta" para analitos cualitativos (inferido). Los valores de alarma sirven para marcar resultados críticos (inferido).

## CONFIGURACION GENERAL > CREDENCIALES SISPRO (/SUROS/Vistas/Privado/WebSispro/CredencialesWebSispro.aspx)
- **Propósito**: gestionar las credenciales de acceso al servicio web SISPRO/MinSalud (confirmado en código: `guardar` llama `CredencialesWebSispro.aspx/GuardarCredenciales`). Página HTML estándar (no Ext), extraída por DOM.
- **Funcionalidades**: el usuario puede agregar una credencial (GUARDAR), modificar una existente (Editar en la fila, luego Modificar), limpiar el formulario, buscar en la grilla y exportar (Copy, CSV, Excel, PDF, Print).
- **Datos**: Tipo de documento {AS, CC, CE, MS, NT, PA, RC, TI, TE, NV, PEP, PPT, PT}; Número; Clave; NIT; Estado activo; Tipo de usuario (combo sin valores extraídos).
- **Listados**: ID | Tipo documento | Número | Clave | NIT | Tipo usuario | Estado | Acciones. La columna Clave aparece en la grilla (se desconoce si se muestra enmascarada).
- **Flujos y reglas inferidas**: cada fila es el acceso de un usuario SISPRO (tipo y número de documento, clave, tipo de usuario) asociado a un NIT y a un estado (confirmado en código: `guardar`); la edición carga la fila en el formulario y cambia GUARDAR por Modificar (confirmado en código: `EditarCredenciales`, `GuardarEdicionCredenciales`).
- **Hallazgos del código**:
  - Métodos de página (AJAX JSON): `GuardarCredenciales`, `ModificarCredenciales`, `CargarInformacionCredenciales`. Datos enviados: TipoDocumento, Numero, Clave, Nit, Estado (1/0), TipoUsuario (+ IdCredenciales al modificar).
  - No hay validación de cliente de campos obligatorios ni de formato (sólo `trim`); no hay mensaje de éxito ni de error visible (los fallos van a la consola).
  - Seguridad: al editar, el servidor devuelve la clave al navegador y la carga en el campo `txtClave` (`EditarCredenciales`); no hay evidencia de enmascarado ni de cifrado en cliente. Qué hace el servidor con ella es lógica del servidor.
  - Los valores de "Tipo de usuario" no están en el JS (se llenan desde el servidor).

## CONFIGURACION GENERAL > EMPRESAS (/SUROS/Vistas/Privado/Empresa/Empresa.aspx)
- **Sin extracción útil de UI**: la re-extracción devolvió el título vacío y ningún campo, botón ni grilla; el código JS sí describe la pantalla (página HTML con jQuery, no Ext).
- **Propósito**: catálogo de empresas/aseguradoras (EPS, particular) usadas en pacientes, convenios y facturación (confirmado en código: `guardar` pide "si es Eps o Empresa", régimen y código de habilitación; el uso en facturación sigue inferido; en Pacientes el filtro de EPS lista "ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I").
- **Funcionalidades**: crear, editar y listar empresas (confirmado en código: `guardar`, `EditarEmpresa`, `GuardarEdicionEmpresa`, `recargar`).
- **Datos** (del código): nombre, dirección, email, teléfono, contacto, código de entidad, NIT, régimen, "aplica SOAT" (check), Eps/Empresa, código de habilitación, estado, país -> departamento -> municipio (listas dependientes).
- **Hallazgos del código**:
  - Mensajes (alerta tipo advertencia, SweetAlert): "Es necesario seleccionar un departamento" (valida el campo municipio); "Es necesario seleccionar el estado de la empresa"; "Es necesario seleccionar la opción de si es Eps o Empresa". Los demás campos no se validan en el cliente.
  - Métodos de página (AJAX JSON): `Empresa.aspx/GetCurrentTime` (nombre engañoso: es el alta), `ModificarEmpresa`, `CargarInformacionCita` (carga una empresa por Id; nombre heredado de otra pantalla), `CargarDepartamento`, `CargarMunicipio`. Servidor Ext: `CargarMunicipio(pais)`, `BindData()`. La lista es un repetidor (`rptEmpresas`).
  - Al editar se alterna el panel Guardar/Modificar; al guardar la página se recarga.
  - Código de habilitación vacío en la edición se envía como "null" (cadena).

## CONFIGURACION GENERAL > SUBPLANES SERVICIOS (/SUROSFacturacion/Vistas/Privado/SubPlanes/SubPlanesServicios.aspx)
- **Propósito**: relacionar servicios con subplanes (facturación).
- **Funcionalidades**: el usuario puede buscar un servicio, listar los subplanes asignados, agregar un subplan al servicio (ventana de subplanes disponibles) y eliminar un subplan del servicio.
- **Datos**: Servicio (trigger de búsqueda), SUSE_ID, SUPL_NOMBRE.
- **Listados**: Servicios (Servicio); SubPlanes asignados (Id Único, SubPlan); SubPlanes disponibles (SubPlan).
- **Flujos y reglas**: relación N:M servicio-subplan (tabla SUSE inferida del nombre del campo). Un subplan define qué servicios cubre (inferido).
- **Hallazgos del código**: el JS de la página es una copia de `RolUsuario.aspx` (funciones `GPI`, `GuardarOtrosPermisos` con PERS_ID y filtro sobre `SERV_NOMBRE`); no contiene la lógica de agregar/quitar subplanes, que corre en el servidor.

## HERRAMIENTAS > UNIFICACION HISTORIA CLINICA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/UnificarHistoriaClinica.aspx)
- **Propósito**: fusionar historias clínicas de pacientes duplicados.
- **Funcionalidades**: el usuario puede buscar dos pacientes (Paciente 1 y 2, con ventana de coincidencias por documento/nombre), ver sus atenciones, transferir información de uno a otro ("Transferir información"), eliminar un paciente, acceder a opciones del paciente.
- **Datos**: documento/nombre de cada paciente; ventana "Transferir información" (células/nombre).
- **Listados**: Paciente 1 y Paciente 2 (ID, Fecha entrada, Fecha salida, Profesional que registra, Estado); coincidencias (Documento, Nombre paciente; Descripción).
- **Flujos y reglas**: origen -> destino: se seleccionan ingresos (atenciones) de un paciente y se mueven al otro; el duplicado no se elimina automáticamente: sólo puede eliminarse a mano cuando ya no tiene ingresos (corregido según código: `TR`, `EliminaPaciente`). Operación destructiva: requiere confirmación (confirmado en código: `TR`); el permiso requerido sigue inferido.
- **Hallazgos del código**:
  - Confirmaciones: "Está seguro de continuar con el proceso?"; "Esta seguro de eliminar el registro del paciente X?".
  - Mensajes: "Seleccione Minimo un ingreso del paciente 1 para continuar." (y 2); "No puede continuar, el paciente X tiene registros de ingreso"; "Seleccione minimo un registro para continuar."; "Es nesesario que seleccione un paciente de destino".
  - Servidor: `TI({PACIID1, PACIID2, nombres, INGRID: ids separados por coma, PACIID destino})` (transfiere ingresos), `EP(...)` (elimina paciente) y `TIP({PACIIDDESTINO, PACIIDORIGEN}, ids)` ("Transferir información" por registros de la grilla de transferencia).
  - El estado del ingreso se pinta: 1 = EN ATENCIÓN, otro = ATENDIDO (`Cambio`).

## HERRAMIENTAS > DISEÑADOR DE CONSENTIMIENTOS (/SUROS/Vistas/Privado/Formatos/Formatos.aspx)
- **Propósito**: diseñar formatos de consentimiento informado versionados, con comodines que se llenan al imprimir.
- **Funcionalidades**: el usuario puede crear/editar/eliminar tipos de formato (filtro por nombre, paginado); crear nueva versión, copiar versión, eliminar versión; editar cabecera, contenido principal y pie con editor HTML (modo código, alineación, estilos, listas, enlaces, imágenes y documentos subidos, bloques Destacado/Nota/Alerta); insertar comodines; previsualizar en PDF; imprimir formatos; asociar procedimientos médicos (búsqueda); abrir ayuda de comodines y edición de versiones.
- **Datos**:
  - Tipo de formato: Nombre, Descripción.
  - Versión: Título, Código, Versión, Tipo de consentimiento {CONSENTIMIENTOS INFORMADOS}, Cabecera, Contenido principal, Pie de página (combos para reutilizar cabecera/pie).
  - Comodines disponibles: nombre del formato, código y versión del formato, logo de la empresa, tabla de diseño, nombre/documento/tipo documento de la persona, firma y huella de la persona, médico en sesión (nombre, firma, especialidad), representante legal o familiar (nombre, identificación y parentesco), fecha actual, nombre de la empresa y del gerente, contenido, procedimiento a realizar y realizado (código y nombre).
  - También hay campos de tipo noticia en la misma página (NOTI_ID, categoría, fecha publicación, palabras clave, estado, periodista, URL, orden, imagen principal, resumen); reutilizan el editor de noticias del CMS: las acciones de fila usan `NOTI_ID`, "Aprobar" y la imagen se sirve desde la carpeta de imágenes del módulo Página Web (confirmado en código: `ejecutarAccionesEnLinea`, `preparandoFormatos`); es código heredado fuera del alcance del diseñador.
- **Listados**: Tipos de Formatos (Título); Versiones de Formatos (Título, Código, Versión); procedimientos (Código, Descripción).
- **Flujos y reglas**: tipo -> N versiones; sólo una versión vigente por código (inferido); un formato se liga a procedimientos (par versión `FOVE_ID` + procedimiento `PRQU_ID`; confirmado en código: `SelecCIE10`, `GuardarProcedimiento`); que se imprima al realizar el procedimiento sigue inferido.
- **Hallazgos del código**:
  - Editor: HTML editor de Ext con botones propios para cabecera, contenido y pie. Los comodines se insertan como marcadores numéricos entre corchetes: [1] nombre de la persona, [3] documento, [19] tipo de documento, [4] firma de la persona, [5] huella, [6] médico en sesión, [7] firma del médico, [8] especialidad del médico, [9] representante legal o familiar, [10] identificación y parentesco, [11] fecha actual, [15] empresa, [16] gerente, [17] procedimiento a realizar, [18] procedimiento realizado; para cabecera/pie: [12] nombre del formato, [13] código, [14] versión, y logo de empresa; "[___]" marca el contenido.
  - El logo se inserta como imagen con URL de un dominio externo (host del cliente; no se documenta).
  - Bloques de resumen: Destacado (`resumen-destacado`), Nota (`resumen-nota`), Alerta (`resumen-alerta`).
  - Confirmaciones: "Esta seguro de eliminar este Formato?"; "Esta seguro de eliminar esta Formatos?"; "Esta seguro de aprobar esta Formatos?"; "Esta seguro de eliminar este procedimiento?" (usan un diálogo de alerta con OK, no Sí/No).
  - Mensajes: "El procedimiento X ya está en la lista."; "Es necesario que escriba un parámetro de búsqueda.".
  - Editar una versión deshabilita la grilla de versiones y habilita "Generar PDF"; el PDF se abre en ventana nueva desde la carpeta temporal del CMS (`GotPDF`). Los documentos adjuntos se insertan como enlaces (clase `linkPdf` o `linkXls`).
  - No usa Ace ni JSONEditor: es el editor HTML nativo de Ext; el editor JSON se usa en Configuración General.
  - Servidor: `Eliminar`, `AprobarAID`, `prepararEdicion`, `CargarProcedimientosQX`, `GuardarProcedimiento`, `CONS`, `EliminarFormatoProcedimiento`, `formatos.EliminarFormato`.

## MI CUENTA > CAMBIAR CONTRASEÑA (/SUROS/Vistas/Privado/Funcionario/CambiarContrasena.aspx)
- **Propósito**: el usuario cambia su propia clave.
- **Funcionalidades**: el usuario puede ingresar contraseña actual, nueva y confirmación, y aceptar.
- **Datos**: contraseña actual, nueva contraseña, repetir contraseña.
- **Flujos y reglas**: valida que las dos nuevas coincidan (confirmado en código: `IN`) y envía la actual al servidor, que la valida (inferido).
- **Hallazgos del código**:
  - Mensajes (en `IN`): "Ingrese contraseña."; "Ingrese verificacion contraseña."; "La contraseña no coincide."; "La contraseña nueva debe tener minimo 8 carateres." (sic).
  - Regla de longitud mínima 8 en cliente; no se exigen mayúsculas, números ni símbolos.
  - Servidor: `MC(nueva, actual)`.
  - Incoherencia: el cambio obligatorio de clave del shell (`CP`) exige "La contraseña debe tener minimo 6 caracteres." y no pide la actual; el mínimo cambia según la ruta.

## MI CUENTA > DATOS PERSONALES (/SUROS/Vistas/Privado/Funcionario/FormularioFuncionarioPersonal.aspx)
- **Sin extracción útil**: la re-extracción sólo devolvió el título "Datos personales funcionario", sin campos ni botones.
- **Propósito**: el funcionario ve/edita sus propios datos: es un contenedor que reutiliza el formulario de funcionario en modo personal (confirmado en código: `Desabilita` llama `parent.DesabilitaC`, que oculta el buscador y titula "Datos personales").
- **Funcionalidades**: ver/editar datos propios con el formulario de funcionario sin búsqueda ni limpiar (confirmado en código: `DesabilitaC` de `FormularioFuncionario`).

## PACIENTE > CONSULTAR CITAS DEL PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/ReporteCitasPaciente.aspx)
- **Propósito**: consultar el historial de citas de un paciente.
- **Funcionalidades**: el usuario puede buscar paciente por documento o nombre (ventana de coincidencias), consultar sus citas y agrupar/ordenar la grilla.
- **Datos**: Documento/Nombre; documento y nombre del paciente (sólo lectura).
- **Listados**: Citas médicas del paciente (Mes, Fecha, Turno, Hora, Médico, Registrado por, Nota, Tipo asignación, Estado); coincidencias (Documento, Nombre paciente).
- **Flujos y reglas**: sólo lectura (confirmado en código: `AsignaN` es la única función y sólo copia documento y nombre de la coincidencia; no hay llamadas de guardado).

## PACIENTE > DATOS PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/FormularioPaciente.aspx)
- **Propósito**: crear y editar la ficha demográfica, administrativa y biométrica del paciente.
- **Funcionalidades**: el usuario puede buscar paciente (documento/nombre), guardar, guardar y cerrar, limpiar formulario; cargar foto de perfil (ventana "Actualizando Foto de Inicio"); cargar documento frente y reverso (Cara A/B); registrar datos biométricos (panel; huella inferida por comodín de consentimientos); buscar municipio (nacimiento, residencia, expedición); asignar o borrar acompañante/responsable (ventana "Datos del Responsable"); buscar grupo poblacional (ventana con grilla); cargar archivo XLS (carga masiva de pacientes; confirmado en código: `cargarXLS` -> `CargarXLS("PACIENTES")`).
- **Datos**:
  - Paneles: Foto de perfil, Cara A del documento, Cara B del documento, Datos del paciente, Datos Biométricos.
  - Identificación: tipo documento (mismo catálogo de 13 valores que en funcionario), documento, expedida en, fecha de nacimiento, edad (calculada, inferido), primer/segundo nombre, primer/segundo apellido.
  - Género {MUJER, INDETERMINADO O INTERSEXUAL, HOMBRE}; identidad de género {NEUTRO, MASCULINO, FEMENINO, TRANSGENERO, NO LO DECLARA}; ocupación; cargo; email.
  - Afiliación: tipo afiliado {COTIZANTE, SUBSIDIADO, CONTRIBUTIVO ADICIONAL, NO AFILIADO, ESPECIAL O EXCEPCIÓN COTIZANTE, ESPECIAL O EXCEPCIÓN BENEFICIARIO, PERSONAS PRIVADAS DE LA LIBERTAD A CARGO DEL FONDO NACIONAL DE SALUD, TOMADOR/AMPARADO ARL, TOMADOR/AMPARADO SOAT, TOMADOR/AMPARADO PLANES VOLUNTARIOS DE SALUD, PARTICULAR, ESPECIAL O EXCEPCION NO COTIZANTE LEY 352 DE 1997}; nombre del cotizante; empresa (EPS); exonerado de copago (check) y tipo de exoneración; tipo de paciente.
  - Demografía: etnia, estado civil, discapacidad, nivel educativo (mismos catálogos que funcionario), ubicación residencial {RURAL, URBANA}, grupo poblacional.
  - Contacto: municipio de nacimiento y de residencia, dirección, celular, teléfono, acudiente.
  - Estado: estado del paciente (combo), continúa atención {Si, No}.
  - Ventana Responsable: documento, nombre, teléfono, parentesco, EPS afiliado, otra EPS.
- **Listados**: coincidencias (Documento, Nombre paciente); grupos poblacionales (Pertenece, Código, Nombre).
- **Flujos y reglas**: buscar -> cargar -> editar -> guardar; el tipo de afiliado sólo es obligatorio si el parámetro `CONF.TIPOAF` = 1 y, cuando el tipo de afiliado tiene id 2, se exige el nombre del cotizante (corregido según código: `GU`; la descripción del id 2 no está en el JS); exoneración de copago habilita el tipo (inferido); el acompañante/responsable es obligatorio para todo paciente, no sólo menores (corregido según código: `GU`).
- **Hallazgos del código**:
  - Mensajes: "Diligencie los campos obligatorios resaltados en rojo por favor."; "Es necesario diligenciar el Responsable."; "Es necesario el grupo poblacional."; "Seleccione el tipo de afiliacion"; "Registre el cotizante para continuar"; "Seleccione un municipio para continuar."; "Ingrese un parametro de busqueda.".
  - Confirmación según el caso: "Esta seguro de registrar a la persona como paciente?" (persona existente sin ficha de paciente), "Está seguro de modificar el registro?" o "Está seguro de crear un nuevo registro?". Así existe la entidad Persona separada de Paciente (`PERSID` y `PACIID`).
  - Responsable (ventana): documento > 5 caracteres, nombre completo > 7, teléfono > 6, parentesco > 2; mensajes "Ingrese un numero de documento valido.", "Ingrese un nombre completo valido.", "Ingrese un numero de telefono valido.", "Ingrese un tipo de parentesco valido.". Se guarda como un solo texto `documento-nombre-teléfono-parentesco-EPS` (u "OTRA" con texto libre), de modo que los guiones en los datos romperían la lectura.
  - Grupos poblacionales: casillas por grupo; se envían listas de agregados y eliminados y el campo muestra los nombres unidos por " - ".
  - Género: se deriva el código F/M/I del texto MUJER/HOMBRE/otro. El municipio de residencia se copia del de nacimiento si está marcada la casilla correspondiente (`SelecUbicacion`).
  - Auditoría: antes de guardar se registra la acción "REGISTRAR PACIENTE" con los datos en el shell (`parent.parent.GAJ`).
  - El tipo de exoneración se envía en el campo `TIPODISCAPACIDAD` (nombre heredado, fuera de lugar).
  - Servidor: `RD(datos)`, `BP(texto,'0')`, `VP(documento)`, `CFF`, `CargarXLS`, `CargarImagen`. Hay filtros de entrada que solo admiten números o letras (`validateNumbers`, `validateLetters`).
  - El documento anterior se envía como `DOCUMENTOANT` (se permite cambiar el número de documento).

## PACIENTE > PACIENTES (/SUROSHistoriaClinica/Vistas/Privado/Paciente/Paciente.aspx)
- **Propósito**: listado maestro y buscador de pacientes.
- **Funcionalidades**: el usuario puede filtrar por ID, documento, nombre, género, fecha de nacimiento, celular, email y empresa; ver total de pacientes; refrescar; exportar; abrir un paciente en "Consultar y gestionar" (lleva al formulario de paciente, pestaña "EDICION DE PACIENTE" con el documento como parámetro; confirmado en código: `ejecutarAccionesEnLinea`).
- **Datos**: filtros; empresa {ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I} (lista dependiente de los datos del entorno).
- **Listados**: ID, Foto, Documento, Nombre, Sexo, Nacimiento, Celular, Email, EPS (paginado). Existe un botón "Esta lista contiene mis pedidos de insumos" que parece residual de otra pantalla (inferido).
- **Hallazgos del código**: la acción Editar queda deshabilitada si el paciente está aprobado (`PERS_APROBADO`, `prepararAccionesEnLinea`); la foto se sirve desde la carpeta de fotos de persona del CMS; todos los filtros se aplican en el navegador sobre la lista ya cargada.

---

## Modelo de seguridad
- **Funcionario**: persona con ficha laboral (identificación, cargo, ocupación, empresa, estado, firma, especialidades, convenios, programas PyP). Si es médico, además registro profesional y especialidades.
- **Usuario**: credenciales (usuario/clave, estado ACTIVO/INACTIVO) ligadas a un funcionario; crear, eliminar, asignar clave; cada persona puede cambiar su clave (Mi cuenta).
- **Rol**: nombre, tipo, observación, estado, indicador "Programa Agenda". Un usuario tiene N roles.
- **Módulos**: cada rol tiene un árbol ordenado de grupos y módulos; el módulo apunta a una página del sistema, tiene ícono, tipo {INICIO, HISTORIA CLINICA, PAGINA WEB, ALMACEN} y puede ligarse a una especialidad. Se pueden copiar módulos entre roles.
- **Páginas**: catálogo de URLs (nombre, URL, estado) del que se arman módulos e informes.
- **Permisos**: (1) por módulo, lista de permisos de descripción habilitables; (2) módulos indirectos (accesos sin menú, p. ej. AGENDA MEDICA, HISTORIA URGENCIA) con permisos Ver/Imprimir x Todos/Propios, por especialidad; (3) "otros permisos" (INICIO HISTORIA); (4) informes asignados por usuario.
- **Sesiones**: monitor de conectados (IP, rol, especialidad, hora), cierre remoto, mensajería y chat (SignalR). Contraseñas: mínimo 8 caracteres al cambiarla desde Mi cuenta y 6 en el cambio obligatorio del shell; sin reglas de complejidad en el cliente.
- **Sedes**: no aparecen en estas pantallas; la sede se elige en el shell (`ComboSede`) y las pantallas operativas la envían como parámetro `SEDE` al servidor (p. ej. agendas e informes). Si el usuario está restringido a ciertas sedes lo decide el servidor.

## Entidades y estados
- Funcionario (estado ACTIVO/INACTIVO), Usuario (ACTIVO/INACTIVO), Rol (ACTIVO/INACTIVO), Página (ACTIVO/INACTIVO), Módulo, Permiso, Informe.
- Especialidad, Tipo de especialidad, Recurso/módulo de atención.
- Entidad hospitalaria, Configuración/parámetro, Empresa, Convenio, SubPlan, Servicio.
- Estudio de laboratorio, Analito, Unidad de medida, Opción de respuesta (estado ACTIVO/INACTIVO).
- Formato de consentimiento, Versión de formato, Comodín.
- Paciente (estado de paciente y "continúa atención" Sí/No), Responsable/acompañante, Grupo poblacional, Cita (estado, tipo de asignación), Atención (ID, entrada, salida, profesional, estado).

## Preguntas abiertas

### Respondidas
1. **Sedes: ¿el usuario/rol se restringe por sede o la sede se elige al ingresar?** La sede se elige en el shell mediante un combo (`ComboSede`) y las pantallas la envían como parámetro `SEDE` (código: `Consulta` de Reporte Citas Médicas, `ActualizaLista` de las agendas). Ninguna pantalla de seguridad asigna sedes a usuario o rol.
2. **Qué servicios SISPRO consume Credenciales SISPRO.** Es un CRUD de credenciales por NIT (tipo y número de documento, clave, tipo de usuario, estado) con métodos de página `GuardarCredenciales`, `ModificarCredenciales` y `CargarInformacionCredenciales` (código: `guardar`, `EditarCredenciales`). El servicio consumido se confirma por el nombre del módulo (WebSispro); la clave sí viaja al navegador al editar (código: `EditarCredenciales`).
3. **Empresas y Datos personales sin campos.** Empresas: nombre, dirección, email, teléfono, contacto, código de entidad, NIT, régimen, aplica SOAT, Eps/Empresa, código de habilitación, estado, país/departamento/municipio (código: `guardar`). Datos personales: reutiliza el formulario de funcionario sin buscador (código: `DesabilitaC`).
4. **Qué contiene Configuración General.** Cada fila es un registro con descripción editable en un editor JSON (código: `GD`); los ítems concretos vienen del servidor.
5. **Semántica de "Propios/Todos".** El cliente sólo guarda las casillas VerTodos/VerPropios/ImprimirTodos/ImprimirPropios por persona y módulo indirecto (código: `GPI`); su efecto lo aplica cada pantalla clínica al listar registros (supuesto estándar del sector: "Propios" = registros del propio profesional).
6. **Alcance de la unificación de historias.** Mueve ingresos (atenciones) seleccionados de un paciente a otro, no elimina al duplicado automáticamente y éste sólo se borra si queda sin ingresos (código: `TR`, `EliminaPaciente`). Tablas afectadas y reversibilidad son del servidor (ver sin respuesta).
7. **Relación de Formatos con el módulo de noticias.** Comparte código con el editor de noticias del CMS (`NOTI_ID`, aprobar, imágenes del CMS) (código: `ejecutarAccionesEnLinea`, `preparandoFormatos`).
8. **Cómo se cargan las páginas desde el árbol de recursos.** Alta manual: se elige un nodo hoja del árbol de recursos del servidor y se confirma nombre y estado (código: `createNewPageFromResource`, `RP`).
9. **Carga de XLS en Datos Paciente.** Es una carga masiva de pacientes (código: `cargarXLS` -> `CargarXLS("PACIENTES")`); el formato de columnas lo define el servidor.
10. **Reglas de contraseña.** Mínimo 8 caracteres en Mi cuenta (código: `IN`) y 6 en el cambio obligatorio del shell (código: `CP`); sin complejidad en cliente. Se recomienda unificar y reforzar la regla (supuesto estándar del sector).
11. **Tratamiento de datos personales de pacientes.** El formulario de paciente captura datos personales y sensibles (discapacidad, etnia, huella, documento escaneado); su manejo cae bajo la Ley 1581 de 2012 y la historia clínica bajo la Res. 1995 de 1999 (norma: Ley 1581/2012, Res. 1995/1999); no se observa consentimiento ni aviso de privacidad en el cliente.

### Sin respuesta por ingeniería inversa
1. Valores de "Tipo de rol" y significado exacto de "Programa Agenda": lógica del servidor.
2. Catálogo exacto de permisos por módulo (columna "Permiso") y de "Otros permisos": lógica del servidor (se cargan de la base).
3. Qué tablas transfiere la unificación de historias y si es reversible: lógica del servidor.
4. Valores de "Tipo usuario" de Credenciales SISPRO y si la clave se almacena cifrada: lógica del servidor.
5. Qué captura el panel de datos biométricos y el formato exigido del XLS de pacientes: requiere paciente real (el panel no expone código en el JS de la página).
6. Qué parámetros contiene Configuración General / Entidad y cuáles gobiernan el comportamiento: decisión del negocio (configuración propia de cada instalación) y lógica del servidor.
7. Si "Cerrar sesión" fuerza realmente el cierre remoto (el JS envía el mismo tipo que "Iniciar chat"): lógica del servidor.
