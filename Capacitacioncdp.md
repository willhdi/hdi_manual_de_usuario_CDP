Capacitación CDP-20260709_150325-Grabación de la reunión
9 de julio de 2026, 8:03p.m.
59m 3s

Carrillo Leon, Juan Andres inició la transcripción

Carvajal Jaramillo, Karen Andrea   0:03
Voy a comenzar por compartirles mi pantalla. La Javi, Javicillo es el que más conoce, pues todo el tema a nivel de contenido que tiene CDP.

Gualdron Romero, Javier Leonardo   0:12
Hello!

Carvajal Jaramillo, Karen Andrea   0:17
Con el equipo estamos trabajando en construir. De hecho, ya había un manual, ya había un manual de CDP que se ha construido desde Liberty para contarles un poquito. Voy a empezar con las generalidades de lo que es CDP de la migración. Bueno, etc, etc, y ya pasamos.
Luego a explorar la base de datos.
Entonces, resulta que, como ustedes saben, pues que primero que antes era el antes Data Program, esto pasó a ser CDP que significa Colombia Data Program. Y esto no es más que una base de datos en Redshift en la plataforma de Amazon, de Amazon.

Carrillo Leon, Juan Andres   0:58
German.

Carvajal Jaramillo, Karen Andrea   1:03
web service donde eh queríamos generar un cambio digamos que esto inicialmente nace nace con propósitos analíticos Sí una cosa es uno de pronto tener una base de datos transaccional y otra cosa es tener bases de datos analíticas eh que se usan principalmente pues para generar insights para generar reportes

Carrillo Leon, Juan Andres   1:17
Bueno, cambiamos.

Trujillo Lavao, Juan Miguel   1:19
Pero Sandra.

Carrillo Leon, Juan Andres   1:24
What?

Carvajal Jaramillo, Karen Andrea   1:27
Entre otras cosas, ahí me corriges Javi, si estoy diciendo algo que de pronto Javi tiene mucha más historia de cómo nace el proyecto.

Carrillo Leon, Juan Andres   1:34
Nice.
Encuentro.

Gualdron Romero, Javier Leonardo   1:39
No está bien.

Carrillo Leon, Juan Andres   1:42
I don't.

Carvajal Jaramillo, Karen Andrea   1:42
Listo.
Entonces, inicialmente este proyecto estaba pensado, pues para que estuviera la información tanto de Chile, de Colombia, de Ecuador. Ustedes saben que nosotros separamos toda la información. Esto quedó solamente para Colombia. Sin embargo, como las directrices venían de mutual y demás, se crearon esquemas, casi que todo el CDP está construido.

Trujillo Lavao, Juan Miguel   1:46
Y.

Carrillo Leon, Juan Andres   1:47
Yeah.
Bien.
Okay.

Carvajal Jaramillo, Karen Andrea   2:06
Con los esquemas, con las dimensiones y demás en inglés, entonces ustedes se van a encontrar mucho si de pronto pudieron echarle una miradita al diccionario de datos que no sé si pudieron solicitar los permisos a Confluence.

Carrillo Leon, Juan Andres   2:17
Sí, Miguel, Miguel ya tienen. A mí fue el único que fue chistoso porque los 2 montamos el caso y a Miguel se los dieron y a mí no, pero bueno, ahí estamos esperando el mío.

Carvajal Jaramillo, Karen Andrea   2:19
Sí.
listo entonces eh aquí cambian varias cosas dentro de adp esto era un poquito lo que les contaba de la arquitectura eh estas pues al final son como las fuentes las fuentes maestras de donde viene la información que no son más que el Core y access a ese 400
Esto está pensado en un esto es un poquito más técnico, pero digamos que en las buenas prácticas de la construcción de data warehouse, o más bien de procesos ITEL, cuando se trae información, hay un estándar que se llama como estándar medallón.
eh Ah bueno sí aunque aquí solamente hay de cerró Data Warehouse sería como lata y el datamarolo cierto Javi Entonces qué pasa usualmente cuando yo traigo la información cruda de de los aplicativos esta llega y obviamente no está relacionada No yo por una parte puedo tener el campo no sé de la cédula
pero no necesariamente va a estar en la misma tabla, me invento algo el nombre o no necesariamente el campo que yo necesito como la suma asegurada o etc, etc. Entonces lo primero que se hace es extraer esa información de manera cruda que viene de los aplicativos, posterior a eso hay una segunda capa donde se hacen algunas reglas de calidad.
Dentro de los datos y por último, los digamos que los datos productivos tienen un modelo de Datamar o un modelo estrella. Digamos que el CDP está construido para tener unas mejores prácticas, que eso también se los explicábamos en la capacitación de Power BI. Y es que lo que pretendemos al final es que esto nos permita reducir costos y eficiencia.
En el momento en el que consultamos la información, entonces, ¿qué es esto del modelo estrella? Esto del modelo estrella y ya pasamos ahorita a mirar el tema de cómo está la nomenclatura y demás. Quiere decir que yo construyo unas tablas de dimensiones y unas tablas de hechos con el fin de hacer mucho más óptimas tanto las consultas como el almacenamiento de información.
¿Cierto? Es decir, yo en una tablita grande podría tener aquí. Ahora vamos, no base de datos, esto es otra. Ahora vamos un Excelito.
Entonces yo acá podría tener.
Esto va a ser ciudad.
Ciudad, nombre, nombre, cliente, me inventó algo.
Gente acá podemos decir.
Que vamos a tener apellido intermediario, por decir algo.
Intermediario que pasa mucho o qué pasaba, por ejemplo, en el DataWarehouse, que estaba esto repetido. Digamos que aquí estaba Bogotá y volvíamos a tener Bogotá y aquí estaba el nombre del cliente xx e intermediario. Entonces acá es la clave doce veinte me inventó algo y esta también estaba acá muchas veces.
Bueno, más bien el nombre.
¿Qué busca al final? Reducir. Entonces yo ya no voy a tener en esa tabla de dimensiones en la tabla derechos, discúlpame, todos los nombres repetidos, sino que seguramente voy a tener un código asignado que cuando yo vaya a esa tabla de dimensiones me va a traer esa información. Sí, esto es mucho más óptimo. Entonces generalmente hay llaves con las que yo cruzo para poder traer esa información.
Este es un ejemplito acá de qué es la FAC. Generalmente las FAC son las tablas de hechos donde está cada uno de los movimientos y las dimensiones son esos atributos que yo busco traer a esa información para darle sentido. Usualmente son los nombres, entonces acá, por ejemplo, estaba la dimensión de Ramos, cierto, entonces tenía una llavecita, tenía un código de ramo y yo acá podía traer
el ramo eh a esta faca no sé si hasta ahí vamos bien o tienen alguna duda

Carrillo Leon, Juan Andres   6:38
¿Cómo se identifica un ******* dim? ¿Tiene algún?

Carvajal Jaramillo, Karen Andrea   6:42
sí tienen la nomenclatura Entonces vamos a entrar a la base de datos esta no es espérenme yo ad cuando ustedes ingresan a cdp
entonces Generalmente les va a aparecer esta basecita que dice adp Atta Warehouse y acá sabemos que estamos conectados de pronto también dentro del manual que estamos trabajando les dejamos todo el tema de las conexiones pero cuando vamos a las bases de datos entonces aquí abrimos el tema de los esquemas
este cosambox datos es como ese sitio donde ustedes pueden explorar pueden generar no solamente digamos que aquí pueden ustedes construir qué pasa con los esquemas productivos que ya les hablamos un poquito de Qué es el esquema general de Qué significa
eh jd jd no es es Sí y demás pero acá por ejemplo si vamos a este esquema que es uno de los más utilizados ustedes van a encontrar que hay muchas que dicen din Entonces esta es la dimensión de direcciones
Di la dimensión de brunch, que es que sin que traduce aquí Javi, o sea, marca no, sino bueno.

Gualdron Romero, Javier Leonardo   8:13
Send.

Carvajal Jaramillo, Karen Andrea   8:15
Exactamente de calendario. Todas estas están marcadas por DIM y también están las FAC, que van a ser las que ustedes acá. Entonces acá están, por ejemplo, las FAC de claims.
de bueno esto tiene acá unos backups y demás Pero ustedes las pueden identificar por el inicio de la nomenclatura entonces Ah bueno yo ya sé que para traer cualquier información de esta F seguramente voy a tener que cruzar por las llavecitas con las din
Por ejemplo, está de riesgo.

Carrillo Leon, Juan Andres   8:53
¿Dónde se están?

Carvajal Jaramillo, Karen Andrea   8:53
esto es como ustedes van a ver los esquemas eh volvemos un poquito a la teoría como para terminarles de explicar esto las tablas de dimensiones las tablas de hecho igual esto también se los dejamos eh dentro del manual Eh Esto ya se los expliqué que cada una de las dimensiones pues va a tener la llave para poderla cruzar
¿Y cómo? Bueno, de pronto yo acá cómo usarlo.

Trujillo Lavao, Juan Miguel   9:18
Una pregunta.
Una pregunta, disculpa, ahí sobre las dimensiones y el fact puede subir un momentico.

Carvajal Jaramillo, Karen Andrea   9:22
Dime, dime.
Mhm.
Claro.

Trujillo Lavao, Juan Miguel   9:30
Por ejemplo, si en las dimensiones sucursales, si yo quiero saber entonces.
La prima emitida en un periodo de tiempo, la llave que me traería la sucursal viene de la dimensión sucursal y la prima estaría en fat, en fat, sí.
Hola.
Si.

Carvajal Jaramillo, Karen Andrea   10:01
Pasó y tenía ese valor.

Carrillo Leon, Juan Andres   10:04
Se registró, ustedes fueron los que nos ayudaron.

Carvajal Jaramillo, Karen Andrea   10:05
Ajá.

Gualdron Romero, Javier Leonardo   10:07
Igual muchas veces tengan en cuenta que cuando cuando ustedes vayan a armar cualquier tipo de reporte, si contiene movimiento, siempre arranquemos desde la FAC.

Trujillo Lavao, Juan Miguel   10:11
O de verdad.
Okay.

Carvajal Jaramillo, Karen Andrea   10:17
Sí.

Gualdron Romero, Javier Leonardo   10:17
Como pueden ver, la FAG es la que la que tiene conexión con todos lados. Tú arrancas desde una DIM, pues seguramente para llegar de la DIM a la sucursal no hay un camino. Si tú ves que no hay un camino directo, si ves, entonces tienes que pasar por la FAG, entonces normalmente en estos en estos modelos multidimensionales y en cubo, digamos que si tú cogieras esas dimensiones que ves ahí en la gráfica.

