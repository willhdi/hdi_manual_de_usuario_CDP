# Política de Gobierno HDI ADP-DWH

| | |
| --- | --- |
| **Versión** | 1.0 |
| **Fecha de entrega** | 2024-11-18 |
| **Título** | Política de Asignación de Funciones y Gobierno de Datos |

## Objetivo

Establecer una clara separación de funciones y responsabilidades entre las áreas de BI (gobierno de datos e ingeniería de datos) y Arquitectura para asegurar una gestión eficiente y gobernanza efectiva de las bodegas de datos de la compañía (DWH Colombia y ADP).

## Áreas y Funciones

### Área de Business Intelligence (BI)

**Responsabilidades:**

- **Análisis de datos y generación de informes:** realizar análisis descriptivos, diagnósticos y prescriptivos para apoyar la toma de decisiones estratégicas y operativas de la compañía de cara a los proyectos estratégicos.
- **Desarrollo de dashboards y visualizaciones:** crear y mantener dashboards interactivos y visualizaciones que permitan a los usuarios finales explorar y entender los datos de manera intuitiva.
- **Identificación de tendencias y patrones:** utilizar técnicas de minería de datos y análisis estadístico para identificar tendencias, patrones y anomalías en los datos.

**Interacción con otras áreas:**

- **Arquitectura de Datos:** coordinar las actividades necesarias para asegurar que los modelos de datos y las estructuras de la bodega de datos estén alineados con los estándares y mejores prácticas.

### Área de Ingeniería de Datos BI

**Responsabilidades:**

- **Diseño, construcción y mantenimiento de pipelines de datos:** desarrollar y mantener procesos automatizados para la extracción, transformación y carga (ETL) de datos desde diversas fuentes hacia la bodega de datos.
- **Integración de datos desde diversas fuentes:** asegurar la integración de datos provenientes de sistemas internos y externos, garantizando la consistencia y calidad de los datos.
- **Optimización del rendimiento de la bodega de datos:** implementar técnicas de optimización para mejorar el rendimiento de las consultas y la eficiencia del almacenamiento de datos.

**Interacción con otras áreas:**

- **Gobierno de Datos:** colaborar para asegurar que los datos utilizados en los análisis cumplan con los estándares de calidad y conformidad.
- **Arquitectura de Datos:** coordinar las actividades necesarias para asegurar que los modelos de datos y las estructuras de la bodega de datos estén alineados con los estándares y mejores prácticas.

### Área de Gobierno de Datos

**Responsabilidades:**

- **Definición y mantenimiento de políticas de calidad de datos:** establecer políticas y procedimientos para asegurar la precisión, integridad, consistencia y actualidad de los datos.
- **Monitoreo y aseguramiento de la conformidad:** supervisar el cumplimiento de las políticas de datos y las regulaciones aplicables, y tomar medidas correctivas cuando sea necesario.
- **Gestión de metadatos y linaje de datos:** mantener un catálogo de metadatos que describa las fuentes, transformaciones y destinos de los datos, facilitando la trazabilidad y el linaje de los datos.

**Interacción con otras áreas:**

- **Ingeniería de Datos (dentro de BI):** trabajar juntos para implementar controles de calidad de datos en los procesos ETL.
- **BI:** asegurar que los datos utilizados en los análisis cumplan con los estándares de calidad y conformidad.

### Área de Arquitectura de Datos

**Responsabilidades:**

- **Definición de la arquitectura de datos y modelos de datos:** diseñar la arquitectura de datos que soporte las necesidades de la organización, incluyendo modelos de datos conceptuales, lógicos y físicos.
- **Establecimiento de estándares y mejores prácticas:** desarrollar y mantener estándares y mejores prácticas para la gestión de datos, incluyendo nomenclatura, modelado y documentación.
- **Evaluación y selección de tecnologías y herramientas:** evaluar y seleccionar las tecnologías y herramientas adecuadas para la gestión y análisis de datos, asegurando su alineación con la estrategia de datos de la organización.

