# Política de uso y mantenimiento de Sandbox CDP

| | |
| --- | --- |
| **Versión** | 1.1 |
| **Título** | Política de administración, uso y acceso CDP |
| **País** | Colombia |
| **Área** | Estrategia y Transformación — Gestión de Datos y Analítica |
| **Fecha** | 09/02/2026 |

## Objetivo

En este documento se definen las políticas de gobierno para los esquemas Sandbox y también el proceso de traspaso de tablas o vistas a los esquemas oficiales de Data Program.

## Alcance

Esta política aplica a todos los esquemas Sandbox que existen y a los futuros que sean creados.

### Aplicabilidad

1. **Unidades de Negocio y Departamentos:** aplicable a todas las unidades de negocio y departamentos que utilicen Amazon Redshift como parte de sus operaciones diarias y toma de decisiones. Incluye la ingesta, almacenamiento, procesamiento y análisis de datos.
2. **Herramientas y Tecnologías:** cubre el uso de Amazon Redshift y sus componentes asociados para la consulta de datos no estructurados almacenados en Amazon S3, SageMaker en entornos de prueba y gestores de bases de datos como SQL Server.
3. **Roles y Responsabilidades:** define los roles y responsabilidades de los propietarios de datos, administradores de ambientes de prueba, analistas de datos y otros usuarios clave en la gestión y uso del Sandbox - CDP.
4. **Procesos y Procedimientos:** establece los procesos y procedimientos para la ingesta, almacenamiento, procesamiento y análisis de datos en ambientes de prueba del CDP. Incluye la validación y limpieza de datos, así como la implementación de medidas de seguridad y cumplimiento normativo.
5. **Mejores Prácticas:** abarca las mejores prácticas para garantizar la seguridad, precisión y cumplimiento normativo en el manejo de la información:
   - **Seguridad de los Datos:** implementación de controles de acceso basados en roles (RBAC), cifrado de datos en tránsito y en reposo, y monitoreo continuo para detectar y responder a incidentes de seguridad.
   - **Calidad de los Datos:** procesos de validación y limpieza de datos, uso de herramientas de calidad de datos y monitoreo continuo de la calidad de los datos.
   - **Cumplimiento Normativo:** asegurar el cumplimiento con regulaciones relevantes, incluido el tratamiento de datos personales.
6. **Futuras Implementaciones:** la política también se extiende a cualquier futura implementación de Amazon Redshift en nuevos proyectos o áreas de la organización que requieran del uso de ambientes de prueba en CDP, asegurando un marco unificado de gobernanza y mejores prácticas para todos los usuarios.

## Definición entorno Sandbox

El esquema Sandbox es un entorno dentro de las bases de datos con propósitos analíticos en la compañía. Su propósito es la exploración y validación de datos dentro de un ambiente de producción; también se utiliza para experimentar soluciones de datos antes de ser publicadas en esquemas oficiales. Una vez que estos desarrollos estén maduros y validados, se deben traspasar a los entornos oficiales y eliminar del ambiente Sandbox.

### Esquemas y accesos

**Esquema Sandbox en Data Program:**

- **`CO_Sandbox_Datos`:** para usuarios de Colombia de la VP de Datos, Pricing y áreas de negocio que necesiten desarrollar soluciones de datos. El acceso es restringido y debe ser autorizado por los líderes de cada área y tramitado a través del Jira de la gerencia de datos.

**Esquema Sandbox en DWH:**

- **`Liberty_Pruebas_Actuaria`:** para usuarios de Colombia de la VP de Datos, Pricing y áreas de negocio que necesiten desarrollar soluciones de datos. El acceso es restringido y debe ser autorizado por los líderes de cada área y tramitado a través del Jira de gestión de usuarios.

