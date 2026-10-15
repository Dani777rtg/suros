# Arquitectura propuesta (supuesto)

Ejercicio, no decisión. Propone cómo reconstruir SUROS para una IPS como PRORED, usando lo documentado y las skills de ECC:
- `architect`, `hexagonal-architecture` y `architecture-decision-records`;
- `healthcare-emr-patterns`, `healthcare-phi-compliance` y `healthcare-cdss-patterns`;
- `postgres-patterns`, `database-migrations` y `api-design`;
- `security-review`, `deployment-patterns` y `docker-patterns`.

## 1. Punto de partida

**Lo que hay (SUROS):**
- ASP.NET WebForms con Ext.NET, en 7 sub-aplicaciones, unas 125 pantallas y unas 1.450 funciones JavaScript.
- Las reglas de negocio están repartidas entre el cliente y el servidor.

**Escala medida:**
- Unos 7.500 pacientes y 75 contratos.
- Varias sedes, que probablemente son varias empresas del mismo grupo.
- Decenas de usuarios.
- No es un problema de escala, es un problema de **orden, seguridad y cumplimiento normativo**.

**Problemas de seguridad observados:**

| # | Hallazgo | Regla ECC que incumple |
|---|---|---|
| S1 | Todo por HTTP sin cifrar, login incluido | `security-review`: TLS obligatorio |
| S2 | Cinco agendas guardan datos de pacientes en `localStorage` (modo sin conexión) y el familiograma también | `healthcare-phi-compliance`: "Never store PHI in localStorage" |
| S3 | No se ve registro de quién consulta cada historia clínica | `healthcare-phi-compliance`: auditoría de todo acceso a PHI |
| S4 | Reglas y cálculos clínicos en el cliente; por ejemplo, la saturación vacía se guarda como 95 | `healthcare-emr-patterns`: "Could this harm a patient?", sin valores silenciosos |
| S5 | Borrado sin confirmación en la bitácora, y permisos que se deciden en el servidor sin una matriz visible | Mínimo privilegio y auditoría |
| S6 | Código de prueba accesible en producción (`CargarTestSV`) | `production-audit` |
| S7 | Credenciales de terceros (SISPRO) guardadas por el sistema, sin saber si cifradas | Gestor de secretos |

**Lo que exige la norma** (a verificar en las fuentes oficiales):
- RDA en HL7 FHIR R4 (Res. 1888/2025).
- RIPS en JSON con CUV (Res. 2275/2023).
- Factura electrónica DIAN.
- Historia clínica reservada, inalterable y con firma (Res. 1995/1999).
- Datos personales (Ley 1581/2012).
- Transición a CIE-11.

## 2. Opciones

### Opción A: monolito modular hexagonal (recomendada)

**Qué es:** una sola aplicación desplegable, dividida en módulos que no se mezclan entre sí. Cada módulo tiene dominio, casos de uso, puertos y adaptadores. Una sola base de datos PostgreSQL, con un esquema por módulo.

- **A favor:**
  - Es simple de operar para un equipo pequeño.
  - Las transacciones son consistentes; por ejemplo, la factura y el inventario se actualizan en la misma operación.
  - Cada integración (DIAN, RIPS, RDA) es un adaptador que se puede cambiar sin tocar las reglas.
  - Si un módulo crece, se puede separar después.
- **En contra:** exige disciplina para no cruzar fronteras entre módulos. Se controla con pruebas de arquitectura.

### Opción B: microservicios

- **A favor:** escalado y despliegue independientes.
- **En contra:**
  - Escala innecesaria para 7.500 pacientes.
  - Cuesta más operarlo: red, observabilidad, consistencia distribuida.
  - Más superficie de ataque.
- **Veredicto:** descartada. ECC lo marca como *premature optimization*.

### Opción C: comprar o adaptar en vez de construir

- **Software colombiano en la nube** (Saludtools, Medifolios y similares):
  - **A favor:** ya cumplen RIPS, DIAN y RDA.
  - **En contra:** pierdes las reglas propias (malla de reumatología, PyP, BOT) y quedas atado al proveedor.
- **Código abierto** (OpenEMR, OpenMRS, ERPNext Healthcare):
  - **A favor:** base madura.
  - **En contra:** hay que adaptarlo a toda la norma colombiana. Es mucho trabajo y no siempre ahorra.
- **Veredicto:** es la opción más barata si PRORED solo necesita lo estándar. La entrevista lo dirá.

### Opción D: modernizar SUROS por partes (*strangler fig*)

**Qué es:** el sistema nuevo (opción A) reemplaza SUROS módulo a módulo, y los dos conviven un tiempo.

- **A favor:** sin "big bang", con riesgo controlado.
- **En contra:** hay que sincronizar datos durante la convivencia.
- **Veredicto:** es **la forma de llegar** a la opción A, no una alternativa a ella.

**Recomendación: A, construida por la vía D**, siempre que la entrevista confirme reglas propias que justifiquen construir. Si no, C.

## 3. Arquitectura de la opción A

