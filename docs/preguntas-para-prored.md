# Preguntas que solo PRORED puede responder

Ingeniería inversa terminada (pantallas + código JavaScript + norma colombiana). Lo que queda abajo **no se puede sacar del sistema**: está en el servidor, requiere atender un paciente real o es una decisión del negocio. Agrupado por quién lo sabe. El detalle y el contexto de cada una está en la sección "Sin respuesta por ingeniería inversa" de cada módulo.

## Para el administrador del sistema (o SoftProject)

1. **Estados y transiciones.** Lista completa y qué acción dispara cada cambio, para: cita, franja de agenda, turno de urgencias, ingreso, factura (borrador, anulada, glosada), orden de compra y pedido (incluido "Consolidado"), y órdenes de imágenes, interconsultas y remisiones.
2. **Permisos.**
   - La matriz de permisos por rol y sede: bloquear, activar para BOT, trasladar, eliminar, visar, anular, convertir recibos, aprobar compras y despachos.
   - Los valores de "Tipo de rol", qué significa "Programa Agenda" y cuál es el catálogo de "Otros permisos".
3. **Parámetros.** Qué contienen Configuración General y Entidad, y cuáles cambian el comportamiento del sistema. Por ejemplo: `AUT_MAX_MESES_RANGO`, `ENVIARCOPAGODIAN` y los umbrales del semáforo de vencimientos.
4. **Unificación de historias.** Qué tablas se trasladan, si se puede revertir y qué pasa con los folios, las facturas y el RDA ya enviados.
5. **Borrados.** Cuando se elimina un registro (por ejemplo, de la bitácora), ¿es lógico o físico?
6. **Credenciales SISPRO.** Los tipos de usuario y si la clave se guarda cifrada.
7. **Sesión.** ¿"Cerrar sesión" cierra de forma remota la sesión de otro usuario?

## Para facturación

1. **Reglas de asignación de citas.**
   - Validez de la autorización y del contrato.
   - Límite de citas por día y paciente duplicado en la agenda.
   - Cuándo se cobra copago o cuota moderadora, y con qué montos según la categoría de afiliación.
2. **Contratos.** Los campos de "Crear contrato" y cómo se calcula el valor en cada modalidad: paquete, costo fijo externo, PGP y capitación.
3. **Caja.** Cuándo se cierra definitivamente y qué pasa con la apertura vigente al guardar el arqueo.
4. **Resolución DIAN.** ¿Se bloquea el consecutivo al agotarse el rango o al vencer la resolución?
5. **SOAT/FURIPS.** Qué hace aparecer ese panel y por qué un servicio "no se puede facturar" por el homólogo.
6. **Integraciones.**
   - Qué se hace con el archivo CUV de la factura global.
   - Qué envía "Enviar a NEOSAGE".
   - Si el módulo genera RIPS o reportes de la Res. 3280.
   - Cómo se valida y reintenta el envío del RDA, y cómo se relaciona con RIPS y facturación.
7. **"Res. 1557".** Qué cubre y por qué tiene un editor aparte.

## Para el área clínica (médico o enfermera jefe)

1. **Formularios por especialidad.** Qué formulario de historia usa cada especialidad: odontología, apoyo terapéutico y medicina especializada.
2. **Agendas internas.** Qué contienen las agendas de hospitalización, observación y cirugía, la nota quirúrgica y las actividades de enfermería.
3. **Destinos de urgencias.** Qué efecto tiene cada destino en el ingreso: morgue, retiro voluntario, fuga, observación, hospitalización o cirugía.
4. **Programas.** Con qué criterios clínicos se aprueba el ingreso a un programa (afinamiento, crónicos, PyP) y cómo se asigna al paciente.
5. **Valores por defecto en el código:**
   - La saturación de oxígeno vacía se guarda como 95.
   - Se usa la fórmula M2 = peso × 4 + 7.
   - ¿Son intencionales? También la hora de egreso sin validar.
6. **Con un paciente de prueba:**
   - La precarga desde urgencias o desde un registro externo.
   - Los tratamientos anteriores y las plantillas.
   - El consentimiento de rayos X.
   - Qué captura el panel biométrico (huella y foto).
   - El formato del XLS de carga de pacientes.

## Para farmacia y almacén

1. **Lotes.** Orden real de salida (FEFO o FIFO) y qué pasa al vencer un lote.
2. **Fórmula y dispensación.** Cómo se crea la solicitud "Formulada" desde la historia clínica y cómo se factura lo dispensado.
3. **Medicamentos de control especial.** Qué contienen los reportes de controlados y las actas de entrega.
4. **Préstamos.** Cómo funcionan los préstamos de suministros entre entidades.

## Para gerencia

1. **Pantallas a migrar.** ¿Se siguen usando las pantallas "OLD" (citas e inventarios), y quién las ve?
2. **Fuera de alcance.** ¿Entran en el alcance punto de venta, punto local, tienda en línea y página web (CMS)?
3. **Agendamiento por BOT.** Qué significan "Prioritaria" y "Por defecto" en la práctica.
4. **WhatsApp.**
   - Proveedor y plantillas aprobadas.
   - ¿Se verifica la autorización de datos (Ley 1581) antes de enviar?
5. **Informes.**
   - Qué informes hay por especialidad y cómo se calculan los indicadores.
   - Qué hacen "Mensajes masivos", el reporte de larga instancia y los colores de la agenda de hospitalización.
