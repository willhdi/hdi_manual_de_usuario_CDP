# Resumen explicado — Capacitación CDP (09/07/2026)

> Grabación: *Capacitación CDP-20260709* — duración 59 min.
> Expositores: **Karen Andrea Carvajal Jaramillo** (generalidades y modelo) y **Javier Leonardo Gualdron Romero** (contenido, datos y práctica).
> Asistentes: Juan Andrés Carrillo León, Juan Miguel Trujillo Lavao, entre otros.
> Este resumen también está incluido como Anexo (sección 9) del `CDP-MANUAL-DE-USUARIO.md`.

Este documento resume la capacitación en un lenguaje sencillo, pensado para alguien que **nunca ha trabajado con el CDP**. Cada vez que aparece un término técnico o de negocio, se explica en palabras simples.

---

## 1. ¿Qué es el CDP?

**CDP** significa **Colombia Data Program**. Antes se llamaba **ADP** (el proyecto original de la época de Liberty). Cuando se separó la información de los países (el proyecto inicial iba a incluir Chile, Colombia y Ecuador), quedó únicamente la información de **Colombia**, y de ahí el nuevo nombre.

En términos prácticos, el CDP es **una base de datos en Amazon Redshift**, montada sobre la nube de **AWS** (Amazon Web Services).

> 🟡 **¿Qué es Amazon Redshift?** Es un servicio de Amazon para almacenar y consultar volúmenes muy grandes de datos. Es una base de datos **columnar**: guarda la información por columnas en vez de por filas, lo que hace que las consultas analíticas (sumar, agrupar, filtrar millones de registros) sean mucho más rápidas.

### Analítico, no transaccional

El CDP nació con **propósitos analíticos**: sirve para generar **reportes e insights** (hallazgos a partir de los datos).

> 🟡 **¿Cuál es la diferencia?**
> - Una base **transaccional** es la que usa la operación del día a día (por ejemplo, el sistema donde se emite una póliza en ese instante).
> - Una base **analítica** consolida esa información para **analizarla después**: reportes, tableros, modelos. No es en tiempo real.

### ¿De dónde vienen los datos?

Las **fuentes maestras** del CDP son dos sistemas:

- **IAxis**: el sistema *core* (el aplicativo central donde se administran pólizas, siniestros, etc.).
- **AS400**: el sistema anterior/legado.

> 🟡 **¿Qué es un "core"?** Es el sistema principal donde ocurre la operación del negocio. El CDP **no reemplaza** a IAxis; toma su información y la organiza para análisis.

### ¿Por qué está en inglés?

Como el proyecto nació bajo directrices de Liberty/casa matriz, los esquemas, tablas y campos quedaron **mayoritariamente en inglés**. Se van a encontrar cosas en inglés y en español; el equipo está evaluando cómo unificar, pero no todo se podrá cambiar.

---

## 2. ¿Cómo está construido el CDP? (el "estándar medallón")

Cuando se trae información de los aplicativos a un data warehouse, hay una buena práctica llamada **estándar medallón**, que organiza los datos en capas:

1. **Capa cruda**: la información se extrae de los aplicativos tal cual llega, sin arreglar nada. Los campos pueden estar sueltos, sin relación entre sí.
2. **Capa de calidad**: se aplican **reglas de calidad** a los datos (limpiezas, validaciones).
3. **Capa productiva**: los datos ya limpios se organizan en un **modelo estrella** (datamarts), listos para ser consultados.

> 🟡 **¿Qué es un data warehouse?** Literalmente "bodega de datos": un repositorio que consolida información de varios sistemas para analizarla. **Ojo con el vocabulario interno:** técnicamente el CDP *es* un data warehouse, pero en el día a día del equipo, "Data Warehouse" se refiere al **antiguo data warehouse en SQL** (otra infraestructura distinta), y a este nuevo se le dice **CDP**. Es solo léxico para no enredarse.

---

## 3. El modelo estrella: tablas FACT y DIM

