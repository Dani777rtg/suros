# Uso real (medición en producción, solo lectura)

Fecha: 2026-10-14. Método tomado de Reversa (agente "Tracer": análisis dinámico read-only para cerrar huecos) y REA (observar la aplicación en ejecución).

Por pantalla se contaron los registros que carga y, en las listas, se ejecutó solo su botón de consulta (Buscar, Consultar, Refrescar, Mostrar toda la agenda) con rango de 30 días. Se guardaron solo conteos y fechas; ningún nombre ni documento.

## Con evidencia de uso

| Área | Evidencia |
|---|---|
| Pacientes | 7.533 pacientes registrados |
| Almacén | 3.038 ajustes de inventario; 421 ítems en bodega; 287 pedidos internos; 271 líneas de plan de compra; 86 órdenes de compra; últimas órdenes y despachos 2026-09-30 |
| Contratos | 75 contratos, vigentes hasta 2027-07 |
| Turnero | consultas terminadas con fecha de hoy (2026-10-14) |
| Caja | 82 registros de apertura; 29 cierres para imprimir |
| Homologador | 98 homologaciones; 5 de procedimientos quirúrgicos |
| Farmacia | 13 solicitudes en el panel; 12 solicitudes de insumos |

## Con poco o ningún uso visible

| Pantalla | Evidencia |
|---|---|
| Notas débito | 0 en 30 días |
| Notas crédito / NC global | 1 cada una |
| Diseñador de consentimientos | 1 formato |
| Entrega de turno (médico/enfermería) | 3 registros |
| Facturación hospitalización | 4 |

## No medible con este usuario

Todas las agendas clínicas (consulta externa, urgencias, hospitalización, observación, cirugía, PyP, crónicos, afinamiento, preingreso, procedimientos) devuelven 0: filtran por el profesional que inicia sesión y el SUPER ADMINISTRADOR no es médico ni tiene especialidad. Igual para Informes. Las búsquedas de citas, facturas e ingresos devolvieron solo catálogos (sus filtros piden más que fechas).

## Conclusión

La medición confirma uso fuerte en pacientes, almacén/farmacia, contratos, caja y turnero, y uso marginal en notas débito/crédito y consentimientos. Para el resto la pregunta más barata es una sola: **¿qué módulos usa cada rol a diario?** Su respuesta descarta la mayoría de las preguntas de [preguntas-para-prored.md](preguntas-para-prored.md).
