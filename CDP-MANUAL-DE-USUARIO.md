# Manual de Usuario — Colombia Data Program (CDP)

**HDI Seguros Colombia**
Fecha de elaboración: 10/07/2026

---

## Control de versiones

| Versión | Descripción | Autor | Fecha | Revisado por |
|---------|-------------|-------|-------|--------------|
| 1.0 | Creación del manual CDP (basado en el Manual de Usuario ADP v2.1 y en la capacitación CDP del 09/07/2026) | Wilson Jerez | 10/07/2026 | — |

---

## Contenido

1. [Introducción](#1-introducción)
2. [Estructura y funcionamiento del CDP](#2-estructura-y-funcionamiento-del-cdp)
3. [Modelo de datos del CDP](#3-modelo-de-datos-del-cdp)
4. [¿Cómo usar el CDP?](#4-cómo-usar-el-cdp)
5. [Conectividad HDI (ambientes, hosts y puertos)](#5-conectividad-hdi-ambientes-hosts-y-puertos)
6. [Sandbox](#6-sandbox)
7. [Consideraciones y buenas prácticas](#7-consideraciones-y-buenas-prácticas)
8. [Soporte y documentación](#8-soporte-y-documentación)
9. [Anexo — Resumen de la Capacitación CDP (09/07/2026)](#9-anexo--resumen-de-la-capacitación-cdp-09072026)

---

## 1. Introducción

En este manual se encuentra la información necesaria para acceder al entorno de trabajo del **Colombia Data Program (CDP)**, así como su funcionamiento e implementación en actividades propias del negocio que requieran el consumo de datos para la gestión eficiente de sus operaciones.

### ¿Qué es el Colombia Data Program (CDP)?

El CDP es el repositorio oficial de datos analíticos de HDI Seguros Colombia. Es una base de datos **Amazon Redshift** desplegada sobre la plataforma **Amazon Web Services (AWS)**, cuyo objetivo es entregar datos con propósito analítico (insights, reportería, modelos) a usuarios de negocio, actuaría, pricing, modeling, distribución y otros, de manera estandarizada, estructurada y gobernada.

El CDP nace como evolución del **Andes Data Program (ADP)** construido en la época de Liberty. Tras la separación de países, el programa quedó exclusivamente con la información de **Colombia** (antes contemplaba también Chile y Ecuador). Por herencia de las directrices originales, gran parte de los esquemas, dimensiones y campos están nombrados **en inglés**.

### ¿Qué NO es el CDP?

- **No es un repositorio de datos en tiempo real ni operacional.** Los procesos de carga desde el origen se ejecutan en horario nocturno; la información tiene un delay de aproximadamente un día.
- **No debe mezclarse con el Data Warehouse tradicional (SQL).** Son infraestructuras distintas, con idiomas y diseños diferentes; no se deben hacer "injertos" entre ambos.
- **No reemplaza el consumo directo de IAxis para operación.** De hecho, se desincentiva extraer datos directamente del core, pues crea silos de información que compiten con la "fuente única de la verdad".

---

## 2. Estructura y funcionamiento del CDP

### Fuentes de datos

Las fuentes maestras de las que se alimenta el CDP son, principalmente:

- **IAxis** (core de la compañía)
- **AS400**
- Cargas manuales/mensuales (p. ej. **Guía Fasecolda**) y datos estáticos que antes vivían en archivos Excel

La columna **`source` / `core_system`** presente en las tablas indica de qué sistema origen proviene cada registro (p. ej. AS400 o IAxis).

### Arquitectura por capas (estándar medallón)

El CDP sigue las buenas prácticas de construcción de data warehouse mediante el **estándar medallón**:

1. **Capa cruda (Raw / ODS):** la información llega tal cual está en los aplicativos de origen, sin relacionar.
2. **Capa de calidad:** se aplican reglas de calidad sobre los datos.
3. **Capa productiva (Data Warehouse / Data Marts):** los datos se disponen en un **modelo estrella** optimizado para consulta y almacenamiento.

### Procesos de carga y ventanas de servicio

- La actualización del CDP se ejecuta en la noche/madrugada. Durante la ventana de carga **el servicio se corta y las queries en ejecución se cancelan automáticamente**.
- Disponibilidad actual: hasta las **10:00 p. m.** aprox. (en transición a corte a las **6:00 p. m.**, para adelantar la actualización y que las áreas comerciales tengan datos más temprano).
- Reapertura automática al terminar la carga, aproximadamente a las **5:00 a. m.**
- **Recomendación:** trabajar en las mañanas; el CDP está mucho más descargado. En horas de la tarde y en semanas de cierre contable el rendimiento se degrada.

---

## 3. Modelo de datos del CDP

El modelo de las vistas de consumo es un **modelo estrella**: de una tabla de hechos (transacciones) se desprenden tablas dimensionales que categorizan el hecho. Esto reduce la repetición de datos (a diferencia de las tablas planas del Data Warehouse antiguo), mejora el rendimiento y hace el modelo más flexible (multidimensional, tipo cubo).

### Nomenclatura

| Prefijo | Tipo de tabla | Contenido |
|---------|--------------|-----------|
| `dim_` | Dimensión | Atributos descriptivos (vehículo, conductor, asegurado, sucursal, ramo, ciudad/departamento, calendario, etc.) |
| `fact_` / `fac_` | Hechos | Movimientos transaccionales (emisión, renovación, cancelación, movimientos de siniestros y reservas, etc.) |
| `*_backup` | Respaldo | Copias de seguridad previas a cambios; **no se consumen**. El nombre de la tabla productiva nunca cambia |

### Tablas de hechos (FACT)

Toda transacción ("todo lo que mueva plata") queda registrada en una FACT: emisión de póliza, renovación, cancelación, movimientos del siniestro, reservas, etc. Entre las más relevantes:

- **Transacciones de primas** (transaction movement): solo movimientos transaccionales.
- **IMX (endosos/movimientos de póliza):** contiene **todos** los movimientos, incluidos los **no transaccionales** (p. ej. cambio de sucursal) que no aparecen en la transaccional.
- **Transacciones de siniestros (claims).**
- **Vigentes:** dos tablas según profundidad histórica — una con **28 días corridos** y otra que guarda solo la **foto del último día de cada mes**.
- **Preguntas y respuestas de IAxis:** tres FACT (preguntas del **riesgo**, del **siniestro** y de la **póliza**). Novedad frente al Data Warehouse antiguo.
- **Mills (inspecciones)** — muy solicitada para autos.
- **Cotizaciones:** auto individual y auto colectivo, con actualización frecuente de variables.
- **Policy cycles:** calcula los **ciclos de vigencia** de la póliza (IAxis solo entrega fecha inicial y final; esta tabla calcula los periodos intermedios).
- **Coaseguro/corretaje:** tabla nueva, con niveles de precisión superiores al Data Warehouse antiguo.
- **Expuestos y devengo (earned premium / `erm_premium`):** el devengo se calcula como expuesto × prima.

### Tablas de dimensiones (DIM)

Contienen las llaves de conexión (SK) y los atributos descriptivos. Dimensiones destacadas:

- **Calendario:** periodo contable, día de la semana, mes, trimestre, cuatrimestre — muy útil para tableros con temporalidad.
- **Ciudad / Departamento:** dimensión de apoyo para homologar nombres (evita inconsistencias tipo "Bogotá" / "BOGOTA" / "Santa Fe de Bogotá"); cruzar siempre por código.
- **Vehículo, conductor, asegurado, riesgo, póliza, sucursal (branch), ramo, intermediario**, entre otras.
- **Marca nuevo/renovado** (datamart de motor): certificada por pricing; lógica compleja pero funcional.

### Llaves (SK) — regla de oro

- Las tablas se cruzan mediante **llaves subrogadas dinámicas (SK)**. Son números generados por el sistema que **se mueven en el tiempo**.
- **NUNCA "quemar" (hardcodear) el valor de una SK en el código** ni usarla como filtro: si el CDP se resetea o recalcula, esas llaves cambian y la consulta deja de traer información. Solo deben usarse en el `JOIN ... ON`.
- Alternativa "colombianizada": construir **llaves lógicas** (p. ej. póliza + certificado) — funciona, pero por **rendimiento** (Redshift columnar) se recomienda cruzar por SK.

### Campo `current_record_flag`

Presente en **todas** las tablas del esquema general. `current_record_flag = 1` marca el **último registro válido/actualizado**:

- En una DIM (p. ej. vehículo): trae el estado más actual del registro (los registros históricos reflejan cambios en el tiempo — color, precio, etc.).
- En una FACT (p. ej. IMX o transaction movement): trae el último movimiento de la póliza.

### Granularidad

El nivel de granularidad de las FACT llega hasta **amparos (coberturas)**. No existe detalle a nivel de recibo. Para obtener cifras a nivel póliza basta agrupar y sumar sobre los amparos.

---

## 4. ¿Cómo usar el CDP?

### Obtener un usuario CDP

Se debe levantar un **ticket** solicitando el usuario de Redshift. Los accesos se otorgan según el perfil del usuario (permitiendo o no, por ejemplo, el acceso a datos PII). El usuario y contraseña son entregados por el equipo de administración del CDP.

> Nota: cada usuario no tiene acceso por defecto a todos los esquemas; los permisos se gestionan por perfil.

### Herramienta de conexión: DBeaver

Anteriormente se utilizaba DB Visualizer; **actualmente la herramienta estándar es DBeaver** (disponible en el portal de aplicaciones corporativo).

Pasos para crear la conexión en DBeaver:

1. `Database` → `New Database Connection`.
2. Seleccionar el tipo **Redshift** (driver JDBC Redshift).
3. Diligenciar los parámetros según el ambiente (ver [sección 5](#5-conectividad-hdi-ambientes-hosts-y-puertos)):
   - **Host:** según ambiente (Prod / Non Prod / Dev)
   - **Port:** `9519`
   - **Database:** `adp_dwh`
   - **Usuario / contraseña:** credenciales entregadas por el equipo CDP.
4. Probar la conexión (`Test Connection`) y finalizar.

DBeaver además ofrece autocompletado/predicción de variables, lo que facilita la escritura de queries.

### Conexión desde Python

```python
import getpass
import psycopg2

# CDP - Producción
username = input("Enter User Name: ")
password = getpass.getpass("Enter Password: ")

cdp = psycopg2.connect(
    dbname="adp_dwh",
    host="corshftanltc-dprogramp.hdicolombia.com.co",  # Prod
    port="9519",
    user=username,
    password=password,
)
```

> **Importante:** nunca dejar usuario/contraseña "quemados" en el código, especialmente si el desarrollo se va a productivizar. Usar `getpass`, variables de entorno o gestores de secretos.

Para los ambientes **Non Prod** o **Dev**, cambiar únicamente el `host` según la tabla de la sección 5.

---

## 5. Conectividad HDI (ambientes, hosts y puertos)

| Ambiente | Host | Puerto | Base de datos |
|----------|------|--------|---------------|
| **Producción (Prod)** | `corshftanltc-dprogramp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| **No Producción (Non Prod)** | `corshftanltc-dprogramnp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| **Desarrollo (Dev)** | `corshftanltc-dprogramd.hdicolombia.com.co` | `9519` | `adp_dwh` |

Notas:

- El puerto (`9519`) y la base de datos (`adp_dwh`) son los mismos en los tres ambientes; solo cambia el host.
- El tipo de base de datos / driver es **Amazon Redshift** en todos los casos.
- Los desarrollos y pruebas deben hacerse preferiblemente en Dev/Non Prod; Producción es para consumo de datos oficiales.

---

## 6. Sandbox

El **sandbox** es el esquema donde los usuarios pueden explorar, crear objetos (tablas, vistas) y construir sus propios desarrollos.

Reglas de uso:

- **Responsabilidad:** cada usuario es responsable de los datos que crea en el sandbox. No deben usarse como información oficial; son transitorios.
- **Permisos:** por defecto solo el creador ve sus objetos. Si otra persona necesita acceder a una tabla, el **dueño debe otorgarle el permiso** directamente.
- **Vida útil:** las tablas del sandbox se **eliminan automáticamente a los 9 meses** de creadas si no se envían a productivizar.
- **Control:** existe una tabla de control donde se puede consultar el dueño de cada objeto, el espacio ocupado (GB) y su antigüedad (el dato de "último uso" es aproximado: la auditoría de Redshift cubre 7 días y se extrae una vez al mes).
- **Espacio:** el uso del sandbox crece rápido y el espacio es limitado. Borrar tablas y backups que ya no se necesiten.

### Desarrollo colaborativo (productivización)

Las áreas de negocio pueden desarrollar vistas/consultas/productos de datos y enviarlas al equipo de ingeniería, quien las revisa (check de requerimientos mínimos), **optimiza el código** y las **productiviza** dentro de los esquemas generales. Así el desarrollo:

- No se pierde al vencer la vida útil del sandbox.
- Queda automatizado (sin depender de ejecuciones manuales).
- Cumple estándares (p. ej. no se aceptan desarrollos con datos "quemados" en el código).

---

## 7. Consideraciones y buenas prácticas

1. **Arrancar siempre desde la FACT** cuando el reporte contenga movimientos, e ir uniendo las DIM necesarias. La FACT es la que tiene conexión con todo; entre DIMs normalmente no hay camino directo.
2. **No quemar SKs ni valores dinámicos en el código.** Las llaves subrogadas cambian en el tiempo. Si se quema una SK (o una SBU, un código que puede cambiar), el desarrollo dejará de traer información sin aviso.
3. **Usar `current_record_flag = 1`** para obtener el último registro válido (última foto de una DIM, último movimiento de una póliza).
4. **Siempre usar `LIMIT`, `WHERE` o filtros** en las queries. Consultas pesadas y sin filtro pueden bloquear el CDP para todos los usuarios.
5. **No dejar queries corriendo en la noche:** el CDP se bloquea durante la ventana de carga y las consultas se cancelan automáticamente. Las consultas de larga duración también pueden ser canceladas.
6. **Preferir las mañanas** para consultas pesadas; en cierres contables el cluster está más congestionado.
7. **No mezclar CDP con el Data Warehouse SQL antiguo** ni extraer datos directamente de IAxis: se rompe la fuente única de la verdad y se crean silos.
8. **Granularidad hasta amparo:** no buscar detalle a nivel recibo.
9. **Idioma:** los objetos están mayoritariamente en inglés (herencia Liberty), con algunos elementos nuevos en español.
10. **Tablas `backup`:** ignorarlas para consumo; conectarse siempre a la tabla productiva (su nombre nunca cambia).
11. **Nuevos requerimientos:** si falta una columna/variable que existe en IAxis, se puede solicitar al equipo CDP; ellos evalúan factibilidad y prioridad ("si existe en IAxis, se puede traer").
12. **Guía Fasecolda:** se carga **mensualmente** (prerrequisito para la corrida del modelo de motor); filtrar el periodo vigente por fecha.
13. **Homologación geográfica:** cruzar ciudad/departamento por **código** usando la DIM correspondiente para evitar inconsistencias de escritura.

---

## 8. Soporte y documentación

- **Diccionario de datos:** disponible en **Confluence** (solicitar permisos de acceso mediante caso/ticket).
- **Repositorio de documentación:** existe un repositorio donde los equipos (pricing, modeling, ingeniería) documentan los cambios a los modelos. Solicitar acceso al equipo CDP.
- **Administración del CDP / infraestructura:** equipo de datos CDP (Javier Gualdron y equipo — Brayan, Esteban).
- **Problemas con DBeaver (la aplicación):** mesa de ayuda de TI.
- **Cambios y evolución:** el CDP se mejora continuamente (nuevas columnas, nuevos productos, nuevas FACT); los cambios de los dueños de los datamarts (pricing/modeling) quedan documentados.

---

## 9. Anexo — Resumen de la Capacitación CDP (09/07/2026)

> Grabación: *Capacitación CDP-20260709* — duración 59 min.
> Expositores: **Karen Andrea Carvajal Jaramillo** (generalidades y modelo) y **Javier Leonardo Gualdron Romero** (contenido, datos y práctica).
> Asistentes: Juan Andrés Carrillo León, Juan Miguel Trujillo Lavao, entre otros.

### Puntos importantes

1. **Qué es CDP:** el antiguo **ADP (Andes Data Program)** pasó a ser **CDP (Colombia Data Program)** tras la separación de países; solo contiene datos de Colombia. Es una base de datos **Redshift en AWS** con propósito **analítico** (no transaccional). Gran parte del contenido está **en inglés** por las directrices heredadas de Liberty/casa matriz.

2. **Arquitectura:** fuentes maestras = **IAxis (core)** y **AS400**. Se sigue el **estándar medallón**: capa cruda → reglas de calidad → capa productiva con **modelo estrella** (datamarts), lo que reduce costos y hace más eficientes las consultas.

3. **Modelo estrella:** tablas de **dimensiones (`dim_`)** y de **hechos (`fact_`)** conectadas por llaves. Las FACT contienen los movimientos; las DIM, los atributos (la nomenclatura permite identificar cada tabla). Existen tablas `backup` que son solo respaldos internos: **el nombre de la tabla productiva nunca cambia**.

4. **Regla práctica:** para cualquier reporte con movimientos, **arrancar desde la FACT** y unir las DIM necesarias. La FACT conecta con todo; entre dos DIM usualmente no hay camino directo.

5. **FACT destacadas:** transacciones de primas y de siniestros; **IMX** (todos los movimientos de la póliza, incluidos los **no transaccionales**, p. ej. cambio de sucursal); **vigentes** (versión 28 días corridos y versión fin de mes); **preguntas/respuestas de IAxis** (riesgo, siniestro y póliza — novedad frente al DW antiguo); **Mills (inspecciones)**; **cotizaciones** (auto individual y colectivo); **policy cycles** (calcula los ciclos de vigencia de la póliza); **coaseguro/corretaje** (nueva, con mejor precisión que el DW).

6. **Datamart de motor (autos):** primer gran desarrollo del CDP, hoy **productivo para pricing y modeling**. Reemplazó (reconstruido, mejorado y automatizado) el antiguo monitor de autos de SageMaker. La vista resumen para el usuario final es **monitor motor full**. Incluye: marca **nuevo/renovado** (certificada por pricing), cálculo de **expuestos** y **devengo** (earned premium = expuesto × prima), **Guía Fasecolda** (carga mensual, prerrequisito del modelo) y datos estáticos que antes vivían en Excel (democratización de los datos).

7. **`current_record_flag`:** campo presente en todas las tablas del esquema general; `= 1` trae el **último registro válido** (última versión de una DIM o último movimiento en una FACT).

8. **Llaves dinámicas (SK):** las SK **cambian en el tiempo**; se usan solo para hacer `JOIN`, **nunca se "queman" (hardcodean) en el código** ni se usan como filtro. Alternativa: llaves lógicas (póliza + certificado), aunque por rendimiento en Redshift (columnar) se recomienda la SK. Igual aplica para no quemar SBUs, códigos ni contraseñas en los desarrollos: no se productiviza código con datos quemados.

9. **Granularidad:** las FACT llegan hasta **amparo**; no hay nivel recibo. Agrupando amparos se obtiene la prima por póliza.

10. **Rendimiento y disponibilidad:** usar siempre `LIMIT`/`WHERE`; queries mal hechas pueden bloquear el CDP. Disponibilidad actual hasta las 10 p. m., próximamente **corte a las 6 p. m.** por la ventana de actualización; reapertura ≈ 5 a. m. **Las mañanas son el mejor horario**; en cierres contables hay congestión. El DBeaver a veces se pone lento por sí mismo (es la aplicación, no el CDP).

11. **Sandbox:** espacio de exploración y construcción. Cada usuario es dueño y responsable de sus objetos y debe **dar permisos** manualmente a quien necesite verlos. Vida útil de las tablas: **9 meses** (luego se eliminan). Hay una tabla de control con dueño, espacio (GB) y antigüedad. El espacio es limitado: borrar lo que no se use. La invitación es a **productivizar** los desarrollos (desarrollo colaborativo: negocio desarrolla → ingeniería revisa y optimiza → pasa al esquema general) para que el trabajo no se pierda ni se vuelva "un Liberty-pruebas-actuaría".

12. **Fuente única de la verdad:** no extraer datos directamente de IAxis ni cruzar CDP con el Data Warehouse SQL antiguo (infraestructuras e idiomas distintos); eso crea silos y "verdades" que compiten. La columna **`source`/`core_system`** indica el sistema de origen del dato. Los datos de AXS/AS400 saliente se dispondrán de forma distinta (ya existen en el datamart de modeling).

13. **Evolución continua:** el CDP se mejora a diario. Si falta una variable que existe en IAxis, se puede solicitar al equipo (análisis de factibilidad y prioridad). Los cambios quedan **documentados** en el repositorio; el diccionario de datos está en **Confluence** (solicitar acceso).

14. **Conexión:** antes DB Visualizer, hoy **DBeaver**; los pasos de conexión están en este manual (sección 4 y 5). Soporte de datos: Javier Gualdron y equipo; soporte de la aplicación DBeaver: mesa de ayuda.

15. **Próxima sesión:** los asistentes deben llevar un **caso de uso real** para desarrollarlo acompañados por el equipo CDP.

---

*Documento generado a partir del Manual de Usuario ADP v2.1 (Liberty, 28/11/2023), la transcripción de la Capacitación CDP (09/07/2026) y los parámetros de conectividad HDI vigentes.*
