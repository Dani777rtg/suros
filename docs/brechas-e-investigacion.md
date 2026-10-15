# Investigación de SURÓS y brechas frente a un sistema completo

Fecha: 2026-10-14.

## Qué se encontró en internet

- **SURÓS / SoftProject:** no tienen presencia pública indexada (ni sitio comercial, ni casos, ni precios). `suros.co` no responde por HTTPS. Es probablemente un desarrollo a la medida o de nicho regional, no un producto de mercado.
- **PRORED:** en el registro de prestadores (REPS) aparece **IPS Pro Red Salud Integral S.A.S.**, NIT 901267760-4, en Pereira (Risaralda). Tiene 1 sede, 10 consultorios y 17 servicios habilitados ([fuente](https://www.cliini.ai/herramientas/consulta-reps/6600102681), datos del REPS al 2026-10-05):
  - **Consulta externa:** medicina general (también domiciliaria), medicina interna, cardiología, endocrinología, hematología, nefrología, neumología, ortopedia, **reumatología**, nutrición, psicología y enfermería.
  - **Apoyo diagnóstico:** toma de muestras de laboratorio, servicio farmacéutico, fisioterapia, terapia ocupacional e imágenes no ionizantes.
  - **No tiene habilitados** urgencias, hospitalización, observación ni cirugía.
  - Encaja con lo observado: la "Malla de reumatología", las especialidades del árbol de historia clínica y la farmacia. Pero SUROS muestra **otras sedes** (Florencia, Popayán, Pasto, Armenia, Neiva, Ibagué, Bucaramanga…) que no aparecen bajo este NIT; pueden ser otras razones sociales del mismo grupo. **Hay que confirmarlo con PRORED.**
- **Consecuencia:** si las sedes son como la de Pereira, los módulos de urgencias, hospitalización, observación y cirugía **no se usan** (no están habilitados), y con ellos caen buena parte de las preguntas abiertas de historia clínica.

## Aclaración: IPS no es EPS

PRORED es una **IPS** (presta los servicios) y SUROS es software de IPS. Una **EPS** (asegura y paga) necesita otro sistema:
- afiliación y BDUA;
- red de prestadores;
- autorizaciones emitidas;
- liquidación de la capitación y del PGP;
- auditoría de cuentas y glosas emitidas;
- recobros ante la ADRES;
- MIPRES.

Nada de eso está en SUROS. Si el objetivo fuera un sistema para EPS, el alcance es otro.

## Brechas de SURÓS frente a una IPS completa (Colombia, 2026)

Marcas usadas: **No visto** = no aparece en el menú, en las pantallas ni en el código. **Parcial** = existe pero incompleto. **Verificar** = norma que el software debe cumplir y que no se pudo comprobar.

| # | Brecha | Estado en SUROS | Por qué importa |
|---|---|---|---|
| 1 | **Cartera, radicación y glosas** ante las EPS | No visto | Es donde se cobra de verdad: radicar facturas, responder glosas y conciliar. Sin esto la IPS no recupera el dinero facturado |
| 2 | **Contabilidad, tesorería, nómina y costos** | No visto (solo centros de costo en almacén) | Normalmente vive en un ERP aparte; hay que saber cuál y cómo se integra |
| 3 | **Atención al usuario: PQRS** (peticiones, quejas, reclamos, sugerencias) y encuestas de satisfacción | Parcial (solo turnero de atención) | Lo exige la Superintendencia; es parte de habilitación y calidad |
| 4 | **Seguridad del paciente**: reporte de eventos adversos e indicadores de calidad | Parcial (existe "Informe Res. 256", eventos no visto) | Requisito del sistema obligatorio de garantía de la calidad |
| 5 | **Portal o app del paciente**: resultados, citas, fórmulas y documentos | No visto (solo el BOT de citas y WhatsApp) | Los pacientes esperan autogestión y reduce llamadas |
| 6 | **Auditoría de acceso a la historia clínica** (quién vio qué y cuándo) | No visto en la interfaz | Res. 1995/1999 y Ley 1581/2012: la historia es reservada y el acceso debe quedar registrado |
| 7 | **CIE-11** | Verificar (SUROS usa CIE-10) | Las guías del sector citan la Res. 1442/2024 para la transición a CIE-11 |
| 8 | **RDA en HL7 FHIR R4** con perfiles colombianos | Parcial (existe "Envío RDA"; formato no verificable) | Res. 1888/2025: exigible desde el 15 de abril de 2026 ([guía](https://www.saludtools.com/articulo/resolucion-1888-2025-rda-interoperabilidad-colombia)) |
| 9 | **RIPS en JSON con CUV** | Parcial (generador de RIPS y archivo CUV en factura global) | Res. 2275/2023: confirmar que valida contra el Ministerio |
| 10 | **SIIFA** | Verificar | Las guías citan la Res. 1962/2025 ([guía](https://softwaremedico.com.co/software-para-ips-en-colombia-guia-completa-de-seleccion-2026/)); confirmar en la fuente oficial |
| 11 | **Imágenes diagnósticas** (RIS/PACS, informes, visor) | No visto (solo turnos de rayos X) | PRORED tiene habilitadas imágenes no ionizantes (ecografía) |
| 12 | **Interfaz con equipos de laboratorio** (LIS) | Parcial (resultados manuales por estudio) | Evita transcribir resultados a mano |
| 13 | **Referencia y contrarreferencia** completa | Parcial (solo un reporte de remisiones) | Seguimiento de pacientes remitidos y respuesta del otro nivel |
| 14 | **Atención domiciliaria** (rutas, agenda en campo, registro sin conexión) | Parcial ("extramural" como modalidad) | Medicina general domiciliaria está habilitada |
| 15 | **Tableros gerenciales** (oportunidad de citas, inasistencia, producción por médico, facturado contra recaudado) | Parcial (informes por especialidad, no medibles) | Base para decidir y para reportar indicadores |
| 16 | **Respaldo, continuidad y seguridad técnica**: HTTPS, MFA, copias, recuperación | Riesgo visto: el sistema corre en **HTTP sin cifrar**, incluido el login | Datos de salud viajando sin cifrar; incumple buenas prácticas y la Ley 1581 |

## Recomendación

1. **Confirmar con PRORED** las sedes y los NIT del grupo, y qué servicios tiene habilitados cada sede. Eso define qué módulos de SUROS se usan; urgencias, hospitalización y cirugía podrían salir del alcance.
2. Para reconstruir el sistema, el **núcleo** es lo que tiene uso medido y servicios habilitados:
   - pacientes;
   - agenda y citas;
   - consulta externa y su historia clínica por especialidad;
   - autorizaciones;
   - facturación, caja y contratos;
   - RIPS y RDA;
   - farmacia, almacén, laboratorio (toma de muestras) y terapias.
3. Añadir lo que falta y es obligatorio o de alto valor:
   - HTTPS;
   - auditoría de acceso a la historia clínica;
   - PQRS;
   - eventos adversos;
   - cartera y glosas;
   - CIE-11;
   - RDA en FHIR.

## Fuentes

- [Consulta REPS de IPS Pro Red Salud Integral S.A.S. (cliini.ai, datos del Ministerio)](https://www.cliini.ai/herramientas/consulta-reps/6600102681)
- [Resolución 1888 de 2025: RDA e interoperabilidad (Saludtools)](https://www.saludtools.com/articulo/resolucion-1888-2025-rda-interoperabilidad-colombia)
- [Resolución 1888: guía y plazos 2026 (softwaremedico.com.co)](https://softwaremedico.com.co/resolucion-1888-guia-cumplimiento-rda/)
- [Software para IPS en Colombia: guía 2026 (softwaremedico.com.co)](https://softwaremedico.com.co/software-para-ips-en-colombia-guia-completa-de-seleccion-2026/)
- [Resolución 1888: la interoperabilidad dejó de ser opcional (Siesa)](https://www.siesa.com/blog/resolucion-1888-de-2025/)

Las fuentes de normas son guías de proveedores, no textos oficiales del Ministerio. Hay que verificar en minsalud.gov.co antes de decidir.