Trujillo Lavao, Juan Miguel   10:25
Sí.
Claro.
MC.
Sí.

Gualdron Romero, Javier Leonardo   10:39
Y los tuvieras encima y los tuvieras debajo y los piezas atrás, pues tú armas un grupo, un cubo, perdón. Entonces eso qué es lo que permite y es parte de las mejoras del CDP, hace un modelo más flexible porque tú puedes jugar con los datos literal como quieras. A diferencia del Data West 2 pues que tienes una tabla plana, tiene sus ventajas, pero pues aquí lo hace más flexible.

Trujillo Lavao, Juan Miguel   10:40
¿Qué?
I am.
Right.
Pero especial.

Gualdron Romero, Javier Leonardo   10:59
Eso es para que tengan eso en cuenta cuando vayan a crear productos, si usa más de una tabla, arranquen por la FAC, arranquen por la FAC y ahí van uniendo las dimensiones que va necesitando.

Carrillo Leon, Juan Andres   11:01
Cortana.
Pero no hay doble por favor.

Trujillo Lavao, Juan Miguel   11:04
Okay.

Carrillo Leon, Juan Andres   11:07
Yeah.

Trujillo Lavao, Juan Miguel   11:07
No.

Carrillo Leon, Juan Andres   11:10
Acá, en el caso del de los PGS, no sé, necesitaríamos la FAC de prima emitida, la FAC de prima devengada, la FAC de siniestros y la FAC de comisiones, y ya eso lo unimos a las sucursales y al resto.

Trujillo Lavao, Juan Miguel   11:14
Y ya eso porque esta.

Gualdron Romero, Javier Leonardo   11:21
Listo.

Carvajal Jaramillo, Karen Andrea   11:24
A quiet.

Gualdron Romero, Javier Leonardo   11:25
Algo así, algo así. Sí, existe una FAC de primas que es esta y existe una FAC de siniestros que se llama Thames, no sé qué, y el tema de la exposición y todo eso está en otro en otro de atamar, pero igual se puede usar para pegarlo a este. O sea, eso es lo que permite la multidimensionalidad.

Trujillo Lavao, Juan Miguel   11:28
¿Qué es?
Yes.
Yeah.
No busco.

Carrillo Leon, Juan Andres   11:37
Hello!
Y el de vigentes, sí.

Trujillo Lavao, Juan Miguel   11:42
Indict.

Gualdron Romero, Javier Leonardo   11:45
Está en construcción y también lo puedes unir.

Carrillo Leon, Juan Andres   11:45
No, yo ya le no, yo le digo, pero entonces yo voy.

Trujillo Lavao, Juan Miguel   11:45
No, yo me diré.

Carvajal Jaramillo, Karen Andrea   11:50
entonces bueno eh aquí ya venían como unos pasitos de conexión antes utilizaba visualizer pero en este momento Pues nosotros utilizamos diver Esto sí hay que actualizarlo acá básicamente lo que les dice es Cómo establecer la conexión eh Y demás Esto sí sí se los pasamos

Trujillo Lavao, Juan Miguel   11:53
Okay.
Sí.
Y.
Canon?
Sí.
I think.

Carvajal Jaramillo, Karen Andrea   12:10
actualizado porque hoy hoy ya funciona un poquito diferente y aquí de pronto pues le doy paso a Javi para que les explique más. Ahora sí, ya en temas de contenido que tenemos hoy en el datamar de motor, que ha sido un desarrollo, pues que fue como el primer gran desarrollo que se hizo en el CDP y hoy ya es productivo tanto para las áreas de pricing como de modeling.

Trujillo Lavao, Juan Miguel   12:17
What?
So, parte de derechos.
No, pues no te la.
Pablo.
Esteban.
Yeah.

Carvajal Jaramillo, Karen Andrea   12:35
como para que ustedes le echen una exploradita. No sé si de todo esto que les he comentado tienen alguna otra pregunta, inquietud, necesitan apoyo con algo de eso.

Trujillo Lavao, Juan Miguel   12:46
¿Este documento que nos presentaste dices que nos lo vas a entregar ya actualizado, verdad? O K listo, perfecto.

Carvajal Jaramillo, Karen Andrea   12:52
Mhm.

Gualdron Romero, Javier Leonardo   12:59
Bueno, muchachos, vamos a ir al combate, vamos a los datos y les voy a mostrar a parpar un poquito.

Carvajal Jaramillo, Karen Andrea   12:59
Stone.

Gualdron Romero, Javier Leonardo   13:09
Pues todo lo que les ha comentado Karencilla, listo, entonces aquí está el esquema general, está viendo mi pantalla.

Trujillo Lavao, Juan Miguel   13:17
Sí.

Gualdron Romero, Javier Leonardo   13:18
Listo, aquí está el esquema general, simplemente es para mostrar lo que ya vieron en el PDF. Aquí está, pues con todas sus facts, digamos que existen fact backup, pero pues eso simplemente es un backup. Entonces hay mucho, muchas cosas que intuitivamente tal vez ustedes las van viendo, ya van deduciendo.

Carrillo Leon, Juan Andres   13:18
To.

Trujillo Lavao, Juan Miguel   13:26
What's the regular?
Salinas.

Gualdron Romero, Javier Leonardo   13:38
Sin necesidad de ir a alguna documentación. Si usted dice, uy, claima, pues esta es una dimensión, es una fac de claim, aquí están los siniestros. Bueno, ahí toca es la conversión de idiomas que aquí está en inglés. Uy, por acá tenemos las dimensiones de la póliza, pero también tenemos las dimensiones del riesgo que está por aquí abajito.

Trujillo Lavao, Juan Miguel   13:52
O K, gracias.

Gualdron Romero, Javier Leonardo   13:57
que sea súper importante aquí está la dimensión del riesgo Uy no resulta que nosotros necesitamos datos de los vehículos donde está por aquí hay una dimensión de vehículos por aquí está no la veo no la veo pero por aquí voy a estar

Trujillo Lavao, Juan Miguel   13:58
Thank you.
Hola.
That's it.

Gualdron Romero, Javier Leonardo   14:10
Aquí está. Uy, resulta que nosotros necesitamos información del conductor. Busquemos a ver dónde está la información del conductor. Aquí está. Uy, no, necesitamos información del asegurado. Busquemos la dimensión del asegurado que debe estar por aquí. Aquí está. Entonces digamos que al final todo es muy. La idea es que sea muy intuitivo y que ustedes mismos puedan jugar con los datos. No hay algo que esté construido que les va a solucionar la vida a todos. no.

Trujillo Lavao, Juan Miguel   14:10
Okay, I did.
Felipe.
Thanks for me.
That's what I'm doing.

Gualdron Romero, Javier Leonardo   14:34
Ustedes van a tener la facilidad de que ustedes empiecen a construir y que ustedes vayan cogiendo lo que necesiten.

Trujillo Lavao, Juan Miguel   14:37
Es que.

Gualdron Romero, Javier Leonardo   14:42
Lo que necesiten. ¿Qué dimensiones es lo más importante que hemos detectado hasta ahora y basado en la experiencia que hemos tenido? Pues están las FAT, está la claim, que aquí está todo el tema.

Trujillo Lavao, Juan Miguel   14:54
Que haya dicho.

Gualdron Romero, Javier Leonardo   14:54
O sea, cuando es una tabla de hechos, una transacción, todo lo que tenga que ver con una transacción está en una FAC, que yo emití una nueva póliza, que yo la renové, que yo la cancelé. Todo eso son transacciones en siniestros es exactamente igual, todos los todos los movimientos que tenga un siniestro, que porque un siniestro nace y empieza a tener movimientos, que la reserva, que va la reserva, que no se que ta ta ta.

Trujillo Lavao, Juan Miguel   15:07
A little bit more.
What?

Gualdron Romero, Javier Leonardo   15:17
Todo va quedando acá, entonces ya después de que ustedes tengan, dime.

Trujillo Lavao, Juan Miguel   15:19
No está.

Carrillo Leon, Juan Andres   15:19
¿Una preguntilla, aquí se ve que digamos ese claims transaction existan como cuatro por capacidad? ¿A caps o k?

Trujillo Lavao, Juan Miguel   15:22
Y.

Gualdron Romero, Javier Leonardo   15:25
Some backups.

Trujillo Lavao, Juan Miguel   15:27
Cuatro.

Gualdron Romero, Javier Leonardo   15:28
Son backup, digamos que cada vez que metemos una nueva columna, porque esto, o sea, esto todos los días nosotros estamos mejorándolo, ya sea mejorando lo que existe, como colocándole cosas nuevas. Digamos que esto es de todos los días. Entonces para evitar, ustedes saben, hay que tener backupsitos por si algo sale mal.

Trujillo Lavao, Juan Miguel   15:30
I mean.
Yeah.

Carrillo Leon, Juan Andres   15:36
Sí, okey.
Digamos, en el caso de que yo me conecte a esa de transacción, si la iban a hacer una modificación, actualizarían esa o crearían una nueva.

Gualdron Romero, Javier Leonardo   15:51
Sí, esa siempre va a ser la misma, esa siempre va a ser la misma. Lo que hacemos es como sacamos un backup y la dejamos al lado, pero esa va a ser la misma. Ese nombre nunca va a cambiar, ese va a ser el nombre que te vas a conectar y siempre se va a llamar así listo.

Carrillo Leon, Juan Andres   15:54
Okay, list.

Trujillo Lavao, Juan Miguel   15:55
Clara.
Pues sí.

Carrillo Leon, Juan Andres   16:01
Okay.

Gualdron Romero, Javier Leonardo   16:06
Ahora se me fue, se me fue la piola. Bueno, no le estaba comentando lo que normalmente y lo que más usamos están las como tal las de hechos.

Trujillo Lavao, Juan Miguel   16:09
Listo.

Gualdron Romero, Javier Leonardo   16:15
Está. Hay un tema que últimamente lo usan mucho. Bueno, aquí está la de vigentes, las FAC de vigentes están 2. Se dividen en qué tanta historia quieras tener. Esta tiene 28 días corridos, esta solamente guarda la del último día de cada mes. Entonces ahí están las 2. Creo que para el tema de autos eso está bastante avanzado. Creo que entonces ya lo certificaron y todo.

Trujillo Lavao, Juan Miguel   16:15
Gracias.
Sí.
Pero yo también.

Carrillo Leon, Juan Andres   16:37
Sí, dice, de hecho, es verdad que está bien aquí.

Trujillo Lavao, Juan Miguel   16:37
Sí.

Gualdron Romero, Javier Leonardo   16:37
Ahí van a quedarlos vigentes de los demás productos, por si algún día eso le les pregunta, están estas estas facts son chéveres porque algo que nos preguntan mucho es las preguntas y respuestas de Iaxis. Allá ahí tiene unas preguntas que dice, la pregunta ahí yo tienes la respuesta, aquí te la vas a encontrar.