Es el concepto más importante de la capacitación. El **modelo estrella** organiza los datos en dos tipos de tablas:

- **FACT (tablas de hechos)**: guardan los **movimientos o transacciones** — "todo lo que mueva plata". Ejemplos: emití una póliza, la renové, la cancelé, se registró una reserva de un siniestro. Piense en un cajero automático: cada operación es una transacción, y cada transacción queda registrada en una FACT.
- **DIM (tablas de dimensiones)**: guardan los **atributos descriptivos** que le dan sentido a esos movimientos — nombres, ciudades, sucursales, ramos, vehículos, asegurados, etc.

### ¿Por qué separar en FACT y DIM?

En el data warehouse antiguo, una tabla "plana" repetía los mismos textos millones de veces (por ejemplo "Bogotá" en cada fila). En el modelo estrella, la FACT solo guarda un **código**, y ese código se cruza con la DIM para traer el nombre. Esto **ahorra almacenamiento y hace las consultas más rápidas y baratas**.

> 🟡 **¿Cómo reconozco cada tipo?** Por el prefijo del nombre: las dimensiones empiezan por `dim_` (ej. dimensión de direcciones, de calendario, de branch/sucursal) y las tablas de hechos por `fact_` (ej. la FACT de claims/siniestros).

### La regla de oro para armar reportes

> **Si el reporte contiene movimientos, siempre se arranca desde la FACT** y a ella se le van uniendo las DIM que se necesiten.

¿Por qué? Porque la FACT es la que "tiene conexión con todos lados". Entre dos DIM normalmente **no hay camino directo**: si usted arranca desde una DIM e intenta llegar a otra, tiene que pasar por la FACT. Ejemplo de la sesión: si quiero la prima emitida por sucursal en un periodo, la **prima está en la FACT** y el nombre de la sucursal viene de la **DIM de sucursal**.

Esta estructura multidimensional (imagínela como un **cubo** donde las dimensiones son las caras) hace el modelo **más flexible** que la tabla plana del data warehouse antiguo: uno puede "jugar con los datos" y combinarlos como quiera.

### Las tablas `_backup`

Van a ver tablas repetidas con sufijo *backup* (por ejemplo, varias de claims transaction). Son **respaldos internos** que el equipo saca cada vez que agrega una columna o mejora algo, por si algo sale mal. **No se consumen.** La tabla productiva **siempre conserva el mismo nombre**: si le hacen una modificación, actualizan esa misma tabla (y dejan el backup al lado); el nombre al que usted se conecta nunca cambia.

---

## 4. Las FACT más importantes del esquema general

El **esquema general** es el que se desarrolla a nivel compañía: es el mismo para todos los productos. Estas son las FACT que se destacaron:

| FACT | ¿Qué contiene? (en palabras simples) |
|------|--------------------------------------|
| **Primas** | Los movimientos de primas (el dinero que paga el cliente por el seguro). |
| **Siniestros (claims)** | Todos los movimientos de un siniestro: nace, se le asigna reserva, se paga, etc. |
| **IMX** | **Todos** los movimientos de una póliza, incluidos los **no transaccionales** (que no mueven plata). Ejemplo: un cambio de sucursal no aparece en la FACT transaccional, pero **sí** en la IMX. Es de las más usadas. |
| **Vigentes** | Las pólizas vigentes. Son **dos tablas** según cuánta historia se quiera: una guarda **28 días corridos** y otra solo la **foto del último día de cada mes**. Para autos ya está certificada; los demás productos irán quedando ahí. |
| **Preguntas y respuestas de IAxis** | Las preguntas que IAxis hace y sus respuestas. Son **tres FACT**: preguntas del **riesgo**, del **siniestro** y de la **póliza**. Esto **no existía** en el data warehouse antiguo. |
| **Mills (inspecciones)** | Información de inspecciones de vehículos. Es reciente y muy solicitada. |
| **Cotizaciones** | Las cotizaciones con sus variables más recientes. Existe para **auto individual** y **auto colectivo**; es de los productos que más se actualiza. |
| **Policy cycles** | Los **ciclos de vigencia** de la póliza. IAxis solo muestra cuándo arranca y cuándo termina la póliza; esta tabla **calcula los ciclos intermedios** (de qué fecha a qué fecha va cada periodo). Tampoco existía antes. |
| **Corretaje / coaseguro** | El corretaje de las pólizas. Es la más nueva (llevaba ~2 semanas al momento de la sesión); no es perfecta, pero con mejor precisión que el data warehouse antiguo. |