Para solicitar acceso, se debe radicar un Jira en el proyecto de la gerencia de datos ([Gerencia de datos DATAHUB - Jira Service Management](https://hdiseguroscol.atlassian.net/servicedesk/customer/portal/14)), por la opción **Solicitud de acceso a productos de datos**.

### Propiedad y administración de Sandbox Data Program

La administración y propiedad del entorno Sandbox está a cargo del director del área de Ingeniería de Datos — Javier Gualdrón.

### Auditoría

El control y monitoreo del esquema Sandbox se realiza a través de una tabla de auditoría que contiene datos sobre las propiedades básicas de los objetos que se creen en el Sandbox (fecha de creación, última actualización, tamaño, entre otros).

**Nombre de la tabla:** `vw_sandbox_audit`

| Campo | Detalle |
| --- | --- |
| `object_name` | Nombre del objeto |
| `object_owner` | Propietario del objeto |
| `object_size_in_gb` | Tamaño del objeto |
| `creation_date` | Fecha de creación |
| `creation_status` | Indica si lleva más de 9 meses de ser creado |
| `date_last_use` | Último uso del objeto |
| `usage_status` | Estado de uso |
| `audit_date` | Fecha de auditoría |

### Eliminación de objetos no utilizados

Existen diferentes criterios para eliminar los objetos del Sandbox, con el objetivo de que el esquema funcione de la mejor manera posible, liberando las capacidades usadas en objetos obsoletos o que deben estar en esquemas productivos por sus propiedades. Los criterios aplicables son:

**Esquema Sandbox en Data Program:**

1. Los objetos que no sean consultados o utilizados por más de **90 días** serán eliminados automáticamente del esquema Sandbox, dado que se considera que el desarrollo ha quedado obsoleto o en pausa.
2. Los objetos que sobrepasen los **270 días** desde su fecha de creación serán eliminados, ya que el entorno Sandbox es exclusivamente para la validación y pruebas de soluciones de datos; las tablas que sobrepasen este tiempo siendo consumidas desde este recurso se deben considerar productivas y deben ser movidas a los esquemas correctos.

**Esquema Sandbox en DWH:**

1. Los objetos que no sean consultados o utilizados por más de **90 días** serán eliminados automáticamente del esquema Sandbox, dado que se considera que el desarrollo ha quedado obsoleto o en pausa.

> ***Esta auditoría y posterior eliminación se realizará el segundo lunes de cada mes.***

### Almacenamiento de scripts de objetos

Es responsabilidad de cada usuario almacenar en sus archivos personales los scripts de creación, modificación, llenado de tablas y creación de procesos (procedimientos o funciones). En la eventualidad de que se borre el objeto por no uso, el usuario podrá recrear sus objetos y conservar el modelo que lo originó.

### Privilegios esquemas Sandbox

En esta sección se definen los privilegios existentes en el esquema Sandbox y los perfiles a los cuales se otorgan:

| Objeto | Privilegio | Perfil |
| --- | --- | --- |
| Tablas, procedimientos y funciones | Creación | Todos los usuarios (*) |
| Tablas | Consulta | Todos los usuarios tienen acceso a consultar sus tablas creadas y otras tablas creadas por otros usuarios |
| Tablas, procedimientos y funciones | Borrado | Owner |
| Tablas | Modificar columnas | Owner |
| Tablas | Agregar columnas | Owner |
| Tablas | Eliminar columnas | Owner |
| Procedimientos y funciones | Ejecución | Owner |
| Procedimientos y funciones | Modificar | Owner |
| Tablas | Crear tablas utilizando tablas de otros owners | Todos los usuarios (*) |

> **Todos los usuarios (*):** son todos los usuarios que tengan acceso a Sandbox.

### Solicitud de privilegios a esquemas Sandbox

Si un usuario requiere privilegios de ejecución sobre un procedimiento o función del cual no es dueño, deberá cursar una solicitud de privilegios de ejecución. El usuario, con autorización del propietario de la data, debe cursar la solicitud a través del Jira de la gerencia de datos indicando:

- Nombre de función o procedimiento.
- Aprobador de la solicitud (corresponde al dueño del procedimiento o función; en caso de que esté fuera de la oficina, el aprobador es el líder de área o el coordinador de Gobierno de Datos).
- Nombre de la tabla.

## Traspaso de vista/tabla desde Sandbox a esquema oficial

### 1. Estandarización de nombres de vistas y columnas en esquema oficial

En los esquemas oficiales de Data Program existen reglas para crear los nombres de tablas/vistas y columnas. Por lo tanto, cada vez que se requiera traspasar una vista o tabla desde el Sandbox a un esquema oficial, se debe cumplir con la estandarización siguiente:

**a) Nombres de columnas**

| Tipo | Formato | Ejemplo |
| --- | --- | --- |
| Llave dimensión | `dim_xxx_key` | `dim_broker_key` |
| Llave tabla de hechos | `fact_xxx_key` | `fact_reinsurer_key` |
| Rut / ID | `xxx_rut` | `insured_rut` |
| Nombres | `xxx_name` | `insured_name` |
| Tipos | `xxx_type` | `policy_holder_type` |
| Códigos | `xxx_code` | `lob_code` |
| Años | `xxx_year` | `contract_year` |
| Números | `xxx_number` | `policy_number` |
| Fechas | `xxx_date` | `contab_date` |
| Columnas únicas y muy conocidas en el negocio | *same as database* | `SSEGURO` |

**b) Nombres de vistas**