**Interacción con otras áreas:**

- **Ingeniería de Datos (dentro de BI):** asegurar que la implementación de la arquitectura de datos esté alineada con los estándares y modelos definidos.
- **Gobierno de Datos:** colaborar para asegurar que la arquitectura de datos soporte las políticas de calidad y gobernanza de datos.

## Gobierno de Datos

**Principios:**

- **Transparencia:** todas las áreas deben tener visibilidad sobre las políticas y procedimientos de gestión de datos, promoviendo una cultura de transparencia y confianza.
- **Responsabilidad:** cada área es responsable de sus funciones específicas y debe rendir cuentas sobre el cumplimiento de sus responsabilidades, asegurando la integridad y calidad de los datos.
- **Colaboración:** fomentar la colaboración entre las áreas para asegurar una gestión de datos coherente y eficiente, aprovechando las sinergias y compartiendo conocimientos.

**Estructura de gobierno:**

- **Comité de Gobierno de Datos:** formado por representantes de cada área, responsable de la supervisión y revisión de las políticas de datos, así como de la resolución de conflictos y la toma de decisiones estratégicas.
- **Roles y responsabilidades:** definir roles claros como Data Stewards (responsables de la calidad y gestión de datos en áreas específicas), Data Owners (propietarios de los datos y responsables de su uso y protección) y Data Custodians (encargados de la administración técnica de los datos).

## Revisión y Actualización

- **Frecuencia:** la política debe ser revisada y actualizada al menos una vez al año o cuando se produzcan cambios significativos en la organización o en las regulaciones.
- **Proceso:** el Comité de Gobierno de Datos es responsable de la revisión y actualización de la política, con la participación de todas las áreas involucradas. Este proceso incluye la evaluación de la efectividad de las políticas actuales, la identificación de áreas de mejora y la implementación de cambios necesarios.

## Flujo de Trabajo para una Nueva Solicitud de Datos

| # | Etapa | Responsable | Descripción |
| --- | --- | --- | --- |
| 1 | Recepción de la solicitud | Solicitante (usuario de negocio) | El usuario de negocio identifica una necesidad de datos y envía una solicitud formal a través del sistema de gestión de solicitudes. |
| 2 | Evaluación inicial | Equipo de Gobierno de Datos | Revisa la solicitud para asegurar que cumple con las políticas y normativas establecidas; verifica la disponibilidad de los datos y la conformidad con las regulaciones de privacidad y seguridad. |
| 3 | Diseño de la solución | Arquitectos de Datos | Analizan la solicitud y diseñan una solución técnica que cumpla con los requisitos del usuario; definen la arquitectura de datos necesaria, incluyendo tecnologías e infraestructura. |
| 4 | Desarrollo e integración | Equipo de Ingeniería de Datos | Implementa la solución diseñada; desarrolla y configura los procesos ETL para obtener, transformar y cargar los datos; asegura almacenamiento eficiente y accesible. |
| 5 | Control de calidad | Equipo de Gobierno de Datos | Realiza controles de calidad, auditorías y pruebas para verificar la precisión y consistencia de los datos frente a los estándares y normativas. |
| 6 | Entrega de datos | Equipo de Ingeniería de Datos | Una vez superados los controles de calidad, entrega los datos al usuario de negocio y proporciona acceso a través de las plataformas y herramientas adecuadas. |
| 7 | Monitoreo y soporte | Equipo de Ingeniería de Datos / Gobierno de Datos | Ingeniería monitorea el rendimiento y la disponibilidad de los sistemas; Gobierno continúa monitoreando la calidad y el cumplimiento normativo. |
| 8 | Revisión y retroalimentación | Solicitante / Gobierno de Datos / Ingeniería de Datos | El usuario revisa los datos entregados y da retroalimentación sobre su utilidad y precisión; los equipos ajustan lo necesario para mejorar futuros procesos. |
