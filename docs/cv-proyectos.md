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

### Stack técnico

- **Hive** e **Impala** — motores SQL sobre Hadoop: Hive para el procesamiento batch/ETL, Impala para consultas analíticas de baja latencia consumidas por los dashboards
- **HDFS** — almacenamiento distribuido, base de la plataforma de datos
- **Apache Spark** — transformaciones de datos dentro del proceso ETL
- **Apache NiFi** — orquestación y automatización de flujos de datos
- **Apache Kafka** — mensajería y disparadores (triggers) de procesos en tiempo real

### Valor entregado

Continuidad y evolución de una plataforma crítica de datos multi-entidad, incorporando nuevos dominios de información bancaria (tarjetas de crédito, clientes, préstamos) de forma sostenida durante 2 años, dando soporte a 4 bancos del grupo con datamarts confiables para la construcción de reportes y dashboards de negocio.

---

## Pendiente para completar este proyecto (opcional)

- [ ] ¿Cuántas personas de Helios System conformaban el equipo?
- [ ] ¿Hay capturas de pantalla, diagramas de arquitectura o dashboards (sin datos sensibles) que se puedan usar como material visual?
- [ ] ¿El proyecto sigue activo hoy o ya finalizó? (fecha de cierre si aplica)

---

## Próximo proyecto

_(esperando el detalle del segundo proyecto)_
