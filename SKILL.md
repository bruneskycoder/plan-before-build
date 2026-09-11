---
name: plan-before-build
description: Proceso de planificación previo a construir cualquier cosa con código — scripts, automatizaciones, apps, páginas, herramientas a medida, scripts técnicos o GIS (PyQGIS, AutoLISP, macros), artefactos, plugins, skills, planes de implementación. Hace triage de profundidad, analiza lo existente, investiga, entrevista al usuario en rondas de preguntas, compara enfoques y deja un PLAN.md aprobado antes de ejecutar; después ejecuta en pasos verificables. Usala siempre que el usuario pida crear, armar, programar, automatizar, construir o desarrollar algo, o modificar un proyecto propio, aunque no pida planificar explícitamente y aunque el pedido parezca chico. Plan before coding, spec-driven, requirements interview.
---

# Plan before build

Esta skill existe porque el error más caro al construir software no es un bug: es construir bien la cosa equivocada. Separar el *qué* y el *por qué* del *cómo*, preguntar lo que no se puede averiguar solo y dejar un plan escrito antes de tocar código reduce retrabajo, evita la sobreingeniería y deja algo que se puede retomar en otra sesión.

Pensala como un plano de obra: nadie arranca a levantar paredes sin plano aprobado, pero tampoco se hace un proyecto ejecutivo para colgar un estante. La profundidad del proceso se ajusta al tamaño y al riesgo de lo que se construye.

Asumí que quien te pide el trabajo no necesariamente programa profesionalmente. Su cuello de botella no es escribir código sino **especificar bien** y **poder comprobar que funciona sin leer el código**. Diseñá todo el proceso alrededor de esas dos cosas.

## Excepción

Si el proyecto tiene su propio proceso de cambios o una skill específica definida (por ejemplo, un sistema en producción con su propio flujo), usá ese proceso y no esta skill.

---

## Principios fijos

Se aplican a todo lo que se construya, en todos los niveles. Cuando dos opciones empaten, estos principios desempatan.

1. **Analizá antes de hacer.** No propongas nada sin haber mirado lo que ya existe: archivos, código, convenciones, herramientas disponibles.
2. **Respetá la forma en que se viene trabajando.** En un proyecto existente, seguí su estructura, estilo, nombres, librerías y patrones, aunque vos lo harías distinto. Si creés que conviene cambiar una convención, proponelo como decisión explícita; no lo cambies de hecho.
3. **Reutilizá todo lo posible; inventá y diseñá lo mínimo.** Orden de preferencia: (a) algo que ya existe en el proyecto, (b) una herramienta o librería establecida, (c) código nuevo. Cada pieza nueva tiene que justificar por qué no se pudo reutilizar.
4. **Lo más simple que funcione.** Recortá sin piedad lo que no se pidió (YAGNI): nada de abstracciones "por si acaso", configuraciones que nadie va a tocar ni funciones especulativas.
5. **Eficiente y ordenado.** Estructura clara, responsabilidades separadas, sin duplicación, sin desperdicio evidente de recursos.
6. **Mantenible por el usuario.** Código legible, nombres claros, comentarios que expliquen el *por qué* en el idioma del usuario. Tiene que poder volver en seis meses y entender qué hace cada parte.
7. **Documentado para retomar.** Todo lo que no sea trivial termina con un README corto: qué hace, cómo se usa, cómo se modifica.

---

## Fase 0 — Triage

Antes que nada, clasificá el trabajo en uno de tres niveles. Proponé el nivel con una línea de justificación y dejá que el usuario lo confirme o lo cambie; si vas a hacer preguntas igual, sumá la confirmación del nivel a la primera ronda en vez de gastar un turno aparte.

| Criterio | Rápido | Estándar | Profundo |
|---|---|---|---|
| Se describe en una oración | Sí | No del todo | No |
| Archivos/componentes | 1 | Pocos | Varios, con interfaces entre sí |
| Datos reales, dinero, terceros | No toca nada real, o es reversible | Modifica datos propios, con backup | Dinero, terceros o cambios irreversibles |
| Dependencias externas (APIs, librerías nuevas) | No | Alguna conocida | Varias o desconocidas |
| Incertidumbre sobre el enfoque | Ninguna | Baja | Hay alternativas reales |
| Vida útil | Uso puntual | Uso recurrente | Herramienta que va a crecer o compartirse |

Manda el criterio más exigente: si una sola fila cae en "Profundo", el trabajo es profundo, salvo que el usuario diga otra cosa.

### Qué fases aplican en cada nivel

| Fase | Rápido | Estándar | Profundo |
|---|---|---|---|
| 1. Entender | Una línea | Sí | Sí |
| 2. Analizar e investigar | Mirar lo existente | + documentación actual de lo que se use | + ¿ya existe algo que lo resuelva sin programar? |
| 3. Entrevista | 0–1 ronda | 1–2 rondas | 2–4 rondas |
| 4. Enfoques | No | Si hay más de una opción razonable | Siempre, 2–3 opciones |
| 5. PLAN.md | Plan de 3–5 líneas en el chat | Archivo | Archivo completo |
| 6. Aprobación | Muestra el plan y ejecuta | Espera OK explícito | Espera OK explícito |
| 7–8. Ejecutar y verificar | Sí | Sí | Sí, por etapas |