Trujillo Lavao, Juan Miguel   16:47
Activación.
También.
Pero.

Gualdron Romero, Javier Leonardo   16:57
Y vas a encontrar 3 FAC: una, las preguntas del riesgo, otra, las preguntas del siniestro y otras preguntas de la póliza. Entonces las 3 las va, las vas a encontrar ahí. Eso es algo nuevo, es algo que no lo teníamos en Tata WhatsApp. Aquí sí lo tenemos y estamos mejorándolo continuamente, porque pues todas estas cosas no son perfectas y hay un tema de preguntas que la pregunta era su pregunta era su pregunta que.
Seguimos mejorando, pero el grueso, el grueso ya está ahí. Esto de Mills creo que si están necesitando información de autos, Mills que son inspecciones, eso es una FAC que hace poquito nos la han pedido y la solicitan y le dan duro a esa vaina. Por aquí está el tema de cotizaciones, aquí está el tema de cotizaciones, mortal técnico, policy coti auto.

Trujillo Lavao, Juan Miguel   17:20
Y.
Thanks.

Carrillo Leon, Juan Andres   17:28
Thank you.

Trujillo Lavao, Juan Miguel   17:28
I.
Pero.

Gualdron Romero, Javier Leonardo   17:42
Ahí está todo lo que es cotizaciones auto individual con sus últimas variables que han solicitado, porque es de los productos que más se mueve que más estamos actualizando diariamente. Lo tenemos para auto individual, lo tenemos para auto colectivo. Listo, entonces, y esta policy cycles es esto es algo nuevo, esto tampoco es en data warehouse.

Trujillo Lavao, Juan Miguel   17:45
Es que ver.
Esa mucha aquí.

Gualdron Romero, Javier Leonardo   18:04
Es algo súper chévere porque te da la vigencia.

Trujillo Lavao, Juan Miguel   18:04
Vale.

Gualdron Romero, Javier Leonardo   18:08
La vigencia en fechas de la póliza. ¿Qué pasa? No sé si ustedes han observado que ni axis. Tú cuando entras ahí axis te dice cuándo arranca la póliza y cuándo termina, pero no te da en que en las mitades, en qué periodo va y en qué ciclo voy, en qué ciclo voy, en qué ciclo voy. Esta te calcula los ciclos.

Trujillo Lavao, Juan Miguel   18:11
I did.
Before you have to.
I.
Ya.

Gualdron Romero, Javier Leonardo   18:27
Entonces ahí te dice, va en el ciclo que empieza desde tal hasta tal fecha y Axis normalmente te da la primera y la última. Esta tabla te calcula los ciclos, entonces te calcula los ciclos de las pólizas. Es una tabla muy chévere que igual como todo lo hemos ido mejorando y cada vez, pues , pues tenemos mejores resultados. Por acá tenemos un tema de cocorretaje también, esa es nuevecitica, esa lleva como.

Trujillo Lavao, Juan Miguel   18:30
Siri.
Good.
¿Por qué?
Sí.

Gualdron Romero, Javier Leonardo   18:48
2 semanas y ese pues el corretaje de las pólizas muy, o sea, si bien no es perfecta, pero hemos tenido unos niveles de precisión más altos que el data warehouse, lo que hemos tratado de hacer aquí en CDPS o estamos igual o estamos mejor, pero peor si no podemos estar o si no, o si no nos pasamos.

Trujillo Lavao, Juan Miguel   18:58
¿Cómo?
Good next.
Avance.

Gualdron Romero, Javier Leonardo   19:07
Esto que están viendo del esquema general es lo que estamos desarrollando a nivel compañía. O sea, que para todos es lo mismo, para todos los productos. Ya cuando vamos a a SDUs o a grupos de productos un poquitico más específicos, digamos que motor generales ya abrimos.

Trujillo Lavao, Juan Miguel   19:25
Salte y salte líder, no, ya decir como ver.

Gualdron Romero, Javier Leonardo   19:27
Abrimos la puerta para que empiecen a desarrollar basado en eso, abrimos la puerta para que empiecen a desarrollar el equipo de modeling y de pricing. Ellos desarrollaron un modelo de datos propio de ellos, que es el que conocemos como el Datamar, que no sé si ustedes algún día conocieron el.

Trujillo Lavao, Juan Miguel   19:30
¿Cuánto están?
Claro que sí.
Dame.
Sí.

Gualdron Romero, Javier Leonardo   19:46
El monitor, El monitor en SageMaker de autos, esa vaina que era un dolor de cabeza. Yo creo que para todos también aquí lo hicimos mejorado. Eso, bueno, eso nosotros lo que hicimos fue o k reconstruyamos esa vaina porque eso es, yo me acuerdo que era hasta bastante complejo.

Trujillo Lavao, Juan Miguel   19:52
That's up.

Carrillo Leon, Juan Andres   19:53
Sí, yo lo actualicé varias veces.

Trujillo Lavao, Juan Miguel   19:54
Un.
No.

Gualdron Romero, Javier Leonardo   20:05
Lo que hicimos fue reconstruirlo, mejorarlo, automatizarlo y entregarlo en tiempos mucho más razonables. Y eso diariamente se está mejorando. Digamos que hay un equipo aquí propendemos por el desarrollo colaborativo. ¿Qué quiere decir eso? Que ustedes como áreas de negocio pueden desarrollar, nos pasan a nosotros desarrollos, pasa como un check de requerimientos mínimos y nosotros lo podemos productivizar.

Trujillo Lavao, Juan Miguel   20:14
El.

Gualdron Romero, Javier Leonardo   20:28
Listo, eso, si ustedes lo quieren hacer, también lo pueden hacer si desarrollan productos de datos y ahí nació.

Carvajal Jaramillo, Karen Andrea   20:34
Que eso, disculpa Javier, te interrumpo que de pronto esa sería la invitación, Juan y Miguel, si de pronto ustedes, no sé, desarrollan simplemente una vista, sean consultas o lo que necesiten, no sé, para alimentar tableros para sus procesos y demás.
Pues esto va a quedar dentro del sandbox por un tiempo limitado. Como ustedes saben, usted tiene una política, pero si no se envía a productivizar se va a eliminar. Sí, en este momento tenemos 9 meses para que puedan generar todo el desarrollo, pero la idea es que esto no se vuelva un liberty pruebas actuaría, sino que todo.

Trujillo Lavao, Juan Miguel   20:55
Cancel.
A.
Me paro de desactivar.
What about you?
Thank you.
¿Qué?

Carvajal Jaramillo, Karen Andrea   21:12
digamos que quede dentro de los esquemas generales para que no se pierda el trabajo que ustedes hacen y podamos automatizar ese desarrollo y no quede ahí como eh una una responsabilidad de estarle dando clic y demás además que también cuando pasan aquí el equipo de ingeniería hace un trabajo de revisar y de revisar como el código y optimizarlo

Trujillo Lavao, Juan Miguel   21:19
Te lo veo.
No.

Carvajal Jaramillo, Karen Andrea   21:33
Para que esas consultas pues queden lo mejor hechas posible.

Trujillo Lavao, Juan Miguel   21:34
Que me da pena.

Gualdron Romero, Javier Leonardo   21:38
Listo, entonces aquí llegamos al a lo que se desarrolló. Digamos que si ven, dirán, uy, estos locos, a qué hora dieron toda esa vaina. Entonces esa vaina al final se se traduce en una sola vista que ustedes ven. No sé si alguna vez la han consultado, que creo que es esta que está por aquí abajito.

Carrillo Leon, Juan Andres   21:38
It.

Trujillo Lavao, Juan Miguel   21:44
Al.
And this.

Gualdron Romero, Javier Leonardo   21:55
Creo que es esta, creo que es monitor motor full, o sea, esto es el resumen de todo esto que está acá arriba, pero les explico que es lo que está arriba. Al final ustedes seguramente solo van a necesitar esto, pero les voy a explicar lo de arriba por si necesitan.
Esto es un datamar, un datamar, digamos que o sea un data warehouse lo componen muchos datamar y normalmente un datamar apunta a un dominio, básicamente un datamar que es un conjunto de FA y un conjunto de dimensiones que toma sus cubitos y sacas sus cubitos. Este fue el datamar que se construyó, que al final reemplaza el reporte que tú ya sabes que es el.

Trujillo Lavao, Juan Miguel   22:20
Good morning.
Este.
Yeah.

Gualdron Romero, Javier Leonardo   22:31
¿Se fue el monitoreo de autos, qué hicieron ellos acá?
¿Qué hicimos? Porque eso fue un trabajo conjunto. Acá se empezaron a crear Team y FAC, mismo modelo, misma dinámica, mismos nombres, misma estrategia, todo igual, pero ya más enfocado a autos. ¿Entonces qué dijimos? Extrajimos mucha, mucha data de autos y empezamos a calcular cosas propias de autos. Por ejemplo, la marca no es renovado.

Trujillo Lavao, Juan Miguel   22:38
Yeah.
Ya.
No sé.
Pepe.
Es.
Claro.

Gualdron Romero, Javier Leonardo   22:55
Entonces tenemos una dimensión que dice la marca no renovado. Esta marca no renovado está muy buena porque ya está certificada por pricing y yo creo que es parte de las cosas que yo sé porque tengo una bolita mágica que ustedes la van a usar y la van a necesitar y la marca está muy buena. Tiene una lógica que de modo es bastante compleja, pero funciona.

Carrillo Leon, Juan Andres   23:06
¿Operaciones, qué más usamos?

Trujillo Lavao, Juan Miguel   23:09
A.

Gualdron Romero, Javier Leonardo   23:14
Funciona, tenemos por aquí.

Carrillo Leon, Juan Andres   23:15
Sí, porque también nos piden los de nuevo y renovo.

Gualdron Romero, Javier Leonardo   23:19
Exactamente, pero hay un pero que se los voy a contar para que lo tengan ahí en el radar. Están por aquí los cálculos de expuesto, creo que están por acá. Mira, aquí está el expuesto, entonces aquí hay una FAC para el cálculo expuesto. Tú me lo mencionaste, ahoritica cuando estaba hablando, aquí está la FAC expuesta, esta está solamente para out, ¿no?

Trujillo Lavao, Juan Miguel   23:33
Para.

Gualdron Romero, Javier Leonardo   23:38
Tengan eso ahí en el está también. ¿Qué cosa sé que usted le sirve?

Carrillo Leon, Juan Andres   23:45
Ahí vengo.