La nomenclatura para las vistas es la siguiente:

- **`fact_nombre_vista_sv`:**
  - `fact`: define una tabla de hechos.
  - `nombre_vista`: nombre representativo que se otorga a la vista.
  - `s`: define que corresponde a una vista segura.
  - `v`: define una vista.
- **`dim_nombre_vista_v`:**
  - `dim`: define una dimensión.
  - `nombre_vista`: nombre representativo que se otorga a la vista.
  - `v`: define una vista.

La ausencia de la letra `s` indica que es una vista que no contiene un dato confidencial.

### 2. Proceso de traspaso de Sandbox a esquema oficial

El Sandbox está definido como esquema de uso temporal, que permite la exploración de datos. Una vez que la tabla creada por el usuario está validada y requiere un uso constante (por ejemplo, para un reporte), es necesario y obligatorio traspasar esta tabla/vista a un esquema oficial de Data Program. Para ello se deben cumplir los siguientes requisitos:

**a) Definir esquema destino.** Se debe definir el esquema al cual serán traspasadas las vistas (esquema de vistas seguras y esquema de vistas no seguras, en español e inglés). En ADP se cuenta con los siguientes esquemas oficiales para el traspaso:

- **`gde_adp_dwh_vw_general`:** esquema general donde se encuentran las principales soluciones de datos en el CDP.
- **`gde_adp_dwh_vw_restricted`:** esquema general donde se encuentran las principales soluciones de datos en el CDP, con restricciones de seguridad de la información.

En caso de requerir un esquema diferente para el paso a producción, consultar con el director de ingeniería de datos.

**b) Estandarización de nombres de vista y columnas.** Se debe cumplir con la estandarización de nombres de vistas y columnas, utilizando la nomenclatura definida para los esquemas oficiales descrita en el punto anterior.

**c) Frecuencia de ejecución.** Se debe definir la frecuencia de actualización de los datos desde el origen, que puede ser:

- Diaria
- Semanal
- Mensual

**d) Query para creación de vista.** Se debe incorporar la query con la cual se va a obtener la información para poblar la vista en el esquema oficial. Tenga en cuenta las mejores prácticas para el desarrollo de productos de datos.

**e) Validaciones de calidad.** El equipo de datos realiza una revisión de las queries compartidas por el desarrollador para asegurar que cumplan con requisitos mínimos de calidad, especialmente en el diseño de las consultas, para evitar usos indebidos de la capacidad de la herramienta.

