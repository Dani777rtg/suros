# Configuración, seguridad, herramientas y pacientes

Resumen: este bloque cubre la parametrización del sistema (entidad, especialidades, laboratorio, subplanes, páginas), la seguridad (funcionarios, usuarios, roles, módulos, informes por usuario, sesiones activas), las herramientas (unificación de historias, consentimientos), la cuenta propia y el maestro de pacientes. 21 pantallas. Dos pantallas vienen sin extracción (Credenciales SISPRO, Empresas) y una casi vacía (Configuración General). Fuente: extracción de UI (Ext.NET); todo lo no visible se marca "(inferido)".

Ruidos globales omitidos: messagebox, OK/Yes/No/Cancel, paginación, ordenar/columnas.

---

## CONFIGURACION GENERAL > CONFIGURACIÓN GENERAL (/SUROS/Vistas/Privado/General/ConfiguracionGeneral.aspx)
- **Propósito**: editar parámetros generales del sistema en formato clave/valor (inferido).
- **Funcionalidades**: el usuario puede ver la lista de configuraciones, editar una configuración seleccionada ("Editar esta configuración") y guardar ("Guardar Configuracion").
- **Datos**: sin campos extraídos (el formulario de edición no aparece; inferido que es una ventana o fila editable).
- **Listados**: grid con Id, Configuración.
- **Flujos y reglas**: seleccionar fila, editar, guardar (inferido). Pantalla casi vacía en la extracción.

## CONFIGURACION GENERAL > FUNCIONARIO > GESTIONAR DATOS FUNCIONARIO (/SUROSHistoriaClinica/Vistas/Privado/Funcionario/FormularioFuncionario.aspx)
- **Propósito**: crear y editar la ficha de funcionarios (personal asistencial/administrativo) incluida su información médica.
- **Funcionalidades**: el usuario puede buscar funcionario por documento/nombre ("Buscar funcionario"; ventana "Coincidencia encontrada" con lista de resultados); guardar cambios; cancelar; limpiar formulario; buscar municipio de nacimiento/residencia (ventana "Municipio" con País/Departamento/Municipio); subir archivo (firma; ventanas "Seleccionar firma" y "Asignar firma"); adicionar especialidad (ventana "Especialidad medica") y adicionar convenio (ventana "Convenios", lista de empresas); seleccionar programas PyP asociados (ventana "Seleccionar los programas asociados"); cambiar estado.
- **Datos**:
  - Identificación: tipo documento {ADULTO SIN IDENTIFICACION, CEDULA DE CIUDADANIA, CEDULA EXTRANGERA, MENOR SIN IDENTIFICACION, NIT, PASAPORTE, REGISTRO CIVIL, TARJETA DE IDENTIDAD, TARJETA EXTRANJERIA, CERTIFICADO NACIDO VIVO, PERMISO ESPECIAL DE PERMANENCIA, PERMISO POR PROTECCION TEMPORAL, PERMISO TEMPORAL}, documento, primer/segundo nombre, primer/segundo apellido.
  - Demografía: género {MASCULINO, FEMENINO, INDETERMINADO O INTERSEXUAL}, fecha de nacimiento, etnia {OTRAS ETNIAS, INDIGENA, RAIZAL, GITANO, PALENQUERO DE SAN BASILIO, NEGRO/MULATO/AFROCOLOMBIANO/AFRODESCENDIENTE, AFROCOLOMBIANO}, estado civil {ESTADO NO SUMINISTRADO, CASADO(A), DIVORCIADO(A), MENOR DE EDAD, SOLTERO(A), UNION LIBRE, VIUDO}, discapacidad {FÍSICA, VISUAL, AUDITIVA, INTELECTUAL, SICOSOCIAL, SORDOCEGUERA, MÚLTIPLE, SIN DISCAPACIDAD}, nivel educativo {NO DEFINIDO, PRESCOLAR, BASICA PRIMARIA, BASICA SECUNDARIA, MEDIA ACADEMICA O CLASICA, MEDIA TECNICA, NORMALISTA, TECNICA PROFESIONAL, TECNOLOGICA, PROFESIONAL, ESPECIALIZACION, MAESTRIA, DOCTORADO}.
  - Contacto/ubicación: municipio de nacimiento, municipio de residencia, dirección/barrio, celular, teléfono, email.
  - Laboral: ocupación, cargo, empresa, estado {ACTIVO, INACTIVO}, "Es medico" {SI, NO}.
  - Información general del médico (fieldset): registro profesional, licencia de salud ocupacional.
  - Ventana de especialidad: estado {ACTIVO, INACTIVO}, cirugía {SI, NO}, PyP {SI, NO} (inferido por columnas del grid).
  - Ventana Convenios: empresa.