Gualdron Romero, Javier Leonardo   23:47
El devengo sí está porque al fin y al cabo el devengo, inclusive de pronto está hasta aquí adentro, porque el devengo se calcula basado el expuesto, que es la multiplicación del expuesto por la prima. Una está el erm, sí, este es el este es el devengo, o sea que se llama como erm premium, que es como lo que me gané, lo que devengué. Básicamente está aquí también.

Trujillo Lavao, Juan Miguel   23:51
Es una.
That's what I'm not.
I can.
That.

Gualdron Romero, Javier Leonardo   24:09
Aquí autos tiene una particularidad de que hay datos que son propios de ellos, ellos compran datos o compraron datos o tienen datos o son cosas que yo los uso y son todas estas.

Trujillo Lavao, Juan Miguel   24:12
Okay.

Carrillo Leon, Juan Andres   24:18
También el juego pasa cuando.

Gualdron Romero, Javier Leonardo   24:20
Ese sí es más general, digamos que hay un código fasecolda compañía, pero aquí tenemos uno que lo llamaron la guía fasecolda.

Carrillo Leon, Juan Andres   24:21
Young.

Trujillo Lavao, Juan Miguel   24:22
No.

Carrillo Leon, Juan Andres   24:22
Sí.

Gualdron Romero, Javier Leonardo   24:28
La guía fase colda la cargamos mensualmente, se carga antes de que se corra el es parte de los requisitos para que se para que se corra el modelo y debe estar por acá. No sé si tú la viste o la nombraste, pero yo estoy seguro que está por acá porque mira, acá está esta es la guía fase colda, esa se carga mensualmente, ¿no? Entonces por ahí si nos manda el archivo se carga mensualmente para que cuando se corra el modelo toda esa data esté.

Trujillo Lavao, Juan Miguel   24:30
Claro que lo que.

Carrillo Leon, Juan Andres   24:36
Thank you.
O sea, el.

Trujillo Lavao, Juan Miguel   24:42
Y.

Carrillo Leon, Juan Andres   24:45
David, David Francisco.

Trujillo Lavao, Juan Miguel   24:47
Claro.
La.

Gualdron Romero, Javier Leonardo   24:52
Y bueno, aquí ya eso fue muy por encimiento, ustedes pueden entrar más a detalle.

Trujillo Lavao, Juan Miguel   24:55
Mira, ahí qué opina, hay un histórico, hay un histórico de San Guía Fa Secolda como a 345346.

Carrillo Leon, Juan Andres   24:55
Salud.
Esa era la prueba que quería para saber el castillo.

Gualdron Romero, Javier Leonardo   25:00
sí.
Yo sé que nosotros la cargamos mensualmente, o sea, cada mes nosotros cargamos y le hacemos una. Ahora, algo muy importante cuando vayan a usar el modelo, el modelo tiene unas banderas. ¿Qué quiere decir eso? Una bandera me marca el último registro actualizado o el último registro válido.

Trujillo Lavao, Juan Miguel   25:18
What?
Man.

Gualdron Romero, Javier Leonardo   25:23
¿Qué pasa? Vamos a poner un ejemplo, ustedes van y consultan la DIM de la DIM de vehículo, un ejemplo como bien facilongo está aquí la de un vehículo y resulta que ustedes de un vehículo van a encontrar muchos registros, van a decir, oh, my, ¿por qué encuentro de este de este vehículo en muchos registros? ¿Por qué el vehículo pudo tener cambios en el tiempo?

Trujillo Lavao, Juan Miguel   25:24
Toma.
And.
So.
Hello!

Gualdron Romero, Javier Leonardo   25:45
No es que pase mucho, pero pasa que cambiaron el color, que cambiaron X parámetro, que cambio el precio, que cambio, bueno, tiene cosas exactamente. Existe una, bueno, el remodelo no es que cambia mucho, pero puede cambiar. No existe una un campo que se llama current record.

Trujillo Lavao, Juan Miguel   25:46
No.
Es excepcional.

Carrillo Leon, Juan Andres   25:51
Modelo.
Denman.

Gualdron Romero, Javier Leonardo   26:04
Este campo está en todas las tablas del esquema general, es como una regla para nosotros tener ese current de correo. ¿Qué quiere decir el current record flag? Que no lo veo.
No lo veo en este momento, no lo veo en este momento.
Uy chica, porque por aquí es tarde.

Trujillo Lavao, Juan Miguel   26:21
Y.

Gualdron Romero, Javier Leonardo   26:24
La vez pasada también puse a buscarlo en esta es el ejemplo más rápido, pero es más difícil encontrarlo.

Carrillo Leon, Juan Andres   26:26
Ahí lo vi, está abajo, está abajo, yo lo vi, está más abajo.
Yes.

Gualdron Romero, Javier Leonardo   26:36
El vehículo.

Trujillo Lavao, Juan Miguel   26:38
Ah sí, ahí está por ahí.

Carrillo Leon, Juan Andres   26:39
Estamos por ahí.

Gualdron Romero, Javier Leonardo   26:42
Aquí está listo. Ese campo lo tienen todo nuestro modelo, todo nuestro modelo y es funcional, depende de la necesidad. Si tú quieres traer el dato más actualizado del vehículo, current record fax igual a uno.

Trujillo Lavao, Juan Miguel   26:48
Te enviar mestigo, chao.
¿Y por qué no?

Gualdron Romero, Javier Leonardo   26:58
Punto, si vamos a la INRIS que tiene todos los movimientos de una póliza, si yo quiero traer el último movimiento, corre el recortrac igual a uno. Si yo voy a la fact transaction movement y quiero traer la el último movimiento transaccional que tuvo esa póliza, corre un recortrac igual a uno. Listo, entonces esa es una forma chévere.

Trujillo Lavao, Juan Miguel   27:09
Yes, that's not this one.

Gualdron Romero, Javier Leonardo   27:17
Para filtrar, digamos, no es un invento ahí que se hizo, que pues ha sido de mucha autoridad, sobre todo cuando tiene el último movimiento. Bueno, cuando piden lo último en guaracha, como dicen por ahí. Aquí también se trató de tener ese esa marca. Digamos que tratamos de dar esas buenas prácticas de que la.

Trujillo Lavao, Juan Miguel   27:21
Es.
Hello.
In.

Gualdron Romero, Javier Leonardo   27:36
archivo de fase colda cargado eso es más fácil porque puede ser o por fecha no digamos que el último es el del mes pasado y es una dinámica que estamos tratando de llevar en todas las tablas para qué simplemente es como una guía para cuando quieran hacer filtros pues igual a uno y ya saben que tiene el último el último dato
¿Qué tenemos aquí? También datos, lo que yo les decía, datos que no se mueven en el tiempo, o sea, son datos estáticos. Ese PC es dato estático. Esos son datos que allá ellos en algún momento tenían guardado, que usaban para sus modelos para el de monitoreo Excel, digámoslo así.

Trujillo Lavao, Juan Miguel   28:13
Pues.

Gualdron Romero, Javier Leonardo   28:15
Los cargamos nosotros aquí a la base de datos, con eso todo el mundo los puede usar y no se quedan en un Excel. Digamos que la cosa del Excel lo estamos tratando de evitar al máximo. Es que entre más datos tengamos aquí cargados, pues uno democratizamos los datos porque no se queda en el dueño del Excel sino se queda abierto para todas las personas y 2 por orden también me parece que es una muy buena para ti.

Trujillo Lavao, Juan Miguel   28:26
Te valido.
Te decía, ya.

Gualdron Romero, Javier Leonardo   28:35
¿Cómo más está ahí?

Trujillo Lavao, Juan Miguel   28:35
Digamos, ahí hay una que dice, ay, se me perdió, decía como intermediario, comisión allá intermediario, comisión. Eso puede ser las comisiones, el porcentaje de comisiones que se lleva cada intermediario.

Gualdron Romero, Javier Leonardo   28:49
Pregunta difícil, déjame mirarlo.
Segunta difícil.
Ya miramos igual todo esto es auto, no cualquier cosa es autos por el nombre, es más como un comodín de tabla. Ay, espera que me traje, no, sí, está bien.

Trujillo Lavao, Juan Miguel   28:59
Primero.
Sí, ya no entiendo.
Y así, no sé.

Gualdron Romero, Javier Leonardo   29:08
Igual si ustedes quieren saber algo más técnico, digamos que nosotros conocemos mucho estos modelos, pero las entrañas, las entrañas, a menos de que tengamos una situación de un lío que nos toque meternos, pues nos metemos. Normalmente los chicos que se arruinan son muy buenos. Entonces, pues le podemos preguntar a ellos: ¿Existe un repositorio? Si ustedes quieren, les puede brindar el repositorio para que entren y averigüen la documentación.

Trujillo Lavao, Juan Miguel   29:09
Amigos.
Y.
A.
Sí.

Gualdron Romero, Javier Leonardo   29:33
Sobre todo eso lo empezamos a hacer, esas prácticas empezaron ahora que a ustedes les puede impactar, no, porque digamos que los dueños de esto es pricing y móvil y ellos hacen movimientos todo, pues todo el tiempo. ¿Qué fue lo que lo que se incluyó últimamente? Que todo movimiento, todo cambio que hagan lo dejen documentado. Entonces si a ustedes algo les cambia, pues pueden ver la documentación. Si es que cambie el modelo, bueno, porque cambio y todo eso. bueno.

Trujillo Lavao, Juan Miguel   29:34
Home.
Ya.
With his name.
No.

Gualdron Romero, Javier Leonardo   29:56
Ahí estará documentado y si no, pues tocaría descargarlo con Johana. Esto es lo que veo ahí, no sé que sea.
Recibido un porcentaje de comisión por acá en algún lado.

Trujillo Lavao, Juan Miguel   30:05
No, no.
Ahh, entonces.

Gualdron Romero, Javier Leonardo   30:12
Valor prima, no sé qué.

Trujillo Lavao, Juan Miguel   30:13
El 500 cero cero del 5.1 creo que dice que es.
Puntaje sobre codicia.

Carrillo Leon, Juan Andres   30:19
Pues ese cero de 19.

Gualdron Romero, Javier Leonardo   30:22
Escucha, estoy de verdad que yo.

Trujillo Lavao, Juan Miguel   30:24
Es que dice puntaje, pero ese es el IVA.

Carrillo Leon, Juan Andres   30:24
Creo que es el 0,19.

Carvajal Jaramillo, Karen Andrea   30:27
Sí, ese es porcentaje, es porcentaje sobre comisión.

Gualdron Romero, Javier Leonardo   30:28
Este.

Carrillo Leon, Juan Andres   30:28
Okay.
De sobre comisión.

Trujillo Lavao, Juan Miguel   30:31
Exploring.

