# Proyectos - Contenido para CV de la empresa

Documento de trabajo: acá vamos acumulando el contenido de cada proyecto antes de armar el CV final (PDF/web/lo que se defina).

---

## Capacidades de la empresa

Sección transversal (no ligada a un proyecto puntual), pensada como página de "quiénes somos" del portfolio.

| Capacidad | Descripción |
|---|---|
| Arquitectura de Datos | Diseño de plataformas analíticas, arquitecturas por capas (Medallion) y repositorios centralizados |
| Ingeniería de Datos | Ingesta, transformación, normalización y construcción de flujos ETL/ELT |
| Integración de Sistemas | Diseño de interfaces y APIs para conectar sistemas internos y desacoplar consumidores |
| Análisis Funcional y Diagnóstico | Relevamiento de sistemas y flujos de negocio existentes para identificar mejoras, cuellos de botella y puntos de dolor |
| Gobierno y Trazabilidad | Catalogación, metadata, lineage, controles de calidad y consistencia |
| QA y Validación | Validación de datos, de la lógica funcional y de la consistencia de los procesos implementados |
| Analítica | Modelado y construcción de Data Marts preparados para tableros y explotación de negocio |
| Evolución de Plataformas | Incorporación de nuevos dominios y adaptación a ecosistemas tecnológicos existentes |

**Cómo trabajamos:** Entender → Diseñar → Implementar → Validar → Evolucionar. La metodología se adapta al contexto de cada organización: relevamiento de la situación existente (incluyendo análisis funcional y diagnóstico), diseño de una solución viable, implementación incremental, validación de calidad de datos y lógica funcional, y evolución sostenida.

---

## Proyecto 1: Repositorio Único de Datos - Grupo Petersen

**Cliente:** Grupo Petersen (entidades bancarias del grupo)
**Bancos involucrados:** Banco Entre Ríos, Banco San Juan, Banco Santa Fe, Banco Santa Cruz
**Duración:** ~2 años
**Rol de Helios System:** Mantenimiento y evolución de una plataforma de datos ya en marcha al momento de incorporarnos al proyecto

### Descripción

Helios System se incorporó a un proyecto de Repositorio Único de Datos ya en funcionamiento para el Grupo Petersen, adaptándose a las herramientas y procesos existentes para dar continuidad y evolucionar la plataforma. El trabajo consistía en generar nuevos **subdominios de datos** por cada producto bancario (tarjetas de crédito, clientes, préstamos, entre otros), integrando información de múltiples entidades del grupo (Banco Entre Ríos, Banco San Juan, Banco Santa Fe y Banco Santa Cruz).

El proceso general era: ingesta de datos crudos desde los sistemas transaccionales de cada banco → proceso de **ETL** → generación de un **datamart** por dominio, que cada banco luego utilizaba como base para construir sus propios dashboards de negocio para distintos sectores/áreas.

El esfuerzo de cada subdominio variaba en complejidad y magnitud según el producto bancario a modelar.

### Arquitectura de datos

Plataforma Big Data (Cloudera / ecosistema Hadoop) organizada en zonas bajo un enfoque tipo **Medallion** (patrón de arquitectura de datos ampliamente adoptado en la industria), sobre datos ingestados desde las 4 entidades del grupo (BER, BSC, BSJ, BSF):

**Fuentes → Ingesta → Landing → Zona Cruda (RAW) → Zona Curada → Zona Refinada / Consumo (Datamart) → Decisiones**

- **Landing:** recepción de archivos crudos enviados por cada banco
- **Zona Cruda (RAW):** primera estructuración en HDFS — modelado, limpieza y estandarización inicial (todos los campos como STRING)
- **Zona Curada:** aplicación de reglas de negocio, tipado y normalización de campos, resolviendo casos de uso concretos
- **Zona Refinada / Consumo:** datamarts finales, organizados según la necesidad de cada área de negocio del banco, usados para construir sus dashboards

Todo el proceso estaba estandarizado mediante un flujo repetible (diseño técnico → creación de tabla RAW → creación de tabla Curada → query de ingesta RAW→Curado → alta del término de gobierno en Atlas → validación de carga), con convenciones estrictas de nomenclatura, tipado y particionado por fecha de proceso.

### Stack técnico

- **Hadoop / Cloudera** — plataforma Big Data distribuida (HDFS como almacenamiento base)
- **Hive** — data warehouse sobre Hadoop, lectura/escritura/gestión de grandes volúmenes de datos vía SQL (HiveQL)
- **Impala** — motor de consultas SQL de baja latencia sobre HDFS/HBase, usado para las consultas analíticas que alimentaban los dashboards
- **Cloudera Hue** — interfaz web para interactuar con el clúster (ejecución de queries, creación de tablas)
- **Apache Kudu** — almacenamiento orientado a datos en tiempo real dentro del ecosistema Hadoop
- **Apache Spark** — procesamiento distribuido de datos dentro del proceso ETL
- **Apache NiFi** — automatización e integración de flujos de datos; microservicio que detecta y levanta automáticamente los archivos entrantes
- **Apache Kafka** — mensajería y disparadores (triggers) de procesos en tiempo real
- **Apache Atlas** — gobierno de datos y gestión de metadata: catalogación de cada fuente ingestada mediante "terms" (glosario), con clasificación, encoding, patrón de archivo y trazabilidad de las queries de transformación
- **FileZilla / WinSCP / PuTTY** — transferencia segura de archivos (SFTP) y administración remota (SSH) entre los servidores de cada entidad y los entornos de desarrollo/producción
- **FortiClient VPN** — conectividad segura a los entornos de los bancos
- **Elastic Stack** — búsqueda, monitoreo y análisis en tiempo real dentro de la plataforma