- **Listados**: especialidades del funcionario (Especialidad, Estado, Cirugia, PyP); convenios (Convenio); programas PyP (PROGRAMA PYP); coincidencias (DOCUMENTO, NOMBRE FUNCIONARIO); empresas; descripciones.
- **Flujos y reglas**: buscar existente -> cargar -> editar -> guardar; si no existe, se crea (inferido). El bloque médico aplica sólo si "Es medico" = SI (inferido). Sólo funcionarios con firma cargada podrían firmar documentos clínicos (inferido, por "Seleccionar firma").

## CONFIGURACION GENERAL > FUNCIONARIO > USUARIO Y CONTRASEÑA (/SUROS/Vistas/Privado/Usuario/UsuarioCredenciales.aspx)
- **Propósito**: administrar los usuarios de acceso de los funcionarios.
- **Funcionalidades**: el usuario puede filtrar por estado y nombre de persona, actualizar la lista, crear usuario, eliminar usuario y asignar contraseña a un usuario (ventana "Asignar contraseña a usuario").
- **Datos**: filtro estado {ACTIVO, INACTIVO}, filtro Nombre persona; ventana de credenciales: Usuario, Contraseña, Confirmar contraseña.
- **Listados**: Usuarios (Tipo Docum, Documento, Nombre persona, Nombre usuario, Estado usuario).
- **Flujos y reglas**: un usuario se vincula a un funcionario existente (inferido); contraseña con confirmación; la eliminación puede ser lógica (inferido).

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN ROL A USUARIO (/SUROS/Vistas/Privado/Usuario/Roles/RolUsuario.aspx)
- **Propósito**: asignar roles a usuarios y conceder permisos sobre módulos indirectos.
- **Funcionalidades**: el usuario puede buscar usuario por nombre; ver los roles asignados y los disponibles; asignar o quitar un rol; abrir "Otros Permisos" (ventana "Gestionar otros permisos", combo {INICIO HISTORIA}); gestionar permisos a módulos indirectos (ventana) con búsqueda por especialidad y permisos Ver (Todos/Propios) e Imprimir (Todos/Propios); actualizar lista de permisos; aceptar/cancelar.
- **Datos**: combo de módulos indirectos {ACTIVACION DE CITA, ACTIVIDADES DE ENFERMERIA, AGENDA MEDICA, CARGAR INVENTARIOS, CATALOGOMEDICAMENTO.ASPX, CONSULTA EXTERNA, HISTORIA CRONICOS, HISTORIA URGENCIA, INICIO, INICIO HISTORIA, PEDIDOS INTERNOS, REPORTE CITAS MEDICAS}; checkboxes VerTodos, VerPropios, ImprimirTodos, ImprimirPropios.
- **Listados**: Usuarios (Documento, Nombre persona, Nombre usuario, Estado usuario); Rol asignado (Rol); Rol disponible (Rol); permisos (Descripción, Permiso; por especialidad: Descripción, Todos, Propios, Todos, Propios).
- **Flujos y reglas**: un usuario puede tener varios roles (inferido por grids asignado/disponible). Permisos "Propios" vs "Todos": restringen a los registros del propio profesional o a todos (inferido). Los permisos por especialidad se dan por módulo indirecto.

