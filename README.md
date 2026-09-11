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

- **Claude (web / desktop / Cowork):** subí el archivo `.skill` en Configuración → Capacidades → Skills, o guardala desde la tarjeta de propuesta.
- **Claude Code:** copiá la carpeta a `~/.claude/skills/plan-before-build/`.

## Basado en

- [Claude Code best practices](https://code.claude.com/docs/en/best-practices) (Anthropic): explorar → planificar → implementar → verificar; el patrón de entrevista.
- [GitHub spec-kit](https://github.com/github/spec-kit): separar qué/por qué de cómo.
- [obra/superpowers — brainstorming](https://github.com/obra/superpowers): preguntas con opciones, enfoques con trade-offs, YAGNI, aprobación antes de codear.