### Valor entregado

Continuidad y evolución de una plataforma crítica de datos multi-entidad, incorporando nuevos dominios de información bancaria (tarjetas de crédito, clientes, préstamos) de forma sostenida durante 2 años, dando soporte a 4 bancos del grupo con datamarts confiables y gobernados (trazabilidad end-to-end vía Atlas) para la construcción de reportes y dashboards de negocio.

---

## Pendiente para completar este proyecto (opcional)

- [ ] ¿Cuántas personas de Helios System conformaban el equipo?
- [ ] ¿Hay capturas de pantalla, diagramas de arquitectura o dashboards (sin datos sensibles) que se puedan usar como material visual?
- [ ] ¿El proyecto sigue activo hoy o ya finalizó? (fecha de cierre si aplica)

---

## Proyecto 2: Integración de Datos y APIs para Originación de Préstamos

**Cliente:** Unazul (Grupo Petersen) / Servicios financieros
**Fuente:** documento "Antecedentes de proyectos - GP" (genérico) + detalle aportado por el caso de QA relacionado (ver Proyecto 3)

### Objetivo

Construir un repositorio central de datos e integrar, vía APIs, la base de datos interna con el frontend de solicitud de préstamos y con bureaus de crédito externos, para poder calcular y ofrecer una oferta crediticia a cada solicitante.

### Enfoque de solución

- Centralización de información proveniente de diferentes sistemas internos
- Diseño de un repositorio de datos común para reducir la dispersión de información
- Desarrollo de una **API** (equipo de desarrollo de Helios System) que conecta la base de datos interna, el frontend de solicitud de préstamos y los bureaus de crédito externos
- Definición de interfaces de consulta e intercambio de información entre componentes
- Organización de la información para facilitar su reutilización por distintos procesos y consumidores (incluyendo el cálculo de la oferta crediticia)

### Flujo

**Base de datos interna + Bureaus de crédito externos → API de integración (Helios) → Repositorio Central (datos consolidados) → Frontend de solicitud de préstamos (cálculo de oferta)**

### Valor entregado

Se estableció una capa central de información e integración que permitió calcular y presentar de forma consistente la oferta crediticia a cada solicitante, conectando de forma desacoplada la base de datos interna, el frontend y los bureaus de crédito externos.

### Pendiente para completar este proyecto

- [ ] Período de ejecución y duración
- [ ] Equipo y roles asignados por Helios System
- [ ] Tecnologías utilizadas (motor de base de datos, tecnología de la API, etc.)
- [ ] Bureaus de crédito concretos integrados
- [ ] Volumen de datos / solicitudes procesadas aproximado
- [ ] Resultados medibles o beneficios concretos obtenidos

---

## Proyecto 3: Validación Funcional y de Datos en el Flujo de Otorgación de Préstamos (QA)

**Cliente:** Unazul (Grupo Petersen) / Servicios financieros
**Relación:** validaba el mismo flujo de originación de préstamos habilitado por la API del Proyecto 2

### Objetivo

Garantizar la calidad del frontend y de la lógica que determinaba la oferta crediticia presentada a cada solicitante.

### Enfoque de solución (rol de QA)

- Validación funcional del frontend de solicitud de préstamos, cubriendo los distintos flujos y casos de uso del solicitante
- Verificación de la integración con la API que conectaba la base de datos interna, el frontend y los bureaus de crédito externos
- Validación de los datos recibidos desde los bureaus de crédito y su correcto procesamiento dentro del flujo
- Verificación de la lógica de cálculo de la oferta: montos, condiciones y demás variables brindadas al solicitante
- Detección y reporte de inconsistencias entre los datos de entrada, la lógica de negocio y lo mostrado en el frontend

### Valor entregado

Un flujo de otorgación de préstamos validado de punta a punta —frontend, API y fuentes externas de crédito— asegurando que la oferta presentada a cada solicitante fuera consistente y confiable.

### Pendiente para completar este proyecto

- [ ] Período de ejecución y duración
- [ ] Equipo y roles asignados por Helios System
- [ ] Herramientas de testing/QA utilizadas
- [ ] Resultados medibles (bugs detectados, cobertura de casos, etc.)

---

## Próximo proyecto

_(esperando el detalle del cuarto proyecto, si aplica)_