Gualdron Romero, Javier Leonardo   30:33
Ese del IVA y ese sería como lo bueno, igual esto, todo esto, mis recomendaciones, pero yo no me la sé todas, o sea, manden del modelo, yo sí, se lo digo a ti al revés, pero ya el detalle en caso de cuando son desarrollos colaborativos, pues nos repetimos a la persona que lo desarrolló igual en algunas cosas nos podemos ayudar, en otras no.

Trujillo Lavao, Juan Miguel   30:38
Y ya.
No.
Este Estos estas tablas están conectadas a yaxis, digamos como para traer información de yaxis.

Gualdron Romero, Javier Leonardo   30:57
Yeah.
Gran parte de estas tablas salen de el modelo general, lo que hacen ellos es extraer la parte de autos y empezar a crear cosas nuevas.
De I axis no creo que salga mucho directamente el core de I axis. Digamos que es algo que es una práctica que estamos evitando que suceda. ¿Para qué? Para cuando llamamos la fuente única, la verdad. Si todos tomamos un mismo modelo, pues todos vamos a tener los mismos datos. Si tú sacas datos de I axis, tú puedes hacer tus datos y creas un silo.

Trujillo Lavao, Juan Miguel   31:20
Yeah.

Gualdron Romero, Javier Leonardo   31:29
Y esa verdad empieza a pelear con la única fuente, la verdad, digámoslo así, entonces tu verdad puede ser distinta a otra verdad que estamos tratando de hacer tener una sola verdad y todos regimos por la misma. Por eso los números a todos nos dan lo mismo, ¿no?

Trujillo Lavao, Juan Miguel   31:39
And.

Gualdron Romero, Javier Leonardo   31:43
¿Alguna otra pregunta que tengan hasta el momento?

Carrillo Leon, Juan Andres   31:47
Y vamos, si yo quisiera buscar salvamentos, puedo buscar los de arriba a ver si existiera algo que se llamara así.

Trujillo Lavao, Juan Miguel   31:47
What's yourself come in?

Gualdron Romero, Javier Leonardo   31:52
Yeah.

Trujillo Lavao, Juan Miguel   31:52
Algo que me llamaras.

Gualdron Romero, Javier Leonardo   31:55
Salvamentos, creo que salvamentos no tenemos todavía toque de buscar en las **** porque al final cosas como más de siniestros.

Trujillo Lavao, Juan Miguel   31:55
Sí.

Carrillo Leon, Juan Andres   31:56
O recoders.

Trujillo Lavao, Juan Miguel   31:57
Face.

Carrillo Leon, Juan Andres   32:04
Oh.

Gualdron Romero, Javier Leonardo   32:05
Eso es como de siniestros.

Carrillo Leon, Juan Andres   32:06
De como un tipo de transacción.

Trujillo Lavao, Juan Miguel   32:06
Thank you.

Gualdron Romero, Javier Leonardo   32:08
Sí, exacto, no estoy seguro que lo tengamos, no estoy muy seguro, pero pues podemos buscarlo, no ya podemos buscarlo y mirar a ver si lo tenemos.
¿Qué otras cosas les digo que esto tiene? Bueno, tiene la dimensión de calendario, es una dimensión chévere porque pues ahí tú ves el periodo contable los meses, si es lunes, si es martes, si es miércoles, bueno, si es un trimestre, cuatrimestre, bueno, un poco de cosas. Eso sobre todo es muy útil cuando construyen tareros en el tiempo, no para saber la temporalidad de todo lo que tú quieras, pues tú vas a la en calendario.
Tenemos dimensiones de apoyo, por ejemplo, esta departamento. Digamos que parte de los problemas que hemos encontrado es que cuando traes el departamento, la ciudad a veces viene mayúscula, a veces viene.

Trujillo Lavao, Juan Miguel   32:47
Listo.
Y.

Gualdron Romero, Javier Leonardo   32:53
Santa Fe, Bogotá, Bogotá. Bueno, viene en formas, si tú cruzas por el código de apartamento acá, pues tú para todos tus tableros y todo lo que tú vas a tener el mismo nombre. Listo.

Trujillo Lavao, Juan Miguel   32:56
Con eso.
They do.

Gualdron Romero, Javier Leonardo   33:02
También tenemos, bueno, aquí está la de calendario de en ciudad departamento.

Trujillo Lavao, Juan Miguel   33:06
Pues no.
Okey, creo.

Gualdron Romero, Javier Leonardo   33:11
Vemos que esas son como las principales que tienen esa casuística.

Trujillo Lavao, Juan Miguel   33:17
Con mi público.

Gualdron Romero, Javier Leonardo   33:18
¿Hasta ahí cómo vamos?

Carrillo Leon, Juan Andres   33:21
Bien.

Trujillo Lavao, Juan Miguel   33:21
Lo recurso en estado.

Gualdron Romero, Javier Leonardo   33:22
Bien, listo. ¿Qué más preguntas tenemos acerca de y de lo que ustedes van a hacer como para ir aterrizando un poquitico toda esta cháchara que les he estado estado echando?

Trujillo Lavao, Juan Miguel   33:24
Y.
Aquí.
Calling.
En.

Carrillo Leon, Juan Andres   33:32
Pues aquí ya es identificar cuáles son los packs de los que nos vamos a colgar, cuáles DIM vamos a usar y ya empezar a armar la vista.

Gualdron Romero, Javier Leonardo   33:42
Listo, vale, cosa importante, súper importante. ¿Cómo cruzo yo las tablas y las vistas? En un principio, cuando nació esto, esto nació de GD, de Liberty, por allá, cuando nos íbamos a unificar con el mundo entero. Entonces ellos dijeron, no creemos un modelo con llaves dinámicas para que no vayamos a tener el problema de que si una política existe en un.

Trujillo Lavao, Juan Miguel   33:47
I'm in.
Cuando.
Ese.

Gualdron Romero, Javier Leonardo   34:03
Una policía existe en un país, pues en el otro día existe la misma póliza y entre países nos nos nos pidemos las mangueras. Acá se inventaron un tema de llaves dinámicas, llaves dinámicas son que llaves que se mueven en el tiempo.

Trujillo Lavao, Juan Miguel   34:07
¿Qué?
No, por favor, no.

Gualdron Romero, Javier Leonardo   34:16
Esas se mueven en el tiempo, tú no las puedes quemar dentro del código porque esa se va a mover, se va a mover, pero es la que te va a permitir empezar a conectarte con el mundo, por decirlo así. Si tú vienes por acá a.

Trujillo Lavao, Juan Miguel   34:22
Esteban.
And.

Gualdron Romero, Javier Leonardo   34:29
La fa, esta miremos esta que es como como la que todos conocemos. Entonces todo esto que dice seca son esas llaves, técnicamente eso le llaman que son crucadas que fueraneas que no sé qué, eso aquí quitémonos entonces apellidos, eso es lo que nos permite cruzar hasta ahora entre ellas. Ahora, ¿cómo la cruzarías si yo te digo o k por aquí, por aquí, por aquí, tengo una vez una que utilicemos alto?

Trujillo Lavao, Juan Miguel   34:30
Bueno, Dios mío.
Sí.
Mhm.

Gualdron Romero, Javier Leonardo   34:54
Esta, si tú tienes esta llave, ¿con qué cree que la puedes cruzar? A ver.

Trujillo Lavao, Juan Miguel   34:55
Juan.
Yeah.

Carrillo Leon, Juan Andres   35:03
Con el número de póliza no.

Trujillo Lavao, Juan Miguel   35:04
Con la dimensión, con la dimensión de riesgo.

Gualdron Romero, Javier Leonardo   35:07
Exactamente, listo, ya saben todo, se acabó esto, cerremos. Eso es lo más importante. Ahora que hay más formas de hacerlo. Sí, digamos que nosotros a partir de que adoptamos el de que nosotros aquí en Colombia cogimos el modelo, porque esto era lo que nos decían los gringos que teníamos que hacer. No hay ningún gringo por acá.

Carrillo Leon, Juan Andres   35:08
Okay.

Carvajal Jaramillo, Karen Andrea   35:08
Yeah, correct.
Ya con eso ya pueden, mejor dicho, armar.

Trujillo Lavao, Juan Miguel   35:15
Mhm.
Yeah.
Es más.

Gualdron Romero, Javier Leonardo   35:26
Que se vaya a sentir ofendido, entonces nosotros lo que hicimos fue colombianizarlo. ¿Qué significa colombianizarlo? Crear llaves lógicas que ustedes también puedan manejar. ¿A qué me refiero que una llave lógica? Lo pueden hacer por esa seca y está bien y va a funcionar, pero también lo pueden hacer creando llaves. Por ejemplo, si yo creo la póliza certificado, yo creo esa póliza certificado.

Carvajal Jaramillo, Karen Andrea   35:28
Es pronto.

Trujillo Lavao, Juan Miguel   35:31
No.
Okay.
Es.
David.

Gualdron Romero, Javier Leonardo   35:46
Y la cruzo con la póliza certificada de la de Enrix te va a funcionar y te va a funcionar. ¿Qué te recomiendo por performance por rendimiento utilizar la seca? Digamos que esto tiene una estructura, o sea, al ser una base de datos en Redshift columnar, que eso es puro bla bla bla en términos españoles, es que mejora el rendimiento de consulta.

Trujillo Lavao, Juan Miguel   35:49
Best.

Gualdron Romero, Javier Leonardo   36:05
Vemos que eso está hecho para que el rendimiento en consulta sea rápido. Listo, igual. ¿Cuál es el riesgo que tenemos acá? Digamos que son los riesgos de abrir la puerta, que es lo que estamos haciendo, democratizar los datos es abrir la puerta porque ustedes los usen, que alguien haga una query mal hecha y nos bloquee el CDP. Eso puede pasar, eso puede pasar, nos ha pasado y estamos mirando estrategias para que eso no pase. Ojalá no sean ustedes, por favor.

Trujillo Lavao, Juan Miguel   36:17
Video.
Good.
Yeah.

Gualdron Romero, Javier Leonardo   36:29
Sino yuca, entonces.

Carrillo Leon, Juan Andres   36:29
I think.
Ajá.

Carvajal Jaramillo, Karen Andrea   36:31
Y de pronto ahí, Javi, cuando tú les decías, no sé si quedó claro el término, pues de las llaves dinámicas y que no las podemos quemar. Sí, o quieren ver un ejemplito porque sí.

Gualdron Romero, Javier Leonardo   36:42
Meter en el código.

Trujillo Lavao, Juan Miguel   36:44
¿Emara qué se refieren como a usar demasiado?

Carrillo Leon, Juan Andres   36:44
Sí, mejor.