> 🟡 **Términos de negocio:** una **prima** es el precio del seguro; un **siniestro** es el evento que activa la cobertura (un choque, un robo); una **póliza** es el contrato de seguro; un **ramo** es la línea de negocio (autos, vida, etc.); una **cotización** es la propuesta de precio antes de emitir.

**Nota sobre salvamentos:** se preguntó en la sesión; el equipo no está seguro de tenerlos todavía (sería algo del lado de siniestros) y quedó de revisarse.

---

## 5. Dimensiones de apoyo útiles

- **DIM de calendario**: para cada fecha indica el periodo contable, el mes, el día de la semana, trimestre, cuatrimestre, etc. Muy útil para tableros con análisis en el tiempo.
- **DIM de departamento/ciudad**: soluciona un problema típico: el nombre de la ciudad puede venir escrito de mil formas ("BOGOTÁ", "Bogotá", "Santa Fe de Bogotá"). Si usted cruza por el **código** de departamento/ciudad de esta dimensión, todos sus tableros mostrarán **el mismo nombre estandarizado**.
- Otras dimensiones clave mencionadas: **póliza, riesgo, vehículo, conductor, asegurado, ramos, sucursal (branch)**. La idea es que la navegación sea **intuitiva**: "¿necesito datos del conductor? busco la DIM de conductor".

---

## 6. El datamart de motor (autos)

> 🟡 **¿Qué es un datamart?** Un data warehouse se compone de varios **datamarts**, y cada datamart apunta a un **dominio** (un tema de negocio). Es un conjunto de FACT y DIM enfocado en ese tema — en este caso, **autos**.

Fue el **primer gran desarrollo del CDP** y hoy es **productivo** para las áreas de **pricing** (tarifación: definir el precio del seguro) y **modeling** (modelación estadística). Lo construyeron esos equipos con el mismo modelo, la misma nomenclatura y la misma estrategia del esquema general, pero enfocado en autos.

Puntos clave:

- **Reemplaza el antiguo monitor de autos en SageMaker** (una herramienta de AWS), que era complejo y doloroso de actualizar. Se reconstruyó, se mejoró, se **automatizó** y se entrega en tiempos mucho más razonables.
- **Vista resumen: `monitor motor full`**. Todo el datamart se condensa en esa sola vista; para la mayoría de usos, es lo único que van a necesitar.
- **Marca nuevo/renovado**: una dimensión que indica si el negocio es nuevo o renovación. Está **certificada por pricing**; su lógica es compleja pero funciona.
- **Expuestos**: hay una FACT para el cálculo del expuesto (por ahora solo autos).
- **Devengo (earned premium / `erm_premium`)**: la prima "ganada" en el tiempo. Se calcula como **expuesto × prima** — es decir, lo que la aseguradora efectivamente devengó del precio del seguro según el tiempo transcurrido de cobertura.
- **Guía Fasecolda**: se **carga mensualmente** (es requisito previo para correr el modelo) y tiene histórico.
  > 🟡 **¿Qué es la Guía Fasecolda?** La referencia del gremio asegurador colombiano con los valores comerciales de los vehículos, por código.
- **Datos estáticos**: autos tenía datos propios en archivos de Excel (comprados o construidos por ellos). Se cargaron a la base de datos para que **todo el mundo pueda usarlos** y no se queden "en el Excel del dueño". Evitar los Excel sueltos es parte de **democratizar los datos**.
- Los **dueños** del datamart son pricing y modeling; ellos hacen cambios todo el tiempo, pero ahora **todo cambio queda documentado** en un repositorio que se puede consultar.

