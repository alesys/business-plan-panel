# business-plan-panel

Skill para Claude que evalúa un plan de negocio con un panel de 9 agentes con personalidades distintas, corriendo en paralelo, y un evaluador final ("El Consejo") que condensa todo en un reporte con veredicto, consensos, riesgos mortales y plan de acción.

## El panel

| Agente | Perfil | Pregunta guía |
|---|---|---|
| Valeria | Inversionista escéptica | ¿Por qué esto no lo replica una empresa grande en seis meses? |
| Don Ernesto | Contador conservador | ¿De dónde sale cada número y qué pasa si es 50% peor? |
| Mike | Cliente real | ¿Por qué pagaría por esto en vez de seguir como estoy? |
| Rafa | Emprendedor veterano | ¿Qué va a doler en los primeros 6 meses? |
| Camila | Estratega de marketing | ¿Cuánto cuesta conseguir un cliente y cuánto deja? |
| Lic. Herrera | Abogado paranoico | ¿Qué podría terminar en una demanda o una multa? |
| La Sombra | Competidor | ¿Cómo lo saco del mercado? |
| Lupita | Operadora | ¿Quién hace esto el martes a las 8 de la mañana? |
| Leo | Optimista visionario | ¿Qué versión de este negocio sería 10 veces más grande? |

## Instalación

### Claude Code

Global (disponible en todos tus proyectos):

```bash
git clone https://github.com/alesys/business-plan-panel.git
cp -r business-plan-panel/business-plan-panel ~/.claude/skills/
```

Solo en un proyecto:

```bash
cp -r business-plan-panel/business-plan-panel .claude/skills/
```

### Claude.ai

Descarga `business-plan-panel.skill` de este repo y súbelo en Settings > Capabilities > Skills.

## Uso

Pídele a Claude algo como:

- "Evalúa mi plan de negocio en ./plan.md"
- "Destroza este pitch" (y pegas el texto)
- "Review my business plan"

En Claude Code los 9 agentes corren en paralelo como subagentes y el reporte se guarda en `./evaluacion-plan.md`, con cada evaluación individual en `./evaluaciones/`. En Claude.ai las evaluaciones se generan una por una y el reporte llega en el chat.

## Estructura

```
business-plan-panel/
├── SKILL.md
└── references/
    ├── personas.md   # los 9 agentes y el formato de salida
    └── consejo.md    # estructura del reporte final
```

## Personalizar

Edita `references/personas.md` para agregar, quitar o cambiar agentes (por ejemplo, un experto sectorial). Mantén el mismo formato: nombre, personalidad, enfoque y pregunta guía.
