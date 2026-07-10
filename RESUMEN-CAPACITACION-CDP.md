# Resumen — Capacitación CDP (09/07/2026)

> Grabación: *Capacitación CDP-20260709* — duración 59 min.
> Expositores: **Karen Andrea Carvajal Jaramillo** (generalidades y modelo) y **Javier Leonardo Gualdron Romero** (contenido, datos y práctica).
> Asistentes: Juan Andrés Carrillo León, Juan Miguel Trujillo Lavao, entre otros.
> Este resumen también está incluido como Anexo (sección 9) del `CDP-MANUAL-DE-USUARIO.md`.

## Resumen general

La sesión presentó el **Colombia Data Program (CDP)**, evolución del antiguo ADP de Liberty tras la separación de países: una base de datos **Amazon Redshift en AWS** de propósito **analítico** (no transaccional ni en tiempo real), que consolida la información de Colombia proveniente de **IAxis (core)** y **AS400** bajo el estándar medallón (capa cruda → reglas de calidad → capa productiva en **modelo estrella**). Se recorrió la nomenclatura de tablas (`dim_` y `fact_`), las FACT y DIM más importantes, el datamart de motor (autos), las reglas de uso de llaves dinámicas, el campo `current_record_flag`, el funcionamiento del sandbox y las buenas prácticas de consulta. La sesión cerró con la invitación a traer un caso de uso real para la próxima reunión.

## Puntos importantes

1. **ADP → CDP:** solo datos de Colombia; contenido mayoritariamente en inglés (herencia Liberty). Es un data warehouse analítico en Redshift/AWS.
2. **Modelo estrella:** FACT = movimientos/transacciones ("todo lo que mueva plata"); DIM = atributos descriptivos. Las tablas `*_backup` son respaldos internos: no se consumen y el nombre productivo nunca cambia.
3. **Regla práctica:** todo reporte con movimientos **arranca desde la FACT** y se le unen las DIM; entre DIMs no suele haber camino directo.
4. **FACT destacadas:** primas y siniestros; **IMX** (todos los movimientos, incluidos los no transaccionales como cambio de sucursal); **vigentes** (28 días corridos / fin de mes); **preguntas y respuestas de IAxis** (riesgo, siniestro, póliza); **Mills (inspecciones)**; **cotizaciones** (auto individual y colectivo); **policy cycles** (ciclos de vigencia de la póliza); **coaseguro/corretaje** (nueva).
5. **Datamart de motor (autos):** primer gran desarrollo del CDP, productivo para pricing y modeling; reemplaza el monitor de SageMaker. Vista resumen: **monitor motor full**. Incluye marca **nuevo/renovado** (certificada por pricing), **expuestos**, **devengo** (earned premium = expuesto × prima) y la **Guía Fasecolda** (carga mensual).
6. **`current_record_flag = 1`:** trae el último registro válido; existe en todas las tablas del esquema general.
7. **Llaves dinámicas (SK):** solo para hacer `JOIN`; **nunca quemarlas (hardcodear) en el código** porque cambian en el tiempo. Alternativa: llaves lógicas (póliza + certificado), pero por rendimiento se recomienda la SK. Tampoco quemar SBUs, códigos ni contraseñas: no se productiviza código con datos quemados.
8. **Granularidad:** hasta **amparo** (no hay nivel recibo); agrupar amparos para obtener cifras por póliza.
9. **Buenas prácticas de consulta:** siempre `LIMIT`/`WHERE`; queries pesadas pueden bloquear el CDP. Mejor horario: **las mañanas**; congestión en cierres contables.
10. **Disponibilidad:** hoy hasta las 10 p. m.; próximamente **corte a las 6 p. m.** por la ventana de actualización nocturna; reapertura ≈ 5 a. m. Las queries en ejecución durante la carga se cancelan.
11. **Sandbox:** cada usuario es dueño y responsable de sus objetos y otorga permisos manualmente; vida útil de **9 meses** (luego se borran); espacio limitado (borrar lo que no se use); existe tabla de control con dueño, tamaño y antigüedad.
12. **Productivización (desarrollo colaborativo):** negocio desarrolla → ingeniería revisa/optimiza → pasa al esquema general. Así el trabajo no se pierde y queda automatizado.
13. **Fuente única de la verdad:** no extraer directo de IAxis ni mezclar CDP con el Data Warehouse SQL antiguo (infraestructuras distintas). La columna `source`/`core_system` indica el sistema de origen del dato.
14. **Evolución continua:** si falta una variable que existe en IAxis se puede solicitar (análisis de factibilidad/prioridad). Diccionario de datos en **Confluence**; cambios documentados en repositorio.
15. **Conexión:** hoy se usa **DBeaver** (antes DB Visualizer). Parámetros por ambiente:

| Ambiente | Host | Puerto | Base de datos |
|----------|------|--------|---------------|
| Producción (Prod) | `corshftanltc-dprogramp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| No Producción (Non Prod) | `corshftanltc-dprogramnp.hdicolombia.com.co` | `9519` | `adp_dwh` |
| Desarrollo (Dev) | `corshftanltc-dprogramd.hdicolombia.com.co` | `9519` | `adp_dwh` |

16. **Próxima sesión:** llevar un **caso de uso real** para desarrollarlo con acompañamiento del equipo CDP (soporte de datos: Javier Gualdron y equipo; soporte de la app DBeaver: mesa de ayuda).