---

## 7. El campo `current_record_flag` (traer "lo último")

En las dimensiones, un mismo objeto puede tener **muchos registros** porque cambió en el tiempo. Ejemplo de la sesión: un vehículo aparece varias veces porque le cambiaron el color, el precio u otro parámetro.

Para eso existe el campo **`current_record_flag`** (bandera de registro vigente), que está **en todas las tablas del esquema general** como regla del modelo:

> **`current_record_flag = 1` → trae el último registro válido/actualizado.**

Ejemplos de uso: el dato más actual del vehículo en su DIM, el último movimiento de una póliza en la IMX, o el último movimiento transaccional en la fact de transaction movement. Es la forma estándar de filtrar cuando piden "lo último".

En la Guía Fasecolda el "último" también puede filtrarse por fecha (el último archivo es el del mes pasado).

---

## 8. Cómo cruzar tablas: llaves dinámicas (SK) y llaves lógicas

> 🟡 **¿Qué es una llave?** Un campo que permite conectar (hacer `JOIN` en SQL) una tabla con otra.

El modelo se diseñó con **llaves dinámicas**, las columnas que terminan en **`sk`** (surrogate keys). Nacieron en la época de Liberty para evitar choques entre países (la misma póliza podía existir en dos países). Son las llaves foráneas que conectan las FACT con las DIM.

**La regla más importante: las SK cambian en el tiempo.** Por eso:

> ⛔ **Nunca "quemar" (hardcodear) una SK en el código.**

> 🟡 **¿Qué significa "quemar" un dato?** Escribir el valor fijo dentro del código. Ejemplo: en vez de cruzar `ON a.sk = b.sk`, escribir `WHERE sk = 9`. Como la SK **se mueve**, ese `9` mañana puede apuntar a otra cosa y la consulta deja de traer la información correcta **sin avisar**.

La misma lógica aplica a otros valores: si usted quema una **SBU** (unidad de negocio, ej. "autos") o un código, y ese valor cambia, su reporte **nunca se va a actualizar**. Y las **contraseñas jamás se dejan quemadas** en el código (aplica sobre todo si trabajan en Python; en SQL puro no tienen ese problema — el equipo enseña cómo manejarlo). Regla del equipo: **no se productiviza código con datos quemados** ("lo sentimos, pero no").

**Alternativa "colombianizada": las llaves lógicas.** El equipo creó llaves construidas con campos de negocio, por ejemplo **póliza + certificado**. Cruzar por ellas también funciona. Sin embargo, **por rendimiento se recomienda la SK**, porque el modelo columnar de Redshift está optimizado para eso.

**Excepción:** hay tablas que ya no usan SK, como la de **ciudades**, que se cruza por código — ese código sí es estable y no cambia.

---

## 9. Granularidad: hasta amparo

> 🟡 **¿Qué es granularidad?** El nivel de detalle de los datos. "Grano fino" = mucho detalle; "grano grueso" = datos agregados.

La granularidad de las FACT llega **hasta amparo** (cada cobertura individual dentro de la póliza). **No existe el nivel recibo**, que es un detalle aún más fino. Si necesita cifras por póliza, **agrupe los amparos y sume** — de amparo hacia arriba todo se puede construir.

> 🟡 **¿Qué es un amparo?** Cada cobertura específica de la póliza (ej. en autos: pérdida total, responsabilidad civil, hurto). Una póliza tiene varios amparos.

---

## 10. Buenas prácticas de consulta y horarios