## CONFIGURACION GENERAL > FUNCIONARIO > ASIGNACIÓN INFORMES USUARIO (/SUROS/Vistas/Privado/Usuario/AsignacionInformeUsuario.aspx)
- **Propósito**: definir qué informes puede ver cada usuario y registrar nuevos informes.
- **Funcionalidades**: el usuario puede buscar funcionario; ver árbol de informes disponibles; asignar o quitar un informe al usuario; "Agregar Nuevo Reporte" (ventana "Agregar Reporte": grupo, carpeta, nombre del reporte, página) y elegir página de la lista "Paginas disponibles" (nombre, nombre página, URL); guardar/salir.
- **Datos**: Nombre Grupo, Nombre Carpeta, Nombre Reporte, Página; filtros nombre/URL de páginas.
- **Listados**: FUNCIONARIOS (Documento, Nombre persona, Nombre usuario, Estado usuario); INFORMES ASIGNADOS (ID, CODIGO, INDICADOR, DOMINIO, RESOLUCION); páginas disponibles (Nombre, Nombre página, Url página); árbol INFORMES DISPONIBLES.
- **Flujos y reglas**: un reporte = grupo > carpeta > nombre, enlazado a una página del sistema. Las columnas INDICADOR/DOMINIO/RESOLUCION sugieren informes regulatorios (inferido, p. ej. resoluciones de indicadores). Hay una ventana "Request Failure" de error AJAX.

## CONFIGURACION GENERAL > CONFIGURACION ENTIDAD HOSPITALARIA (/SUROS/Vistas/Privado/General/InformacionEntidad.aspx)
- **Propósito**: datos de la institución y parámetros globales.
- **Funcionalidades**: el usuario puede editar datos generales de la entidad, editar el valor de cada parámetro (combo ComboValor) y guardar.
- **Datos**: nombre, NIT, correo, dirección, teléfono, ciudad, nivel (numérico).
- **Listados**: Configuración general (Item, Nombre, Descripción, Valor).
- **Flujos y reglas**: el valor de cada parámetro se elige de un combo según el ítem (inferido); confirmación de guardado (messagebox "Notificación").

## CONFIGURACION GENERAL > GESTIONAR ESPECIALIDAD (/SUROSHistoriaClinica/Vistas/Privado/Medico/Especialidad.aspx)
- **Propósito**: catálogo de especialidades médicas y tipos de especialidad, con su comportamiento en agenda e historia.
- **Funcionalidades**: el usuario puede crear, editar y eliminar tipos de especialidad (Nuevo/Editar/Eliminar); crear/editar especialidades (Aceptar/Cancelar); asociar módulos (recurso) principal y secundario que se usan al atender desde la agenda médica; "Transferir a" (mover especialidades a otro tipo, inferido).
- **Datos**: Nombre; "Multiple cita" {SI, NO}; Recurso 1, Recurso 2; checks: Otras Evoluciones, Permite Remontar Agenda, Fórmula Médica Otras Evoluciones, Mostrar Panel Escala detección riesgo suicida en otras evoluciones; tipo de especialidad (TIES_NOMBRE, TIES_MULTIPLECITA {SI, NO}); campo fecha.
- **Listados**: Tipo especialidad (Descripción, Multiple cita); Especialidad (Módulo/Recurso principal, secundario, Otras Evoluciones); Modulo(Recurso) (Nombre).
- **Flujos y reglas**: el recurso define qué módulo abre el médico al atender desde la agenda. "Multiple cita" permite más de una cita por paciente en esa especialidad (inferido). "Remontar agenda" habilita reabrir/ampliar agenda (inferido).