```
           Navegador (personal)        App/Portal paciente        BOT / WhatsApp
                    │ HTTPS                    │ HTTPS                  │
              ┌─────▼──────────────────────────▼────────────────────────▼─────┐
              │  Proxy / WAF  ·  TLS 1.3  ·  HSTS  ·  límite de peticiones     │
              └─────────────────────────────┬──────────────────────────────────┘
                                            │
┌───────────────────────────────────────────▼──────────────────────────────────────┐
│ API (monolito modular)  ·  autenticación OIDC + MFA  ·  permisos por rol y sede   │
│                                                                                   │
│  Pacientes │ Agenda y citas │ Atención clínica (HC) │ Órdenes (lab, imágenes)    │
│  Farmacia e inventario │ Facturación, caja y contratos │ Cartera y glosas (nuevo) │
│  Calidad: PQRS y eventos adversos (nuevo) │ Seguridad y administración            │
│                                                                                   │
│  Puertos de salida → adaptadores: DIAN · RIPS/CUV · RDA FHIR R4 · WhatsApp ·      │
│                      equipos de laboratorio (HL7 v2) · firma digital              │
└──────────┬──────────────────────────────┬─────────────────────────┬──────────────┘
           │                              │                         │
   PostgreSQL (un esquema por módulo)  Cola de salida (outbox)   Almacén de archivos
   RLS por sede · auditoría             → reintentos hacia        cifrado (adjuntos,
   solo-inserción · cifrado de columnas   DIAN/RIPS/RDA           consentimientos, PDF)
           │
   Réplica de lectura → reportes e indicadores (Res. 256, oportunidad, producción)
```

### Módulos

Salen de lo que tiene uso medido y servicios habilitados; lo no usado queda fuera hasta que se pida.

| Módulo | Contiene | Reglas clave (ECC) |
|---|---|---|
| Pacientes | Demografía, afiliación, acudiente, unificación de historias | Identificador interno opaco (UUID), nunca el documento en las URL |
| Agenda y citas | Programación, franjas, bloqueos (por IPS o por médico), canales (ventanilla, BOT, WhatsApp), activación y turnero | Duración múltiplo de 5 minutos; causa obligatoria al bloquear |
| Atención clínica | Encuentro de consulta por especialidad, diagnóstico (CIE-10 y CIE-11), fórmula, órdenes, incapacidad, firma | `healthcare-emr-patterns`: encuentro en una sola página; **firmado = bloqueado, solo adendas** |
| Seguridad clínica (CDSS) | Interacciones de medicamentos, alergias, dosis por peso, valores críticos | `healthcare-cdss-patterns`: interacción crítica **bloquea**; anularla exige un motivo que queda auditado; las pruebas no toleran falsos negativos |
| Órdenes | Laboratorio (toma de muestras, resultados), imágenes (ecografía) | Valores críticos con alerta que no se puede descartar |
| Farmacia e inventario | Catálogo CUM, lotes y vencimientos (FEFO), dispensación, pedidos internos, compras, control especial | Las reglas en el servidor, no en el navegador |
| Facturación | Contratos (evento, paquete, PGP, capitación), facturador, caja, notas, homologador, copago y cuota moderadora | El cálculo, en el dominio y probado |
| Cartera y glosas | Radicación, glosas, respuestas y conciliación | **Nuevo**: hoy no existe |
| Calidad | PQRS, encuestas, eventos adversos, indicadores | **Nuevo** |
| Seguridad y administración | Usuarios, roles, matriz de permisos explícita, sedes y parámetros | Mínimo privilegio; la matriz de permisos se puede leer y probar |

## 4. Seguridad (corrige S1–S7)

1. **Transporte (S1):** HTTPS obligatorio con TLS 1.3 y HSTS; nada por HTTP.
2. **Identidad:**
   - OIDC (Keycloak o el proveedor de la nube) con **MFA obligatorio** para personal clínico y administrativo.
   - Sesión que caduca por inactividad y re-autenticación al firmar. SUROS ya pide re-autenticación en la entrega de turno.
3. **Autorización (S5):**
   - Permisos por rol **y** por sede.
   - La sede se aplica en la base de datos con *Row-Level Security*: un médico de la sede A recibe 0 filas de la sede B (`healthcare-phi-compliance`, ejemplo 2).
   - La matriz de permisos es explícita y tiene pruebas.
4. **Auditoría (S3):**
   - Tabla de auditoría **solo de inserción**, sin permiso para editar ni borrar.
   - Registra lectura, creación, edición, impresión y exportación de toda historia clínica, con usuario, paciente, recurso, IP y sesión.
5. **Datos de pacientes en el cliente (S2):**
   - **Prohibido** guardar datos de pacientes en `localStorage`.
   - Si una sede necesita trabajar sin conexión, se resuelve en el servidor (caché de la sede con cifrado), no en el navegador. Esa necesidad se confirma en la entrevista.
6. **Datos en reposo:**
   - Disco cifrado.
   - Columnas sensibles cifradas: documento, diagnósticos de salud mental o VIH si aplica.
   - Columnas etiquetadas `PHI:` en el esquema.
   - Copias de seguridad cifradas con recuperación a un punto en el tiempo, y prueba de restauración mensual.