- **Siempre usar `LIMIT`, `WHERE` o filtros** en las consultas. Una query pesada y sin filtros puede **bloquear el CDP para todos** (ya ha pasado).
- **Mejor horario: las mañanas** — el CDP "anda relajado". Desde media mañana (≈10 en adelante) y en **cierres contables** la cosa se pone lenta y congestionada.
- Si una consulta se demora demasiado, el sistema **puede cancelarla**.
- **Disponibilidad:** hoy el servicio va hasta las **10 p. m.** En pocos días el corte pasará a las **6 p. m.**, porque a esa hora arranca la **ventana de actualización nocturna** (las áreas comerciales necesitan sus datos más temprano). Reapertura automática al terminar la carga, aproximadamente a las **5 a. m.** Más adelante se normalizará a un horario más amplio.
- Si nota lentitud, distinga la causa: a veces es **DBeaver** (la aplicación) y no el CDP. Y ojo: el **Data Warehouse SQL antiguo es otra infraestructura** — si ese está lento, no es un problema del CDP ni lo resuelve el equipo CDP.

---

## 11. El sandbox: su zona de trabajo

> 🟡 **¿Qué es un sandbox?** Literalmente "caja de arena": un espacio donde cada usuario puede **explorar, crear tablas y vistas, y experimentar** sin afectar los esquemas productivos.

Reglas del sandbox del CDP (diferente a como funcionaba "pruebas actuaría"):

1. **Cada usuario es dueño y responsable de sus objetos.** Si un compañero necesita ver su tabla, **usted mismo le otorga el permiso** (los permisos se dan entre usuarios, manualmente).
2. **Vida útil: 9 meses.** Una tabla con más de 9 meses **se elimina**.
3. **El espacio es limitado y está muy disparado** (mucha gente está creando productos de datos). Es un tema de conciencia: si ya no necesita una tabla o un backup, **bórrelo**. Si no mejora el uso, tocará endurecer las políticas de retención.
4. Existe una **tabla de control** consultable donde se ve: el **dueño** de cada tabla, el **espacio** que ocupa (en GB), si **lleva más de 9 meses** (candidata a borrado) y un dato aproximado de **último uso** (aproximado porque la auditoría de Redshift solo guarda 7 días y se extrae una vez al mes). También sirve para saber a quién pedirle permiso sobre una tabla.

---

## 12. Productivización: que su trabajo no se pierda

El equipo promueve el **desarrollo colaborativo**:

1. **El área de negocio desarrolla** en el sandbox (una vista, una consulta, un producto de datos — por ejemplo para alimentar tableros).
2. Se envía al equipo CDP, donde pasa un **chequeo de requerimientos mínimos**.
3. **Ingeniería revisa y optimiza el código**, y lo pasa al **esquema general** (lo "productiviza").

¿Por qué hacerlo? Porque lo que se queda en el sandbox **se borra a los 9 meses**; al productivizarlo, el trabajo **no se pierde**, queda **automatizado** (nadie tiene que "estarle dando clic") y queda con el código optimizado. La invitación explícita de la sesión: que el sandbox no se convierta en el nuevo "Liberty pruebas actuaría".

---

## 13. Fuente única de la verdad

Un principio central del CDP:

- **No extraer datos directamente de IAxis** para armar reportes propios. Si cada quien saca sus datos del core, crea un **silo** (una "verdad" aislada) y su verdad empieza a pelear con la de los demás. Si todos consumen el mismo modelo, **a todos les dan los mismos números**.
- **No mezclar el CDP con el Data Warehouse SQL antiguo** en una misma consulta ("injertos"): son infraestructuras distintas, diseñadas en lenguajes distintos, y no se pueden conectar entre sí desde una misma conexión.
- Para saber de qué sistema viene un dato, existe la columna **`source` / `core_system`**, que indica el **sistema de origen** (por ejemplo AS400). Nota de la sesión: los movimientos del AS400 **no** van a quedar dentro de las FACT de este modelo (el AS400 va de salida); esos datos se habilitarán de otra forma — en el datamart de modeling ya está resuelto.

---

## 14. Evolución continua y soporte