## CONFIGURACION GENERAL > PAGINAS DEL SISTEMA (/SUROS/Vistas/Privado/General/Paginas.aspx)
- **Propósito**: registro de las páginas (URLs) disponibles para armar módulos y roles.
- **Funcionalidades**: el usuario puede ver el árbol de recursos disponibles, actualizar el árbol, crear una nueva página (ventana "Adicionar pagina al sistema"), eliminarla y actualizar la lista.
- **Datos**: Nombre página, Url, Estado {ACTIVO, INACTIVO}; filtros por ID, nombre, URL, página.
- **Listados**: Paginas disponibles (ID, Nombre, Url página, Nombre página, Estado); árbol de recursos.
- **Flujos y reglas**: el árbol parece reflejar los archivos .aspx del servidor, desde donde se registran (inferido). Estas páginas alimentan Roles y Módulos e Informes.

## CONFIGURACION GENERAL > ROLES Y MODULOS (/SUROS/Vistas/Privado/Usuario/Roles/RolModulos.aspx)
- **Propósito**: definir roles y la estructura de menú (grupos y módulos) con permisos.
- **Funcionalidades**: el usuario puede crear/editar/eliminar roles; ver usuarios asociados al rol; gestionar módulos indirectos; armar el árbol de módulos: adicionar grupo, adicionar módulo, insertar en un grupo, editar nombre, editar módulo, eliminar módulo, subir/bajar orden, copiar módulos a otro rol (ventana); elegir ícono (ventana "Iconos disponibles"); elegir página; habilitar permisos del módulo y guardarlos.
- **Datos**:
  - Rol (ventana "Nuevo rol"): estado {ACTIVO, INACTIVO}, tipo rol, nombre rol, observación, check "Programa Agenda".
  - Módulo (ventana "Adicionar Modulo"): nombre módulo, orden (numérico), página, ícono, especialidad.
  - Tipo de módulo {INICIO, HISTORIA CLINICA, PAGINA WEB, ALMACEN}.
- **Listados**: Roles del sistema (Usuario, Programa Agenda, Estado); usuarios asociados (Tipo doc, Número documento, Nombre usuario; Usuario, Programa Agenda); árbol de configuración de módulos; Asignar permisos al módulo (Descripción, Permiso); permisos de módulos indirectos (Descripción, Permiso); páginas disponibles (Nombre, Nombre página, URL).
- **Flujos y reglas**: rol -> árbol de grupos/módulos (orden) -> cada módulo apunta a una página; los permisos por módulo se asignan por descripción de permiso (inferido: lista de acciones por módulo). "Programa Agenda" marca el rol como programable en la agenda (inferido). Los módulos pueden asociarse a una especialidad.

## CONFIGURACION GENERAL > USUARIOS ACTIVOS EN SUROS (/SUROS/Vistas/Privado/SignalR/UsuariosActivos.aspx)
- **Propósito**: monitorear sesiones conectadas y comunicarse con ellas (SignalR).
- **Funcionalidades**: el usuario puede ver usuarios conectados, enviar mensaje a uno, cerrar la sesión de un usuario, iniciar chat, preparar y enviar mensaje masivo (ventana "Envio Masivo").
- **Datos**: Mensaje (texto).
- **Listados**: Id usuario, Nombre usuario, Conectado desde, Ip, Rol, Especialidad, Fecha y hora conexión, Id Signal.
- **Flujos y reglas**: comunicación en tiempo real por conexión SignalR (Id Signal). Cerrar sesión fuerza logout remoto (inferido); la ventana "Sesión finalizada" global lo respaldaría.

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
- **Propósito**: gestionar las credenciales de acceso al servicio web SISPRO/MinSalud (inferido por el nombre). Página HTML estándar (no Ext), extraída por DOM.
- **Funcionalidades**: el usuario puede agregar una credencial (GUARDAR), modificar una existente (Editar en la fila, luego Modificar), limpiar el formulario, buscar en la grilla y exportar (Copy, CSV, Excel, PDF, Print).
- **Datos**: Tipo de documento {AS, CC, CE, MS, NT, PA, RC, TI, TE, NV, PEP, PPT, PT}; Número; Clave; NIT; Estado activo; Tipo de usuario (combo sin valores extraídos).
- **Listados**: ID | Tipo documento | Número | Clave | NIT | Tipo usuario | Estado | Acciones. La columna Clave aparece en la grilla (se desconoce si se muestra enmascarada).
- **Flujos y reglas inferidas**: cada fila es el acceso de un usuario SISPRO asociado a un NIT (inferido); la edición carga la fila en el formulario y cambia GUARDAR por Modificar (inferido).