7. **Registros y errores:** sin datos de pacientes en logs, mensajes de error ni URL; solo identificadores opacos.
8. **Secretos (S7):** credenciales de DIAN, SISPRO y WhatsApp en un gestor de secretos (Vault o el de la nube), nunca en la base de datos en texto plano.
9. **Reglas clínicas en el servidor (S4):** nada de valores por defecto silenciosos (como saturación = 95). Las reglas viven en el dominio y tienen pruebas.
10. **Cadena de entrega (S6):**
    - Revisión de dependencias en cada cambio.
    - Escaneo SAST/DAST en CI.
    - Sin código de prueba en producción.
    - Pentest antes de salir a producción.
11. **Ley 1581:** autorización de tratamiento de datos registrada (antes de enviar por WhatsApp), derecho de consulta y política de retención.

## 5. Integraciones

Cada integración es un adaptador detrás de un puerto (`hexagonal-architecture`). El dominio emite un evento y la **cola de salida (*outbox*)** lo entrega con reintentos, sin perder nada si DIAN o el Ministerio no responden.

| Integración | Estándar | Nota |
|---|---|---|
| Factura electrónica | DIAN, mediante un proveedor tecnológico | No implementar la firma DIAN a mano |
| RIPS | JSON con CUV (validador del Ministerio) | Se genera desde la factura, no se digita |
| RDA / historia clínica interoperable | HL7 FHIR R4, perfiles colombianos | Se puede apoyar en un servidor FHIR (HAPI) como traductor |
| WhatsApp y BOT | WhatsApp Business API | Solo si hay autorización de datos |
| Laboratorio | HL7 v2 / ASTM con los equipos | Elimina la transcripción manual |
| Firma | Tabletas de firma (hoy Wacom STU) o firma digital | Al firmar, la historia queda bloqueada |

## 6. Tecnología: tres combinaciones equivalentes

Las tres sirven; se elige por el equipo que lo va a mantener.

| | .NET 8 (ASP.NET Core) | TypeScript (NestJS + Next.js) | Python (Django + DRF) |
|---|---|---|---|
| Mejor si | El equipo actual de SUROS sigue (ya es .NET) | El equipo es web/JavaScript o se construye con agentes (Shipwright/Claude) | Equipo pequeño; muchas pantallas son catálogos (CRUD) |
| ECC | `dotnet-patterns`, `csharp-testing` | `nestjs-patterns`, `nextjs-turbopack`, `api-design` | `django-patterns`, `django-security`, `django-tdd` |
| A favor | Continuidad, rendimiento, buen soporte de tipos | Un solo lenguaje en frontend y backend; tipos compartidos | Panel de administración gratis para los catálogos, seguridad por defecto, el más rápido de construir |
| En contra | Más ceremonia | Hay que elegir bien las librerías | La interfaz clínica rica igual necesita React |

Común a las tres:
- **PostgreSQL 16** (`postgres-patterns`), con RLS, esquemas por módulo y migraciones versionadas (`database-migrations`);
- **React** para las pantallas clínicas y de agenda;
- **Docker** (`docker-patterns`), CI con pruebas y escaneo, y despliegue *blue-green* (`deployment-patterns`);
- nube con contrato de transmisión de datos conforme a la Ley 1581.

**Mi elección para este caso:** TypeScript (NestJS + Next.js) si se construye con Shipwright; .NET si lo mantiene el equipo de SoftProject.

## 7. Cómo llegar (por la vía D)

1. **Base:**
   - Identidad, permisos, sedes y auditoría.
   - HTTPS ya en SUROS: es un arreglo inmediato que no depende de reconstruir nada.
2. **Pacientes, agenda y citas:** es lo más usado y lo que menos depende del resto.
3. **Atención clínica de consulta externa**, con firma, adendas y CDSS de medicamentos.
4. **Farmacia e inventario.**
5. **Facturación, RIPS, DIAN y RDA.**
6. **Cartera, glosas y calidad**, que hoy no existen.

En cada paso, el módulo nuevo reemplaza al de SUROS y se sincroniza mientras conviven. Pruebas de caracterización primero: fijar cómo se comporta hoy antes de cambiarlo.

## 8. Decisiones para registrar como ADR (`architecture-decision-records`)

| ADR | Decisión |
|---|---|
| ADR-001 | Monolito modular hexagonal frente a microservicios |
| ADR-002 | PostgreSQL con RLS por sede |
| ADR-003 | Auditoría solo de inserción de todo acceso a la historia clínica |
| ADR-004 | Historia firmada inmutable, solo adendas |
| ADR-005 | Cola de salida (*outbox*) para DIAN, RIPS y RDA |
| ADR-006 | Ningún dato de paciente en el navegador |
| ADR-007 | Stack según el equipo (sección 6) |

## Pendiente de la entrevista

Lo que puede cambiar esta propuesta:
1. **Sedes y servicios habilitados:** si urgencias, hospitalización y cirugía entran o no.
2. **Necesidad de trabajar sin conexión:** afecta la seguridad (punto 5 de la sección 4).
3. **Quién mantendrá el sistema:** decide la tecnología.
4. **Si basta con un producto del mercado:** si es así, gana la opción C.