Carvajal Jaramillo, Karen Andrea   36:47
No, entonces qué sí.

Gualdron Romero, Javier Leonardo   36:48
No meter dentro del código, o sea que tú dentro del código, ahí donde se cae es igual a tal número, eso no lo podemos hacer.

Carvajal Jaramillo, Karen Andrea   36:52
Uh-huh.
Yo no puedo sacar y decir exactamente mejor dicho, generalmente cuando uno hace joins y esto no nos vamos a teoría SQL. Entonces nosotros si quisiéramos traer, hagamos ese ejemplito, Javi, de cruzar con el riesgo, vamos a traernos algún valor para esta FAC.

Trujillo Lavao, Juan Miguel   36:59
Yeah.
Pero.

Gualdron Romero, Javier Leonardo   37:06
Yeah.

Trujillo Lavao, Juan Miguel   37:06
No.

Carvajal Jaramillo, Karen Andrea   37:13
Vamos a cruzar la transacción móvil y vamos a traer algún valor del riesgo.

Gualdron Romero, Javier Leonardo   37:15
Alright.
Pero aquí está link.

Trujillo Lavao, Juan Miguel   37:25
Bueno.

Carvajal Jaramillo, Karen Andrea   37:25
I.

Gualdron Romero, Javier Leonardo   37:27
Ya estoy por acá, tengo ya.

Carvajal Jaramillo, Karen Andrea   37:27
el dato per se de la SK para cualquiera de esas transacciones no puede quedar quemado cuando nosotros decimos quedar quemado es decir exactamente el número de la SK porque esto es Dinámico es decir era lo que explicaba Javi que esto se está moviendo constantemente el tema de las llaves
Entonces no si yo tengo una SK que corresponde me invento algo una póliza 10 20 Sí nosotros dijimos Ah no pues la SK de esto es eh 9 ese 9 no puedo dejarlo ahí dentro del código en el Inner sino que tengo que dejar solamente el el on con la SK para que cruce
No sé si sí, no, yo creo que eso es más fácil de ver con un ejemplo, porque cierto.

Trujillo Lavao, Juan Miguel   38:12
Sí, total, sí.

Gualdron Romero, Javier Leonardo   38:16
Estoy buscando una mano de cuero y no se para usar ahora.

Carrillo Leon, Juan Andres   38:19
No, pero básicamente es que si lo que más, ese dato no se va a actualizar nunca.

Trujillo Lavao, Juan Miguel   38:19
Pero.

Gualdron Romero, Javier Leonardo   38:22
Exactamente, sí, esta no he dicho, igual es algo que siempre provendamos, ¿no? O sea, por favor, traten, traten. No le digo que no lo hagan nunca porque a veces necesita de quemar datos dentro de dentro de los códigos. Digamos que es un es por prácticas, ¿no? Y seguramente si van a productivizar algo que tenga datos quemados, pues nosotros vamos a decir lo sentimos, pero es que no.

Carvajal Jaramillo, Karen Andrea   38:22
Exactamente, no va a traer la información, sí.

Carrillo Leon, Juan Andres   38:24
Sí.

Trujillo Lavao, Juan Miguel   38:33
Call.
I don't.

Gualdron Romero, Javier Leonardo   38:46
Hay otra forma de hacerlo y seguramente les vamos a decir cómo se debe hacer. Tampoco es que lo vamos a decir, no se puede, nos vamos a decir tirados, no les indicamos o tal vez existe alguna alguna nueva dimensión, alguna cosa que nos hayamos inventado para decirles oiga, no hágalo así, que así es mucho mejor.

Trujillo Lavao, Juan Miguel   38:46
Así es.
Ay.
Canción.
It.

Carrillo Leon, Juan Andres   39:00
Digamos la tabla de ciudades de códigos de ciudades, eso no está quemado porque eso no se actualiza.

Trujillo Lavao, Juan Miguel   39:00
Sí.

Gualdron Romero, Javier Leonardo   39:03
Hola.
La tabla de ciudades, por ejemplo, ya no tiene seca. Digamos que la tabla de ciudades eso fue cuando ya nosotros tomamos todo. Ahí sí, eso pues sí.

Trujillo Lavao, Juan Miguel   39:05
Yeah.

Carvajal Jaramillo, Karen Andrea   39:13
Por código y esa sí no va a cambiar, sí, esa sí no.

Gualdron Romero, Javier Leonardo   39:16
Exactamente, entonces, pues igual, o sea, esto es traten de, digamos, yo entiendo, yo me pongo en la posición de IT, sí, es que eso está mal técnicamente porque eso no debería nunca, pero me voy para negociar y digo, pero es que también para que les voy a complicar la vida. Hombre, si yo manejo autos, pues yo quemo.
Mi SBU auto dentro del cobro y ya no pasa nada y está bien, es como eso, es una recomendación también.

Carvajal Jaramillo, Karen Andrea   39:41
Eso trae problemas, ¿no? Porque si llega a cambiar alguna SBU y yo las tengo quemadas dentro del código, pues nunca se va a actualizar. Sí, es decir, si yo quemé la SBU 10, la 20, pero no tengo una tablita donde ahí sí lleguen directamente todos los cambios que hacen, pues no se actualiza.

Gualdron Romero, Javier Leonardo   39:43
Exactamente.
Eso es importante.

Carrillo Leon, Juan Andres   39:51
Sí, exacto.

Carvajal Jaramillo, Karen Andrea   40:00
Es por eso que nosotros decimos no quemen, no quemen datos dentro del código.
Luis.

Gualdron Romero, Javier Leonardo   40:15
Nosotros les enseñamos cómo hacer para que sus contraseña no queden ahí quemar entre los códigos porque apenas lo vamos a pasar de producción yuca esos soles se van a trabajar en Python más que todo si van a trabajar SQL puro no van a tener ese problema.

Trujillo Lavao, Juan Miguel   40:29
Stop!

Gualdron Romero, Javier Leonardo   40:29
Oiga, qué mano de Queris tengo y llevo rato sin hacer una consulta en las transaccionales.
Hagamos una de cero.

Trujillo Lavao, Juan Miguel   40:47
What is up?

Gualdron Romero, Javier Leonardo   40:48
Tengamos una de cero en la rango de cero, como esta señora.
¿Es de las más usadas, no? La imx tiene una particularidad porque es la que más usas se los voy a contar. Cuando ustedes consultan la transaccionalidad, solo van a encontrar movimientos transaccionales. Entonces, si solo encuentran movimientos transaccionales que no van a encontrar lo que no es transaccional y lo que no es transaccional, ¿dónde si lo van a encontrar? Acá en la imx.
Me refiero a que cambió la sucursal.
Por ejemplo, no sé si se pueda pagar, pero sí, entonces si cambio la sucursal es un movimiento no transaccional que no van a encontrar en la transacción movimiento, pero aquí en está la de Inbrex sí van a encontrar absolutamente 2. Sí que mueve prima o que cancele o que genere o que renueve o que agregaron un amparo, entonces eso.

Carrillo Leon, Juan Andres   41:28
Transaccionales que genere prima.

Trujillo Lavao, Juan Miguel   41:28
Translaciones.

Carrillo Leon, Juan Andres   41:31
Okay.
Okay.

Trujillo Lavao, Juan Miguel   41:37
Y me lo que dice.

Gualdron Romero, Javier Leonardo   41:37
Todo lo que mueva plata, básicamente haga cuenta cuando uno va en cajero, yo hago una, es una transacción, entonces aquí también y con sin estos igual todo lo que es transaccional y en general para la vida, las fax son así, eso es.

Carrillo Leon, Juan Andres   41:39
Okay.

Trujillo Lavao, Juan Miguel   41:41
That's what I'm doing.
No.

Gualdron Romero, Javier Leonardo   41:52
Pura teoría es mi, pues a mí me es la forma que me lo aprendí en su momento y yo hablo mucho y no hago nada, entonces espérate.

Trujillo Lavao, Juan Miguel   41:54
O.

Gualdron Romero, Javier Leonardo   42:03
Seguramente van a llegar a este nivel cuando empiecen a cacharrear, tener como 50 pestañitas y cada 1.1 cosa distinta, y después vas a ver y te vas a olvidar.
Aquí tenemos la de imbricks. ¿Qué otras recomendaciones doy? Si encuentran lentitudes, a veces no siempre es el de Bible. A veces el de Bible yo no sé qué le da, pero como que se chifla y le da por ponerse lento.
A veces no, no siento.

Carrillo Leon, Juan Andres   42:36
Y vamos hoy, nosotros tenemos un chat para los incidentes de Power Bi que se ponen lentos y hoy Andrea escribió que el Data Warehouse estaba como tenía como su vaina.

Gualdron Romero, Javier Leonardo   42:36
Aquí tenemos.
Ese dato warehouse es distinto.

Carrillo Leon, Juan Andres   42:49
Ahí sí, exacto, entonces ahí es otro tema, sí.

Gualdron Romero, Javier Leonardo   42:50
Esa es otra, otra es otra, esa es otra infraestructura.

Carrillo Leon, Juan Andres   42:56
Pero ahí, digamos, ellos no nos podrían ayudar con eso. Digamos que acá en el deber se ponga lento, ellos no nos podrían ayudar ahí para que.

Trujillo Lavao, Juan Miguel   42:56
Pero.

Gualdron Romero, Javier Leonardo   43:04
A bueno, sí hay un soporte de Deviber. Bueno, aunque es que Deviber es como la aplicación per se, no digamos que Deviber sí es más con la mesa de ayuda.

Carrillo Leon, Juan Andres   43:12
Sí.

Gualdron Romero, Javier Leonardo   43:17
Pero si es el CDP, si ya es con la parte de nosotros que administramos el CDP, contar un poco más la infraestructura del CDP, pero si es con otro porque ahora somos ITE y a veces se me olvida.

Trujillo Lavao, Juan Miguel   43:17
Y.

Gualdron Romero, Javier Leonardo   43:31
Entonces, aquí le damos el SDK, creo que es la llavecita así.
¿Cómo es que la llave? Bueno, aquí también pueden para el de Viper pueden jalar cosas, ¿no?
Y lo bueno del deber es que a veces te ayuda con predecir las variables. Eso también es como chévere, tiene sus cositas. Igual es un es una interfaz, no tiene todos sus contra.
Aquí está Team.
Pues venimos acá, le dijimos que esto es igual a esto.
Igual a de punto nivel de granularidad, tema importante, el nivel de granularidad de la FAC va hasta amparos.
Si buscan cosas por recibo, que es un nivel de granularidad mucho más abajo, no si van a encontrar cosas, pero no es el nivel de granularidad. O sea, nosotros vamos a estampar de ahí para arriba. Ustedes pueden empezar a agrupar, no dicen, quitemos los amparos y sumemos y ahí sale la prima. Sí, bien, listo para que lo tengan ahí en cuenta el nivel de granularidades.
Súper importante.
Esta cosa funciona.
Por favor, cuando hagan query siempre poner un limit o where o filters. No digamos que lanzar queries así súper súper pesados van a morirse. Aquí dice algo mal.
¿Qué hice mal, tu no un limit 10 simplemente, un limit 10 no estoy haciendo nada, a ver, a on, listo ya?