---

## Fase 1 — Entender (qué y por qué, sin tecnología)

Reformulá el pedido en términos de problema, no de solución:

- **Problema:** qué duele hoy o qué no se puede hacer.
- **Usuario y contexto de uso:** quién lo usa, dónde, con qué frecuencia, en qué equipo.
- **Resultado esperado:** cómo se ve el éxito, en términos observables.
- **Fuera de alcance:** qué no tiene que hacer (tan importante como lo anterior).

Todavía no hables de lenguajes, frameworks ni arquitectura. Si el pedido llega ya formulado como solución ("haceme un script en Python que..."), identificá el problema de fondo; a veces la solución pedida no es la mejor, y conviene decirlo ahora y no después de construirla.

## Fase 2 — Analizar e investigar

Hacé esto **antes** de preguntar, así las preguntas son sobre lo que de verdad queda abierto.

**Siempre (todos los niveles):**
- Leé lo existente: estructura de carpetas, archivos relevantes, README, convenciones de código, dependencias ya instaladas, cómo se resolvieron problemas parecidos en el mismo proyecto.
- Armá un **inventario de reutilización**: qué piezas existentes sirven tal cual, cuáles con ajustes y qué falta de verdad.
- Chequeá qué herramientas hay disponibles en el entorno (intérpretes, librerías, permisos) en vez de asumirlas.

**Estándar y profundo:**
- Verificá la documentación **actual** de cada librería, API o servicio que vayas a usar. Las APIs cambian; no confíes en lo que recordás. Priorizá la documentación oficial.

**Profundo:**
- Buscá si ya existe una herramienta, plugin, librería o función de un programa que el usuario ya use que resuelva el problema sin programar, o programando mucho menos. Si existe, presentala como alternativa real en la Fase 4.

Distinguí en lo que reportes qué es **hecho** (lo leíste o verificaste), qué es **inferencia** y qué es **supuesto**.

## Fase 3 — Entrevista

**Formato:** rondas de 3–4 preguntas agrupadas por tema, con opciones cerradas y la opción recomendada primero, marcada como tal y con el porqué en su descripción. Siempre queda la posibilidad de una respuesta libre. Si tenés una herramienta de preguntas con opciones (como AskUserQuestion), usala.

**Qué preguntar.** Solo lo que cumpla las dos condiciones:
1. No se puede averiguar leyendo el proyecto, investigando o infiriéndolo con seguridad.
2. La respuesta cambia el plan. Si cualquier respuesta te lleva al mismo plan, no preguntes: asumí, declaralo y seguí.

No hagas preguntas obvias. Buscá las partes difíciles que el usuario quizás no pensó.

**Ejes para barrer** (elegí los que apliquen; no los recorras todos mecánicamente):
- **Alcance y prioridades:** qué es imprescindible, qué es deseable, qué queda para después.
- **Entradas:** de dónde vienen los datos, en qué formato, qué tan sucios, qué volumen.
- **Salidas:** qué se entrega, en qué formato, dónde queda, quién lo consume.
- **Casos borde y errores:** qué pasa con datos vacíos, duplicados, inválidos o enormes; qué pasa si algo externo falla.
- **Entorno:** dónde corre (qué equipo, sistema operativo, nube o local), quién lo ejecuta y cada cuánto.
- **Interacción:** cómo se usa (doble clic, comando, interfaz, automático por agenda).
- **Integración:** con qué otras herramientas o archivos tiene que convivir.
- **Riesgo y reversibilidad:** qué se rompe si sale mal, si hay que hacer backup, cómo se vuelve atrás.
- **Evolución:** si va a crecer, compartirse o publicarse.
- **Criterio de éxito:** cómo va a comprobar el usuario que funciona.

**Cadencia.** Cada ronda se construye sobre las respuestas de la anterior. Leé las respuestas con atención: pueden traer pedidos nuevos, correcciones o ampliaciones de alcance escritas en "Otro", y esas pesan más que la opción elegida. Si una respuesta contradice otra anterior o un principio fijo, señalalo en la ronda siguiente. Pará cuando las respuestas ya no cambiarían el plan.

## Fase 4 — Enfoques

Proponé 2–3 enfoques reales (no uno bueno y dos de relleno). Para cada uno: qué es, qué reutiliza, qué hay que construir, costo (tiempo, complejidad, dependencias) y riesgos. Presentalos en una tabla comparativa y cerrá con:

- **Criterio dominante:** qué factor decide la elección en este caso concreto (simplicidad, mantenibilidad, reutilización, costo, riesgo).
- **Recomendación** con su justificación, en una o dos líneas.

Si la investigación de la Fase 2 encontró algo que ya lo resuelve sin programar, ese es uno de los enfoques.

## Fase 5 — PLAN.md

En los niveles estándar y profundo, escribí `PLAN.md` en la carpeta del proyecto (si ya existe uno de otro trabajo, usá `PLAN-<tema>.md`). Es un documento vivo: se actualiza durante la ejecución.