- El CDP **no es perfecto y se mejora todos los días**: nuevas columnas, nuevas variables de IAxis, nuevos productos.
- **Si le falta una variable** que usted ve en una pantalla de IAxis, **se puede solicitar**: el equipo hace un análisis de **factibilidad y prioridad** (todo cambio requiere pruebas porque afecta a la compañía). "Todo es factible, a su debido tiempo y en su debida prioridad" — y puede que el dato **ya esté**.
- **Diccionario de datos:** está en **Confluence** (hay que solicitar permisos de acceso).
- **Documentación de cambios:** los cambios del modelo quedan documentados en un **repositorio** que se puede solicitar.
- **Soporte:** temas de **datos** → Javier Gualdron y su equipo. Problemas con la **aplicación DBeaver** → mesa de ayuda.

---

## 15. Conexión al CDP

Antes se usaba **DB Visualizer**; hoy la herramienta es **DBeaver**.

> 🟡 **¿Qué es DBeaver?** Un programa gratuito para conectarse a bases de datos y ejecutar consultas SQL. Tiene ayudas útiles, como el autocompletado que "predice" los nombres de las variables. Al conectarse verán la base `adp_dwh` (ADP Data Warehouse) y dentro de ella los esquemas (el general, el sandbox, los datamarts).

Parámetros de conexión por ambiente:

| Ambiente | Host | Puerto | Base de datos |
|----------|------|--------|---------------|
| Producción (Prod) | `corshftanltc-dprogramp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| No Producción (Non Prod) | `corshftanltc-dprogramnp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| Desarrollo (Dev) | `corshftanltc-dprogramd.hdicolombia.com.co` | `9519` | `adp_dwh` |

> 🟡 **¿Qué significan los ambientes?** **Producción (Prod)** es el ambiente real, con los datos oficiales que consume la compañía. **Desarrollo (Dev)** y **No Producción (Non Prod)** son ambientes donde el equipo técnico construye y prueba cambios antes de llevarlos a producción.

---

## 16. Tarea para la próxima sesión

Traer un **caso de uso real** (algo que ustedes de verdad necesiten construir) para desarrollarlo en la siguiente reunión **con acompañamiento del equipo CDP**. La dinámica: ustedes lo hacen, el equipo acompaña y guía.

---

## Mini-glosario rápido

| Término | En palabras simples |
|---------|---------------------|
| **CDP** | Colombia Data Program: la base de datos analítica de HDI Colombia en Redshift/AWS. |
| **Data warehouse** | Bodega de datos: consolida información de varios sistemas para analizarla. |
| **Datamart** | Porción del data warehouse enfocada en un tema (ej. autos). |
| **FACT** | Tabla de hechos: movimientos/transacciones ("todo lo que mueva plata"). |
| **DIM** | Tabla de dimensiones: atributos descriptivos (nombres, ciudades, vehículos…). |
| **Modelo estrella** | Organización FACT + DIM que hace las consultas más rápidas y baratas. |
| **SK (llave dinámica)** | Columna para cruzar tablas; **cambia en el tiempo**, nunca quemarla en el código. |
| **Llave lógica** | Llave construida con campos de negocio (ej. póliza + certificado). |
| **Quemar (hardcodear)** | Escribir un valor fijo dentro del código; prohibido para SK, SBUs, códigos y contraseñas. |
| **`current_record_flag = 1`** | Filtro estándar para traer el último registro válido. |
| **Granularidad** | Nivel de detalle de los datos; en el CDP llega hasta **amparo**. |
| **Amparo** | Cada cobertura individual dentro de una póliza. |
| **Sandbox** | Espacio personal para experimentar; los objetos viven máximo 9 meses. |
| **Productivizar** | Pasar un desarrollo del sandbox al esquema general, revisado y automatizado. |
| **Fuente única de la verdad** | Todos consumen el mismo modelo para que los números den igual para todos. |
| **IAxis** | El sistema core (aplicativo central de la operación). |
| **AS400** | Sistema legado, en proceso de salida. |
| **DBeaver** | Programa para conectarse al CDP y ejecutar consultas SQL. |
| **Devengo (earned premium)** | Prima "ganada" según el tiempo de cobertura: expuesto × prima. |
| **Guía Fasecolda** | Referencia de valores comerciales de vehículos; se carga cada mes. |