Carvajal Jaramillo, Karen Andrea   44:59
¿Sí, Javi, por qué? ¿Qué estás trayendo? ¿Lo estás cruzando tú a ver?
Ajá.

Carrillo Leon, Juan Andres   45:11
Hola Juan, Guau, ya hice averiguación al área legal, ellos dicen todo bien, primero ellos que yo es primero que todo.

Trujillo Lavao, Juan Miguel   45:12
Stop!
Okay.

Gualdron Romero, Javier Leonardo   45:14
Listo.

Trujillo Lavao, Juan Miguel   45:16
Sí.

Gualdron Romero, Javier Leonardo   45:17
Y así, pues básicamente es como la dinámica, ya entrar, hacer quitos y todas esas cosas. Bueno, ya les dejo un poquito que experimente.

Carrillo Leon, Juan Andres   45:24
Sistema financiero, bueno, que la compañía no presente, excedente en la operación del rango, en el periodo que estamos preguntando, eso es lo primero y lo más importante es que no se llevó a cabo ninguna notificación en la ADRE.

Trujillo Lavao, Juan Miguel   45:26
Digamos, yo tengo el usuario del CDP, pero creo que no tengo acceso a las todas las tablas del Data Warehouse. Ahí yo igual puedo llamarlas.

Gualdron Romero, Javier Leonardo   45:37
No.
Acá no nos puede llamar y la idea es no hagamos esos injertos, por favor. Esos injertos no van a ser buenos porque está porque al fin y al cabo están diseñados en idiomas distintos y funcionan distinto, ¿no?

Carrillo Leon, Juan Andres   45:45
Pues te digo que como un resultado positivo y dentro de la regulación, existe una obligación de clase.

Trujillo Lavao, Juan Miguel   45:52
Pero ahí tú no estás llamando algo del data warehouse.

Gualdron Romero, Javier Leonardo   45:55
No, o sea, es esto es CDP, o sea, aquí estoy conectado solamente CDP, o sea, yo no puedo aquí conectar data warehouse con cpy todos felices aquí metidos en una misma sabana, ¿no?

Carvajal Jaramillo, Karen Andrea   45:56
Usted sea de pi.

Carrillo Leon, Juan Andres   45:57
Nothing.

Trujillo Lavao, Juan Miguel   46:00
O.K.

Carrillo Leon, Juan Andres   46:03
Del siguiente periodo por la nomenclatura.

Trujillo Lavao, Juan Miguel   46:05
Lo decía.
O K, lo decía por el nombre de pero sí.

Carrillo Leon, Juan Andres   46:10
TWH.

Gualdron Romero, Javier Leonardo   46:12
Okay, sí, lo que pasa es que CDP es un DWH, básicamente no en la teoría, pero pues como para diferenciar la nomenclatura, sino hablar de los data warehouse, porque sino son data warehouse. Nosotros nos referimos al data warehouse de SQL como data warehouse y este como CDP es un tema de léxico que usamos.

Carvajal Jaramillo, Karen Andrea   46:12
Ah.

Trujillo Lavao, Juan Miguel   46:18
Okay.
A.
O K.

Gualdron Romero, Javier Leonardo   46:31
Porque al final su base es la misma vaina, son tus datauerrados, pero en la práctica para facilidad y para no enredarnos, pues lo llamamos así.
Ahí está pareja, ahí está pensando. ¿Qué otras cosas tienen así como preguntas?

Trujillo Lavao, Juan Miguel   46:44
Paul.
Okay.
No puede ser.

Gualdron Romero, Javier Leonardo   46:48
Dudas está en inglés, digamos que van a encontrar cosas en inglés y en español. Estamos ahí mirando a ver cómo nos quedamos por una línea, porque hay cosas que ya cambiarán, no vamos a poder, pero pues no, tampoco le digo, no un problema, ¿no?

Trujillo Lavao, Juan Miguel   47:00
¿Qué bonito es?

Gualdron Romero, Javier Leonardo   47:04
Igual si tienen cosas que necesitan nuevas columnas, no lo pueden decir a nosotros y nosotros priorizamos y miramos a ver si es factible traerlas.
Sí, digamos que esto no es perfecto y esto va a seguir desarrollándose hasta secula seculón y agrega nuevas variables y axis y agrega nuevas variables a cotizaciones y entra un nuevo producto y esto se mueve full time todo el tiempo. Si ustedes ven cosas que necesitan, que no las tenemos disponibles en el esquema general, pues nos pueden decir ya nosotros miramos la factibilidad y bueno, hacemos un análisis y pues las traemos, no dependiendo de su complejidad.

Trujillo Lavao, Juan Miguel   47:16
Uy.
Starting working.
I want you.

Gualdron Romero, Javier Leonardo   47:39
Y nos llega y vamos a traer, no. Eso tiene un análisis por detrás que tenemos que hacer unas prioridades, pero pues tampoco vamos a decirles que no se puede, porque sí se puede, sobre todo si existe ni axes. Bueno, al tema de los core, muy importante, el tema de los dime.

Trujillo Lavao, Juan Miguel   47:45
Open.
Digamos en ese caso, sí, en ese caso, digamos, para traer sí como los factores de gasto de yaxis por póliza o por intermediario, sería posible.

Gualdron Romero, Javier Leonardo   48:04
Todo es factible, todo es factible, solo que a su debido tiempo y en su debida prioridad. Si existe en Iaxis, si tú me dices, mira, en esta pantalla Iaxis lo tengo, se puede traer. Tú me dices, Javier, mira, aquí veo una pantalla Iaxis que trae este dato y ese dato necesito si se puede traer, si está ahí, si tú lo ves, si se puede traer.

Carrillo Leon, Juan Andres   48:12
Any axis.

Trujillo Lavao, Juan Miguel   48:12
Ya.

Gualdron Romero, Javier Leonardo   48:23
¿Ahora que cuánto nos cueste traerlo? Eso es, pues hay que hacer un análisis, hay que pues todo un proceso. Hay que hacer pruebas porque cualquier cambio que hagamos acá afectamos la compañía. Entonces nos toca ser muy cuidadosos porque ya estamos tomando decisiones sobre algo que no podemos dañar, digámoslo así.

Carrillo Leon, Juan Andres   48:44
O puede que ya esté.

Trujillo Lavao, Juan Miguel   48:44
Ready.

Gualdron Romero, Javier Leonardo   48:44
Pero si existe, se puede dime.

Carrillo Leon, Juan Andres   48:47
O puede que ya esté.

Trujillo Lavao, Juan Miguel   48:47
Good.

Gualdron Romero, Javier Leonardo   48:48
Sí, o puede que ya esté, sí, puede que ya esté, digamos que lo que hemos tratado de hacer es traer lo más grueso, traer lo de siempre, traer lo que más se usa, tal vez como lo que yo diría, como lo normal que piden o lo más grueso que piden, pero ya sí es algo más deterial igual que se puede traer, pero pues con los respectivos cuidados.
En cuanto a la data, yo sé que ustedes pueden identificar bueno, que si es de autos, pues no hay mucho problema, pero bueno, no lo voy a mencionar. Existe una columna que se llama.
Core system o system core, ya me olvido.
Que básicamente lo que te dice ahí es de qué sistema viene.
La data que está que estás viendo.

Trujillo Lavao, Juan Miguel   49:34
Percepción.

Gualdron Romero, Javier Leonardo   49:34
Mi contrario está, pero en malas condiciones hoy.
Michael.

Trujillo Lavao, Juan Miguel   49:43
Five.
Pues Carolina.

Gualdron Romero, Javier Leonardo   49:47
Estoy haciendo cómo se llama, mira, aquí está el color récord que les decía.

Trujillo Lavao, Juan Miguel   49:48
Sí.
Al.
También.

Gualdron Romero, Javier Leonardo   49:57
Aquí están los temas de modalidad, que sé que a ustedes les va a servir un montón que les voy mostrando cositas que nos piden siempre.

Trujillo Lavao, Juan Miguel   49:59
Pick up.
O.
Este.
No arreglando.

Gualdron Romero, Javier Leonardo   50:18
Ya lo sepan, ahí este source nos dice que es de dónde viene la data, si viene de a S 400 o viene de AX que no van a encontrar acá, sí.

Trujillo Lavao, Juan Miguel   50:23
Y.
Yes.

Gualdron Romero, Javier Leonardo   50:30
No lo van a encontrar dentro de este modelo. Estamos habilitando estos datos de otra forma, porque pues sí, ya va de salida y no tiene sentido mover todo esto para meter sí, no lo vamos a hacer, no lo vamos a hacer, pero sí vamos a traer los datos y los vamos a dejar disponibles de forma distinta. No van a ser así como en la factura, vamos a encontrar los movimientos.
No, eso no va a pasar, eso no va a pasar, pero si lo vamos a tener de otra forma y tal vez toca hacer un trabajito un poquitico más denso es que.
¿Ya Modeling lo hizo, no? O sea, ya en el datamar de Modeling, eso ya está allá. Entonces, pues para que tengan eso ahí clarito.

Trujillo Lavao, Juan Miguel   51:08
Las consultas.

Gualdron Romero, Javier Leonardo   51:08
¿Alguna?

Trujillo Lavao, Juan Miguel   51:10
Tienden a ser demoradas porque veo que el límite es 10 y ya lleva 6 minutos corriendo.

Gualdron Romero, Javier Leonardo   51:17
Pues ya llevamos 6 minutos, depende de la consulta, le ponemos un hueso, depende de la consulta, depende del tiempo. Digamos que ahoritica se está haciendo como un tema de calibración de recursos también.
Lo que hemos detectado es que cuando es cierre, por lo menos esta semana, semana pasada, uf, ha sido bastante.
Está por ahí.
Bastante eso en la mañana es mucho más rápido. Esto tiene horarios, digamos que tú si consultas por hablar las 10:00 de la noche no te va a funcionar. Si dejas una consulta que se demore más de tanto tiempo, seguramente se va a cancelar. Tengan eso en cuenta ahoritica dentro de pocos días.
Dentro de pocos días, ahoritica la disponibilidad está hasta las 10:00 de la noche. Dentro de pocos días la disponibilidad del CDP va a estar a las 6:00. ¿Eso qué quiere decir? Que a las 6:00 se corta el chorro y arranca y arranca un tema de actualización. ¿Por qué está pasando eso? Porque la actualización de CDP.