## CONFIGURACION GENERAL > EMPRESAS (/SUROS/Vistas/Privado/Empresa/Empresa.aspx)
- **Sin extracción útil**: la re-extracción devolvió el título vacío y ningún campo, botón ni grilla.
- **Propósito**: catálogo de empresas/aseguradoras (EPS, particular) usadas en pacientes, convenios y facturación (inferido; en Pacientes el filtro de EPS lista "ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I").
- **Funcionalidades**: crear, editar, listar empresas (sin extracción, inferido).

## CONFIGURACION GENERAL > SUBPLANES SERVICIOS (/SUROSFacturacion/Vistas/Privado/SubPlanes/SubPlanesServicios.aspx)
- **Propósito**: relacionar servicios con subplanes (facturación).
- **Funcionalidades**: el usuario puede buscar un servicio, listar los subplanes asignados, agregar un subplan al servicio (ventana de subplanes disponibles) y eliminar un subplan del servicio.
- **Datos**: Servicio (trigger de búsqueda), SUSE_ID, SUPL_NOMBRE.
- **Listados**: Servicios (Servicio); SubPlanes asignados (Id Único, SubPlan); SubPlanes disponibles (SubPlan).
- **Flujos y reglas**: relación N:M servicio-subplan (tabla SUSE inferida del nombre del campo). Un subplan define qué servicios cubre (inferido).

## HERRAMIENTAS > UNIFICACION HISTORIA CLINICA (/SUROSHistoriaClinica/Vistas/Privado/HistoriaClinica/UnificarHistoriaClinica.aspx)
- **Propósito**: fusionar historias clínicas de pacientes duplicados.
- **Funcionalidades**: el usuario puede buscar dos pacientes (Paciente 1 y 2, con ventana de coincidencias por documento/nombre), ver sus atenciones, transferir información de uno a otro ("Transferir información"), eliminar un paciente, acceder a opciones del paciente.
- **Datos**: documento/nombre de cada paciente; ventana "Transferir información" (células/nombre).
- **Listados**: Paciente 1 y Paciente 2 (ID, Fecha entrada, Fecha salida, Profesional que registra, Estado); coincidencias (Documento, Nombre paciente; Descripción).
- **Flujos y reglas**: origen -> destino; tras transferir, el duplicado se elimina (inferido). Operación destructiva: requiere confirmación y permiso (inferido).

## HERRAMIENTAS > DISEÑADOR DE CONSENTIMIENTOS (/SUROS/Vistas/Privado/Formatos/Formatos.aspx)
- **Propósito**: diseñar formatos de consentimiento informado versionados, con comodines que se llenan al imprimir.
- **Funcionalidades**: el usuario puede crear/editar/eliminar tipos de formato (filtro por nombre, paginado); crear nueva versión, copiar versión, eliminar versión; editar cabecera, contenido principal y pie con editor HTML (modo código, alineación, estilos, listas, enlaces, imágenes y documentos subidos, bloques Destacado/Nota/Alerta); insertar comodines; previsualizar en PDF; imprimir formatos; asociar procedimientos médicos (búsqueda); abrir ayuda de comodines y edición de versiones.
- **Datos**:
  - Tipo de formato: Nombre, Descripción.
  - Versión: Título, Código, Versión, Tipo de consentimiento {CONSENTIMIENTOS INFORMADOS}, Cabecera, Contenido principal, Pie de página (combos para reutilizar cabecera/pie).
  - Comodines disponibles: nombre del formato, código y versión del formato, logo de la empresa, tabla de diseño, nombre/documento/tipo documento de la persona, firma y huella de la persona, médico en sesión (nombre, firma, especialidad), representante legal o familiar (nombre, identificación y parentesco), fecha actual, nombre de la empresa y del gerente, contenido, procedimiento a realizar y realizado (código y nombre).
  - También hay campos de tipo noticia en la misma página (NOTI_ID, categoría, fecha publicación, palabras clave, estado, periodista, URL, orden, imagen principal, resumen); parecen reutilizar el editor de noticias (inferido, fuera del alcance del diseñador).
