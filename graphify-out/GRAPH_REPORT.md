# Graph Report - docs/modulos  (2026-10-14)

## Corpus Check
- Corpus is ~26,247 words - fits in a single context window. You may not need a graph.

## Summary
- 236 nodes · 369 edges · 18 communities (11 shown, 7 thin omitted)
- Extraction: 74% EXTRACTED · 26% INFERRED · 0% AMBIGUOUS · INFERRED: 96 edges (avg confidence: 0.78)
- Token cost: 238,922 input · 0 output

## Community Hubs (Navigation)
- Facturacion contratos y caja
- Agendamiento y demanda inducida
- Ingreso y atencion clinica
- Inventario y abastecimiento
- Citas autorizaciones y pacientes
- Seguridad roles y funcionarios
- Pedidos internos y enfermeria
- Catalogo de medicamentos
- Informes e indicadores
- Afinamientos y preingresos
- Turnero atencion al usuario
- Punto de venta y tickets
- PyP y ciclo RPMS
- Entidad hospitalaria
- Configuracion general
- Datos de funcionario
- Categorias
- Empresa proveedora

## God Nodes (most connected - your core abstractions)
1. `Cita médica unificada` - 19 edges
2. `Módulo Facturación` - 19 edges
3. `Módulo Citas médicas` - 13 edges
4. `Facturador manual V2` - 12 edges
5. `Historia clinica consulta externa` - 12 edges
6. `Cita` - 11 edges
7. `Farmacia (panel regente)` - 11 edges
8. `Factura` - 10 edges
9. `DIAN` - 10 edges
10. `Despacho pedidos` - 9 edges

## Surprising Connections (you probably didn't know these)
- `Reautenticacion con usuario y clave` --semantically_similar_to--> `Despacho pedidos`  [INFERRED] [semantically similar]
  06-historia-clinica.md → 05-almacen-farmacia.md
- `Llamada de bitácora` --references--> `Factura`  [INFERRED]
  01-citas-medicas.md → 03-facturacion.md
- `Administracion Catalogo Medicamentos` --semantically_similar_to--> `Catalogo Medicamento Nuevo`  [INFERRED] [semantically similar]
  04-informes-catalogos.md → 05-almacen-farmacia.md
- `Cita médica unificada` --references--> `Diseñador de consentimientos`  [INFERRED]
  01-citas-medicas.md → 02-configuracion-seguridad-pacientes.md
- `Datos paciente` --shares_data_with--> `Cita médica unificada`  [INFERRED]
  02-configuracion-seguridad-pacientes.md → 01-citas-medicas.md

## Hyperedges (group relationships)
- **Flujo cita a activación a facturación** — 01_citas_medicas_agenda_medica, 01_citas_medicas_cita_unificada, 01_citas_medicas_activacion_cita, 03_facturacion_facturador_v2, 03_facturacion_recibo_copago [INFERRED 0.80]
- **Facturación electrónica y validación DIAN/Ministerio** — 03_facturacion_listado_facturas, 03_facturacion_factura_global, 03_facturacion_nota_credito, 03_facturacion_dian, 03_facturacion_websispro, 03_facturacion_cuv [EXTRACTED 1.00]
- **Modelo de seguridad usuario-rol-módulo-página** — 02_configuracion_seguridad_pacientes_funcionario, 02_configuracion_seguridad_pacientes_usuario, 02_configuracion_seguridad_pacientes_rol, 02_configuracion_seguridad_pacientes_modulo_menu, 02_configuracion_seguridad_pacientes_paginas_sistema, 02_configuracion_seguridad_pacientes_permisos_modulos_indirectos [EXTRACTED 1.00]
- **Cadena de abastecimiento a dispensacion** — 05_almacen_farmacia_plan_compra, 05_almacen_farmacia_orden_compra, 05_almacen_farmacia_carga_inventarios, 05_almacen_farmacia_pedido_interno, 05_almacen_farmacia_despacho_pedidos, 05_almacen_farmacia_farmacia [EXTRACTED 0.95]
- **Flujo de urgencias Triage a facturacion** — 06_historia_clinica_triage, 06_historia_clinica_agenda_urgencia, 06_historia_clinica_historia_urgencia, 06_historia_clinica_destino, 06_historia_clinica_epicrisis, 06_historia_clinica_facturacion [INFERRED 0.85]
- **Dispensacion a paciente entre HC y Almacen** — 06_historia_clinica_inicio_historia, 05_almacen_farmacia_enfermeria, 05_almacen_farmacia_farmacia, 05_almacen_farmacia_lote, 05_almacen_farmacia_acta_entrega [INFERRED 0.80]

## Communities (18 total, 7 thin omitted)

### Community 0 - "Facturacion contratos y caja"
Cohesion: 0.08
Nodes (49): Contrato (EPS), Programa Res. 3280 / RIPS, Credenciales SISPRO, SISPRO / MinSalud, Subplan, Subplanes servicios, Apertura de caja, Buscar una factura (+41 more)

