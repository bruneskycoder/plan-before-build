# plan-before-build

**Skill para Claude que obliga a planificar antes de construir.** Triage de profundidad, análisis de lo existente, investigación, entrevista en rondas de preguntas, comparación de enfoques y un `PLAN.md` aprobado antes de escribir código; después, ejecución en pasos verificables con evidencia.

*A Claude skill for spec-driven, plan-first development: triage, requirements interview, trade-off analysis, living PLAN.md, verified execution.*

## Qué hace

| Fase | Qué pasa |
|---|---|
| 0. Triage | Clasifica el trabajo en rápido / estándar / profundo según tamaño y riesgo |
| 1. Entender | Problema, usuario, resultado esperado y qué queda fuera, sin hablar de tecnología |
| 2. Analizar e investigar | Lee lo existente, arma un inventario de reutilización y verifica la documentación actual |
| 3. Entrevista | Rondas de 3–4 preguntas con opciones; solo lo que no se puede averiguar y cambia el plan |
| 4. Enfoques | 2–3 alternativas, sus trade-offs y el criterio que decide |
| 5. PLAN.md | Plan escrito y vivo: alcance, pasos verificables, riesgos, registro de decisiones |
| 6. Aprobación | No se escribe código sin OK (en los niveles estándar y profundo) |
| 7–8. Ejecutar y verificar | Pasos chicos, desvíos según su impacto, pruebas automáticas con evidencia + checklist manual |

## Principios

Analizar antes de hacer · respetar cómo se viene trabajando · reutilizar al máximo e inventar lo mínimo · lo más simple que funcione · mantenible y documentado.

## Instalación

- **Claude (web, escritorio o Cowork):** comprimí en un `.zip` una carpeta `plan-before-build` que tenga adentro el `SKILL.md`, y subila en la sección de Skills de la configuración.
- **Claude Code:** cloná este repositorio en `~/.claude/skills/plan-before-build/`.

## Cómo se hizo

No programo. Construyo con Claude Code: yo defino qué hay que resolver, para quién y cómo me doy cuenta de que funciona; Claude investiga, escribe y prueba. Esta skill es ese reparto de tareas puesto por escrito, y la armé con Claude a partir de las fuentes de abajo.

## Un ejemplo real

El [PLAN.md de A la Luz del Fogón](https://github.com/bruneskycoder/ciclo-de-sueno/blob/main/PLAN.md) tiene el formato que deja esta skill: nivel de profundidad, objetivo, lo que queda afuera, pasos verificables y un registro de decisiones y desvíos. Incluye el momento en que el plan apuntaba al lugar equivocado y hubo que rehacerlo.

## Basado en

- [Claude Code best practices](https://code.claude.com/docs/en/best-practices) (Anthropic): explorar → planificar → implementar → verificar; el patrón de entrevista.
- [GitHub spec-kit](https://github.com/github/spec-kit): separar qué/por qué de cómo.
- [obra/superpowers — brainstorming](https://github.com/obra/superpowers): preguntas con opciones, enfoques con trade-offs, YAGNI, aprobación antes de codear.

## Licencia

CC-BY-4.0: libre para usar, modificar y reutilizar con atribución.