- **Listados**: Tipos de Formatos (Título); Versiones de Formatos (Título, Código, Versión); procedimientos (Código, Descripción).
- **Flujos y reglas**: tipo -> N versiones; sólo una versión vigente por código (inferido); un formato se liga a procedimientos para imprimirse al realizarlos (inferido).

## MI CUENTA > CAMBIAR CONTRASEÑA (/SUROS/Vistas/Privado/Funcionario/CambiarContrasena.aspx)
- **Propósito**: el usuario cambia su propia clave.
- **Funcionalidades**: el usuario puede ingresar contraseña actual, nueva y confirmación, y aceptar.
- **Datos**: contraseña actual, nueva contraseña, repetir contraseña.
- **Flujos y reglas**: valida la actual y que las dos nuevas coincidan (inferido).

## MI CUENTA > DATOS PERSONALES (/SUROS/Vistas/Privado/Funcionario/FormularioFuncionarioPersonal.aspx)
- **Sin extracción útil**: la re-extracción sólo devolvió el título "Datos personales funcionario", sin campos ni botones.
- **Propósito**: el funcionario ve/edita sus propios datos (inferido; versión personal del formulario de funcionario).
- **Funcionalidades**: ver/editar datos propios (sin extracción, inferido).

## PACIENTE > CONSULTAR CITAS DEL PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/ReporteCitasPaciente.aspx)
- **Propósito**: consultar el historial de citas de un paciente.
- **Funcionalidades**: el usuario puede buscar paciente por documento o nombre (ventana de coincidencias), consultar sus citas y agrupar/ordenar la grilla.
- **Datos**: Documento/Nombre; documento y nombre del paciente (sólo lectura).
- **Listados**: Citas médicas del paciente (Mes, Fecha, Turno, Hora, Médico, Registrado por, Nota, Tipo asignación, Estado); coincidencias (Documento, Nombre paciente).
- **Flujos y reglas**: sólo lectura (inferido).

## PACIENTE > DATOS PACIENTE (/SUROSHistoriaClinica/Vistas/Privado/Paciente/FormularioPaciente.aspx)
- **Propósito**: crear y editar la ficha demográfica, administrativa y biométrica del paciente.
- **Funcionalidades**: el usuario puede buscar paciente (documento/nombre), guardar, guardar y cerrar, limpiar formulario; cargar foto de perfil (ventana "Actualizando Foto de Inicio"); cargar documento frente y reverso (Cara A/B); registrar datos biométricos (panel; huella inferida por comodín de consentimientos); buscar municipio (nacimiento, residencia, expedición); asignar o borrar acompañante/responsable (ventana "Datos del Responsable"); buscar grupo poblacional (ventana con grilla); cargar archivo XLS (probable carga masiva, inferido).
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
- **Flujos y reglas**: buscar -> cargar -> editar -> guardar; si el tipo de afiliado es beneficiario se pide nombre del cotizante (inferido); exoneración de copago habilita el tipo (inferido); para menores el acompañante/responsable es relevante (inferido).

## PACIENTE > PACIENTES (/SUROSHistoriaClinica/Vistas/Privado/Paciente/Paciente.aspx)
- **Propósito**: listado maestro y buscador de pacientes.
- **Funcionalidades**: el usuario puede filtrar por ID, documento, nombre, género, fecha de nacimiento, celular, email y empresa; ver total de pacientes; refrescar; exportar; abrir un paciente en "Consultar y gestionar" (lleva al formulario de paciente, inferido).
- **Datos**: filtros; empresa {ASMET SALUD EPS SAS, PARTICULAR, PIJAOS SALUD E.P.S.I} (lista dependiente de los datos del entorno).
- **Listados**: ID, Foto, Documento, Nombre, Sexo, Nacimiento, Celular, Email, EPS (paginado). Existe un botón "Esta lista contiene mis pedidos de insumos" que parece residual de otra pantalla (inferido).