### Community 1 - "Agendamiento y demanda inducida"
Cohesion: 0.09
Nodes (36): Activación de cita, Adjunto, Programar agenda médica, Bitácora demanda inducida, BOT App/Web (canal de agendamiento), Campaña WhatsApp, Cita médica unificada, Consentimiento informado (+28 more)

### Community 2 - "Ingreso y atencion clinica"
Cohesion: 0.09
Nodes (36): Agenda Hospitalizacion (facturacion/instancia), Diagnostico CIE-10, Despacho de suministros desde enfermeria, Estado de ingreso, Ingreso, Inicio Almacen, Inicio Historia Clinica (home), Pagina Web (CMS) (+28 more)

### Community 3 - "Inventario y abastecimiento"
Cohesion: 0.11
Nodes (26): Acta de entrega, Activacion de cargas, Ajuste de inventario, Carga de inventarios, Centros de costo, Ciclo de abastecimiento, Despacho pedidos, Devolucion a inventario de farmacia (+18 more)

### Community 4 - "Citas autorizaciones y pacientes"
Cohesion: 0.11
Nodes (23): Autorización / Orden, Cita, Empresa / EPS, Estado de recepción de autorización, Paciente, Prestador PRORED (sedes), Procedimiento (CUPS), Recepción autorizaciones (+15 more)

### Community 5 - "Seguridad roles y funcionarios"
Cohesion: 0.18
Nodes (18): Agenda (programación), Asignación informes usuario, Cambiar contraseña, Gestionar especialidad, Especialidad, Funcionario, Gestionar datos funcionario, Modelo de seguridad (+10 more)

### Community 6 - "Pedidos internos y enfermeria"
Cohesion: 0.14
Nodes (15): Almacenes, Canastas de cirugia, Enfermeria (solicitud de insumos), Estados de solicitud/pedido, Estados de pedido, Parametros de configuracion, Pedido interno, Solicitudes de suministros (+7 more)

### Community 7 - "Catalogo de medicamentos"
Cohesion: 0.24
Nodes (10): Administracion Catalogo Medicamentos, Medicamento (catalogo de nombres), Plantilla Insumos, Plantilla Medicamentos, Catalogo Insumos Nuevo, Catalogo Medicamento Nuevo, Homologacion de medicamento, Medicamentos (Facturacion) (+2 more)

### Community 8 - "Informes e indicadores"
Cohesion: 0.33
Nodes (7): CUPS, Estado de cita, Indicador con estandar y unidad, Panel de Informes (INFORMES), Prestador de servicio (sedes PRORED), Reporte Citas Medicas, Informe Resolucion 256

### Community 9 - "Afinamientos y preingresos"
Cohesion: 0.50
Nodes (4): Afinamientos, Agenda afinamiento (enfermeria), Agenda de cronicos, Preingresos

### Community 10 - "Turnero atencion al usuario"
Cohesion: 1.00
Nodes (3): Agenda Consultas Terminadas (turnero), Atencion al Usuario (turnero servicios), Puesto y asesor (turnero)

## Knowledge Gaps
- **64 isolated node(s):** `Diagnóstico (CIE10)`, `Adjunto`, `Visado de autorización`, `Estados de urgencias`, `Estado de recepción de autorización` (+59 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **7 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Cita médica unificada` connect `Agendamiento y demanda inducida` to `Facturacion contratos y caja`, `Citas autorizaciones y pacientes`, `Seguridad roles y funcionarios`?**
  _High betweenness centrality (0.105) - this node is a cross-community bridge._
- **Why does `Cita` connect `Citas autorizaciones y pacientes` to `Facturacion contratos y caja`, `Agendamiento y demanda inducida`?**
  _High betweenness centrality (0.085) - this node is a cross-community bridge._
- **Why does `Farmacia (panel regente)` connect `Inventario y abastecimiento` to `Ingreso y atencion clinica`, `Pedidos internos y enfermeria`?**
  _High betweenness centrality (0.058) - this node is a cross-community bridge._
- **Are the 4 inferred relationships involving `Cita médica unificada` (e.g. with `Diseñador de consentimientos` and `OLD Asignación cita médica`) actually correct?**
  _`Cita médica unificada` has 4 INFERRED edges - model-reasoned connections that need verification._
- **Are the 2 inferred relationships involving `Facturador manual V2` (e.g. with `Manual tarifario ISS/SOAT` and `Notas débito`) actually correct?**
  _`Facturador manual V2` has 2 INFERRED edges - model-reasoned connections that need verification._
- **Are the 2 inferred relationships involving `Historia clinica consulta externa` (e.g. with `Farmacia (panel regente)` and `Agenda medica (consulta externa)`) actually correct?**
  _`Historia clinica consulta externa` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Diagnóstico (CIE10)`, `Adjunto`, `Visado de autorización` to the rest of the system?**
  _64 weakly-connected nodes found - possible documentation gaps or missing edges._