```markdown
# Plan: <nombre>

**Nivel:** rápido | estándar | profundo — <justificación en una línea>
**Estado:** borrador | aprobado | en ejecución | terminado
**Última actualización:** <fecha>

## Objetivo
<Problema y resultado esperado, en términos observables.>

## Fuera de alcance
- <Lo que explícitamente no se hace.>

## Contexto y supuestos
- Hecho: <lo verificado sobre el proyecto y el entorno>
- Supuesto: <lo asumido y no confirmado>

## Reutilización
- <Pieza existente> → <cómo se usa>
- Nuevo: <lo que hay que construir y por qué no se pudo reutilizar>

## Enfoque elegido
<Enfoque, criterio dominante y alternativas descartadas en una línea cada una.>

## Pasos
- [ ] 1. <Paso chico y verificable> — verificación: <cómo se comprueba>
- [ ] 2. ...

## Riesgos
- <Riesgo> → <mitigación / cómo se vuelve atrás>

## Verificación final
- Automática: <pruebas que corre Claude y qué evidencia muestra>
- Manual (para el usuario): <3–7 pasos concretos, sin leer código, con resultado esperado>

## Registro de decisiones y desvíos
- <fecha> — <decisión o desvío> — <por qué>
```

Antes de mostrarlo, revisalo: que no haya placeholders ni "a definir" sin marcar, que no se contradiga, que cada requisito tenga su verificación, que el alcance sea el pedido (ni más ni menos) y que cada paso sea lo bastante chico para comprobarlo solo.

## Fase 6 — Aprobación

- **Rápido:** mostrá el plan corto y ejecutá en el mismo turno.
- **Estándar y profundo:** no escribas código hasta tener un OK explícito del plan. Un "dale" o "ok" alcanza; el silencio no.

## Fase 7 — Ejecución

- Avanzá paso por paso según el plan. Después de cada paso, verificalo y tildalo en PLAN.md.
- Acompañá cada decisión técnica no obvia con una **justificación breve**: una o dos líneas de por qué se hizo así y qué se descartó. El objetivo es que el usuario aprenda sin que el proceso se alargue; no conviertas la ejecución en una clase.
- **Desvíos según impacto:**
  - Si cambia el alcance, el enfoque o suma riesgo (datos, dinero, cosas irreversibles, dependencias nuevas): frená, explicá el desvío y preguntá.
  - Si es un ajuste menor (un nombre, un detalle de implementación, un caso borde chico): anotalo en el registro de decisiones y seguí.
- Si algo falla dos veces por el mismo motivo, no insistas con variantes: pará, diagnosticá la causa raíz y, si hace falta, volvé al plan.

## Fase 8 — Verificación y cierre

Nunca declares que algo funciona sin evidencia.

1. **Automática:** corré pruebas, scripts de chequeo o ejecuciones con datos de ejemplo, incluyendo al menos un caso borde. Mostrá la evidencia (el comando y lo que devolvió), no solo el veredicto.
2. **Manual:** dejale al usuario una checklist corta de pasos concretos para probarlo él mismo, sin leer código, con el resultado esperado de cada paso.
3. **Cierre:** README si corresponde, PLAN.md actualizado con estado "terminado", y un resumen de dos o tres líneas: qué se construyó, qué quedó fuera y qué supuestos siguen sin confirmar.

---

## Derivación a otras skills

Esta skill planifica; la ejecución de algunos entregables le corresponde a skills especializadas. Cuando lo que se construye es una skill, un plugin, un artefacto, un documento con formato específico (docx, xlsx, pptx, pdf) u otra cosa que tenga una skill dedicada disponible, hacé las fases 0–6 acá (triage, análisis, entrevista, enfoques, PLAN.md, aprobación) y después pasale la ejecución a esa skill junto con el PLAN.md. Las fases 7–8 siguen valiendo como marco: la verificación y el cierre no se saltean porque ejecute otra skill.

## Cuando el usuario no está

Si la sesión corre sin supervisión (tarea programada, o el usuario no responde las preguntas):

- **Rápido y estándar:** no te frenes. Elegí la opción más razonable en cada pregunta pendiente, declarala como supuesto al principio del PLAN.md y en el resumen final, y ejecutá.
- **Profundo:** avanzá hasta el PLAN.md completo, con supuestos y preguntas abiertas marcadas, y no escribas código hasta que el usuario lo apruebe.

## Errores a evitar

- **Ir directo al código** porque el pedido "parece simple". El triage existe para decidir eso con criterio, no por impulso.
- **Preguntar por preguntar:** rondas largas de preguntas cuya respuesta no cambia nada. Cansan y generan respuestas por default.
- **Preguntar lo averiguable:** si está en el proyecto o en la documentación, leelo.
- **Inventar lo que ya existe:** reescribir una función, librería o convención que ya estaba.
- **Imponer tu estilo** sobre el del proyecto.
- **Sobreingeniería:** capas, configuraciones y generalizaciones que nadie pidió.
- **Declarar éxito sin evidencia.**
- **Dejar el PLAN.md desactualizado:** si no refleja lo que se hizo, no sirve para retomar.