---

## Modelo de seguridad
- **Funcionario**: persona con ficha laboral (identificación, cargo, ocupación, empresa, estado, firma, especialidades, convenios, programas PyP). Si es médico, además registro profesional y especialidades.
- **Usuario**: credenciales (usuario/clave, estado ACTIVO/INACTIVO) ligadas a un funcionario; crear, eliminar, asignar clave; cada persona puede cambiar su clave (Mi cuenta).
- **Rol**: nombre, tipo, observación, estado, indicador "Programa Agenda". Un usuario tiene N roles.
- **Módulos**: cada rol tiene un árbol ordenado de grupos y módulos; el módulo apunta a una página del sistema, tiene ícono, tipo {INICIO, HISTORIA CLINICA, PAGINA WEB, ALMACEN} y puede ligarse a una especialidad. Se pueden copiar módulos entre roles.
- **Páginas**: catálogo de URLs (nombre, URL, estado) del que se arman módulos e informes.
- **Permisos**: (1) por módulo, lista de permisos de descripción habilitables; (2) módulos indirectos (accesos sin menú, p. ej. AGENDA MEDICA, HISTORIA URGENCIA) con permisos Ver/Imprimir x Todos/Propios, por especialidad; (3) "otros permisos" (INICIO HISTORIA); (4) informes asignados por usuario.
- **Sesiones**: monitor de conectados (IP, rol, especialidad, hora), cierre remoto, mensajería y chat (SignalR).
- **Sedes**: no aparecen en estas pantallas; la autorización por sede no es visible en el UI extraído (ver preguntas abiertas).

## Entidades y estados
- Funcionario (estado ACTIVO/INACTIVO), Usuario (ACTIVO/INACTIVO), Rol (ACTIVO/INACTIVO), Página (ACTIVO/INACTIVO), Módulo, Permiso, Informe.
- Especialidad, Tipo de especialidad, Recurso/módulo de atención.
- Entidad hospitalaria, Configuración/parámetro, Empresa, Convenio, SubPlan, Servicio.
- Estudio de laboratorio, Analito, Unidad de medida, Opción de respuesta (estado ACTIVO/INACTIVO).
- Formato de consentimiento, Versión de formato, Comodín.
- Paciente (estado de paciente y "continúa atención" Sí/No), Responsable/acompañante, Grupo poblacional, Cita (estado, tipo de asignación), Atención (ID, entrada, salida, profesional, estado).

## Preguntas abiertas
1. Sedes: ¿el usuario/rol se restringe por sede o la sede se elige al ingresar? No aparece en ninguna pantalla de seguridad.
2. Empresas y Datos personales siguen sin campos (la re-extracción sólo dio título); de Credenciales SISPRO se conocen los campos, pero no qué servicios SISPRO se consumen, los valores de Tipo usuario ni si la clave se almacena/muestra enmascarada.
3. Qué parámetros contiene Configuración General / Entidad (ítems y combos de valor) y cuáles gobiernan el comportamiento del sistema.
4. Catálogo exacto de permisos por módulo (columna "Permiso") y semántica de "Todos/Propios" y "Otros permisos".
5. Alcance real de la unificación de historias (qué tablas se transfieren, si es reversible) y relación de la página de Formatos con el módulo de noticias.
6. Tipo de rol (valores) y significado de "Programa Agenda"; cómo se cargan las páginas desde el árbol de recursos (escaneo de archivos o alta manual).
7. Carga de archivo XLS en Datos Paciente: formato y regla de importación; qué captura el panel de datos biométricos.