Una vez que el usuario cumpla con todo lo requerido, deberá radicar un Jira en el proyecto de la gerencia de datos ([Gerencia de datos DATAHUB - Jira Service Management](https://hdiseguroscol.atlassian.net/servicedesk/customer/portal/14)), bajo las opciones **Solicitud de mejora → Optimización de procesos de producción de datos**, titulado *"Traspaso vistas desde esquema Sandbox (indicar el esquema correspondiente) a esquema Oficial"*, indicando que se ha cumplido con todos los requisitos y adjuntando:

- Nombre(s) de esquema(s) destino.
- Nombres de vistas y columnas estandarizadas (español e inglés).
- Periodicidad de ejecución.
- Query para crear la(s) vista(s).

## Responsabilidades

- **Administrador del Entorno Sandbox (Director de Ingeniería de Datos):** responsable de gestionar el proceso de transición de las soluciones desarrolladas y certificadas en el entorno Sandbox hacia el entorno de producción. Además, debe garantizar el uso adecuado del entorno de pruebas, asegurándose de que se cumplan las políticas establecidas.
- **Gobierno de Datos:** encargado de establecer las pautas mínimas para el uso eficiente y seguro de la herramienta Sandbox. También debe realizar un monitoreo continuo para verificar el cumplimiento de dichas pautas.
- **Usuarios del Entorno Sandbox (Desarrolladores):** deben familiarizarse con las políticas aplicables al uso del entorno Sandbox y seguir estrictamente los lineamientos definidos. Esto garantiza un entorno de pruebas optimizado y funcional para todos los usuarios.

## Normativa interna asociada a la Política

- Metodología de desarrollo de productos de datos — [Política de productos de datos - Gerencia de Datos DATAHUB - Confluence HDI](https://hdiseguroscol.atlassian.net/wiki/spaces/GDDD/pages/118161679/Pol+tica+de+productos+de+datos)

# Nomenclatura de esquemas y ambientes

## Prefijo según el tipo de base

Los esquemas se nombran según el tipo de procesamiento de la base a la que pertenecen:

- **`gde_`** — prefijo para las bases y esquemas **analíticos** (procesamiento analítico, orientado a reportes, consultas y análisis). Es el caso del CDP y de los esquemas oficiales de Data Program (por ejemplo `gde_adp_dwh_vw_general` y `gde_adp_dwh_vw_restricted`).
- **`non_gde`** — prefijo para las bases y esquemas **transaccionales** (procesamiento operativo del día a día).

## Ambientes

Dentro de esta estructura existen tres ambientes:

| Ambiente | Propósito |
| --- | --- |
| **DEV** | Desarrollo. |
| **NON_PROD** | Pruebas / preproducción. |
| **PROD** | Producción. |

## Regla de pase a producción

Cada paso a producción (**PROD**) requiere:

- **Aprobación de Ingeniería de Datos.**
- **Copia a Gobierno de Datos.**

# Glosario y Términos

**Colombia Data Program (CDP):** base de datos oficial de la compañía en Amazon Redshift, fuente única de verdad para la información con propósitos analíticos de la compañía.

**Data Warehouse (DWH):** almacén de datos en SQL Server, orientado al análisis histórico y generación de reportes.

**Sandbox:** entornos aislados para pruebas y desarrollo dentro de las bases de datos oficiales de la compañía, que permiten experimentar sin afectar datos ni procesos en producción.

**`gde_`:** prefijo que identifica a las bases y esquemas **analíticos** (procesamiento analítico, orientado a análisis y reportes).

**`non_gde`:** prefijo que identifica a las bases y esquemas **transaccionales** (procesamiento operativo del día a día).

**Ambientes (DEV / NON_PROD / PROD):** las tres ramas en las que se gestionan los esquemas — desarrollo (DEV), pruebas/preproducción (NON_PROD) y producción (PROD). Todo pase a PROD requiere aprobación de Ingeniería de Datos y copia a Gobierno de Datos.
