# Proyectos - Contenido para CV de la empresa

Documento de trabajo: acá vamos acumulando el contenido de cada proyecto antes de armar el CV final (PDF/web/lo que se defina).

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

## Proyecto 2: Repositorio Central de Datos e Integración con Sistemas Internos

**Cliente:** Grupo Petersen (a confirmar si es la misma unidad/entidad que el Proyecto 1, o un area distinta del grupo)
**Fuente:** documento "Antecedentes de proyectos - GP" (borrador preliminar, sin datos comerciales completos)

### Objetivo

Construir un repositorio centralizado que permitiera concentrar información relevante para la operación y disponibilizarla de manera consistente a otros componentes y sistemas de la organización.

### Enfoque de solución

- Centralización de información proveniente de diferentes sistemas internos
- Diseño de un repositorio de datos común para reducir la dispersión de información
- Integración con aplicaciones y sistemas internos mediante **APIs**
- Definición de interfaces de consulta e intercambio de información entre componentes
- Organización de la información para facilitar su reutilización por distintos procesos y consumidores

### Flujo

**Sistemas internos / Fuentes operativas → Integraciones vía APIs → Repositorio Central (datos consolidados) → Servicios consumidores / Aplicaciones y procesos**

### Valor entregado

Se estableció una capa central de información e integración, facilitando que los sistemas internos pudieran intercambiar y consumir datos a través de interfaces definidas y desacopladas.

### Pendiente para completar este proyecto

Este proyecto todavía está descrito en términos genéricos (viene de un documento preliminar). Para poder armar su canvas con el mismo nivel de detalle que el Proyecto 1, falta:

- [ ] Nombre formal del proyecto y contexto/area dentro de Grupo Petersen
- [ ] Período de ejecución y duración
- [ ] Equipo y roles asignados por Helios System
- [ ] Tecnologías utilizadas (motor de base de datos, tecnología de APIs, mensajería, etc.)
- [ ] Sistemas internos concretos que se integraron, y cuántas fuentes/integraciones
- [ ] Volumen de datos aproximado
- [ ] Resultados medibles o beneficios concretos obtenidos

---

## Próximo proyecto

_(esperando el detalle del tercer proyecto, si aplica)_