Trujillo Lavao, Juan Miguel   52:09
I'm coming.
Okay.
Esteban.
¿Qué tienes?

Gualdron Romero, Javier Leonardo   52:21
Está quedando muy tarde y necesitamos correrla hacia atrás por un tema de producción de la de todo el tema comercial que necesitan tener sus datos más temprano. Entonces hasta las 6 digamos que va a haber servicio, que después lo vamos a normalizar y va a ser más tarde, sí, pero por ahora ese es el horario.

Trujillo Lavao, Juan Miguel   52:26
I.
Sí.
I think.

Carrillo Leon, Juan Andres   52:37
¿A qué horas apertura en la mañana?

Trujillo Lavao, Juan Miguel   52:38
I que.

Gualdron Romero, Javier Leonardo   52:41
Pues es como a las 5:00 de la mañana más o menos, y tal vez ahoritica se mueva un poquitico más atrás porque se mueve todo, ¿no? Así que a esta edad 10 que digamos que se corta el servicio.

Trujillo Lavao, Juan Miguel   52:48
Yes.
What?

Gualdron Romero, Javier Leonardo   52:54
Y apenas termine el automáticamente.

Trujillo Lavao, Juan Miguel   52:55
Y.
What's that?

Carrillo Leon, Juan Andres   52:59
Se apertura.

Gualdron Romero, Javier Leonardo   52:59
El automáticamente hace apertura exactamente, igual mi recomendación es las mañanas, las mañanas SDP anda relajado.
Súper relajada, ya en las tardecillas, por ahí después de las 10:00 en adelante, ya la cosa es más densa.
Es mucho más densa, como pueden ver en este momento.

Trujillo Lavao, Juan Miguel   53:24
¿Qué?

Gualdron Romero, Javier Leonardo   53:26
A Miguel le muestro el tema del sandbox, cómo funciona el sandbox, porque hay algo muy importante que difiere de pruebas actuaría.
El sandbox es este de acá.
Este señor, ustedes pueden crear los objetos que ustedes necesiten para hacer sus cosas. Aquí hay miles de objetos. Los responsables de los datos que estén ahí es cada uno de ustedes. Si necesitan que alguien más vea sus datos, cada uno de ustedes le tienen que dar permiso a esa persona para que vea los datos que tú estás manejando. Listo.
Que que eso, claro, digamos que si Juan hizo una tabla, uy, que aquí me jodieron Juan Miguel necesita una Juan hizo una tabla que Juan Andrés necesita, necesita usar exactamente. Entonces entre ustedes dicen, oye, ya dame permisos para ver esa tabla que o para validaciones o para cualquier cosa. Entonces ustedes tienen que darse permisos para que puedan acceder a esas tablas de del SAMBUS.

Carrillo Leon, Juan Andres   54:07
Aquí está Juan Pablo y está Juan Esteban.
Perfecto, solamente.
Polification.
Pero.

Gualdron Romero, Javier Leonardo   54:23
Sí, pues que tengan en cuenta que la vida de las tablas en sandbox ahoritica a hoy es de 9 meses. Después de 9 meses, tuki, tuki, luyu, o sea, el dato se se elimina. Si quieren ver, espérate, por aquí yo tengo una cosa, si quieren ver cuánto lleva su tabla ahí, porque seguramente ustedes dirán, uy, no me acuerdo hace cuánto cree esa tabla y no sé si me la van a borrar.

Carrillo Leon, Juan Andres   54:25
Yes.
¿Sabes?
Banco di.
¿Quién, esa chica?
O promoción.
Acepta.
Pero ya no puede.

Gualdron Romero, Javier Leonardo   54:46
Tenemos una acá.

Carrillo Leon, Juan Andres   54:49
Hoy.
De la prueba con la del BFI en ocasiones y ya tengo el rol, es una idea cual es trasladarle en un gira. Entonces yo hablé con la reto. Claro que sí, les colabora, lo tengo mapeada.

Gualdron Romero, Javier Leonardo   54:53
Espero que está muriendo acá está.
Acá tenemos una Mariachi, muy esta, por acá está.
Ay, creo que ya terminó la otra consulta, pero bueno, espérate, se volvió que se hizo.

Carrillo Leon, Juan Andres   55:08
cambiarles a esas chicas, así el el el nuevo rol, con la posibilidad de hacer modificaciones, entró la chica en la competición, me hizo la prueba y ya no aparece opción de emisión, no la tiene porque los otros tampoco tenemos opción para hacer misión, entonces ya.

Gualdron Romero, Javier Leonardo   55:14
Y manos arriba.
Porque se está.
Listo, aquí en esta tablita que ustedes tienen acceso, pueden ver el dueño de la tabla, cuánto espacio usó y si lleva más de 9 meses usada. O sea, por ejemplo, estas tablas van a ser borradas.

Carrillo Leon, Juan Andres   55:27
Me encargó y era eso para que tú estuvieras enterado de que era como un alcance al proceso anterior. Son apenas cuatro sueldos. Listo, listo, claro.

Gualdron Romero, Javier Leonardo   55:38
Y en general, pues qué objetos tiene en caso de que ustedes quieran acceder a una tabla que no sepan quién fue el que la creó. Ustedes consultan acá y dice esa la creó debido campo. Dime.

Carrillo Leon, Juan Andres   55:41
Tan pronto no llegues, me país y conmigo era eso, gracias. Ay, no se puede ver el uso.
No se puede ver el uso porque digamos no sé ver una tola y dice uy okay.

Gualdron Romero, Javier Leonardo   55:51
En espacio.
Miren acá, están gigabytes.
Is there you 1 gigabytes?

Carrillo Leon, Juan Andres   55:57
Pero digamos, no sé, último último uso ayer a las 4:00 o nunca la usaron.

Gualdron Romero, Javier Leonardo   56:01
Tenemos una, sí, tenemos uno que digamos que es este, el data las use, pero no es muy exacto porque digamos que el tema de auditoría de Redshift está sujeto a 7 días y esto se saca una vez al mes. Así que básicamente podríamos ver los últimos 7 días de cada mes que ha sido usado, pero sí sería este.

Carrillo Leon, Juan Andres   56:18
Mhm.

Gualdron Romero, Javier Leonardo   56:24
Digamos que esto es para que lleven control, que pasa y que nos ha pasado y que seguramente vamos a tener que reforzarlo un poquitico, que el uso del sandbox, pues como puede ver, está súper disparado. O sea, mucha gente está creando productos de datos, están cacharreando. Eso que nos ha traído problemas de espacio.
Digamos que hemos agregado, agregado de espacio y no estamos dando abasto. Digamos que todo tiene límite. Entonces eso es un tema de conciencia. Si ustedes usaron una tabla que ocupa un giga y ya no la necesito más, pues la borro o si saco un backup, ya no la necesito más, pues la borro. Es más de conciencia porque si no, pues nos va a tocar de pronto.
Ser un poquitico más fuertes en el tema de cuánto tiempo almacenamos los datos. Tenemos que esto es como una recomendación. Esto es nuevo, hasta hasta ahora nos está pasando porque esto está creciendo muy rápido, va creciendo muy rápido. Y si mira, yo oiga, ya tengo una tabla aquí como pesada, bueno, pero que pasa es que es solito día vieja.
Es de del año pasado, pero bueno, aquí ustedes también pueden controlar lo que ustedes están haciendo y también cuando necesiten permiso de alguien, pues aquí miran el nombre de la persona dueña de Ropet y le dicen a ella.

Carrillo Leon, Juan Andres   57:29
Pero digamos hoy, digamos hoy de auto, los únicos que están ahí moviendo datos sería los de pricing, no y modeling.

Gualdron Romero, Javier Leonardo   57:35
Sí, pues aquí está, espérate y miramos a ver.

Carvajal Jaramillo, Karen Andrea   57:36
No.

Carrillo Leon, Juan Andres   57:38
Digamos de siniestro o hay de siniestros alguien que esté hoy moviendo, sí.

Gualdron Romero, Javier Leonardo   57:41
También.

Carvajal Jaramillo, Karen Andrea   57:42
Sí, también.

Gualdron Romero, Javier Leonardo   57:42
También también está el de siniestros del modeling, está ya el de pricing, creo que pasó a generales, pero bueno, no pricing.

Carrillo Leon, Juan Andres   57:51
Como para ir conociendo esas personas y uno, pues también, oye, si estás moviendo, pues crea la vista con todo esto, no sé.

Gualdron Romero, Javier Leonardo   57:58
Sí.
sí, tal cuerpo.
Aquí está Wilmer también, bueno, aquí van a encontrar de todas las personas que mueven o están moviendo o han movido, estos que son así son de nosotros, digamos que cuando nosotros productilizamos cosas, a veces también creamos para hacer validaciones como un usar administrador que usamos, entonces cualquier cosa que vean de este señor.
¿Me pueden decir a mí esto?

Carrillo Leon, Juan Andres   58:26
Javi, una cosilla es que ya nos toca estar ahorita a la reunión de cierre, entonces pues reprogramamos la siguiente y continuamos con el tema.

Gualdron Romero, Javier Leonardo   58:29
Yo también.
Ja, ja.
Si quieren, pero porfa, traigan un caso de uso, traigan un caso de uso para hacer un ejercicio real de algo que ustedes quieran y empezamos y la idea es que ustedes lo hagan. Yo los acompaño, los llevo, les traigo el tinto, pero ustedes lo hacen. Listo, listo, pues vale, chao chao.

Carrillo Leon, Juan Andres   58:36
Pero hasta aquí.

Carvajal Jaramillo, Karen Andrea   58:36
No tienen alguna duda adicional, sí.

Carrillo Leon, Juan Andres   58:44
Even up.
Y bueno, esa es la idea.
Muchas gracias, de verdad. Bueno, cuídense, chaos.

Trujillo Lavao, Juan Miguel   58:53
¿Y sabes si luego?

Carvajal Jaramillo, Karen Andrea   58:54
Chao.

Gualdron Romero, Javier Leonardo   58:55
Cualquier cosa me dicen, no.

Carrillo Leon, Juan Andres   58:57
una, gracias.

Trujillo Lavao, Juan Miguel   58:57
Yes.

Gualdron Romero, Javier Leonardo   58:58
Datos con Javier o con mi equipo, Brayita Esteban, chao, chao.

Carrillo Leon, Juan Andres   58:59
Bueno, vale, gracias.
And talk.

Carrillo Leon, Juan Andres detuvo la transcripción

