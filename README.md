# business-plan-panel

Skill para Claude que evalúa un plan de negocio con un panel de 9 agentes con personalidades distintas, corriendo en paralelo, y un evaluador final ("El Consejo") que condensa todo en un reporte con veredicto, consensos, riesgos mortales y plan de acción.

## El panel

| Agente | Perfil | Pregunta guía |
|---|---|---|
| Valeria | Inversionista escéptica | ¿Por qué esto no lo replica una empresa grande en seis meses? |
| Don Ernesto | Contador conservador | ¿De dónde sale cada número y qué pasa si es 50% peor? |
| Mike | Cliente real | ¿Por qué pagaría por esto en vez de seguir como estoy? |
| Rafa | Emprendedor veterano | ¿Este equipo es el indicado y qué le va a doler en los primeros 6 meses? |
| Camila | Estratega de marketing | ¿Cuánto cuesta conseguir un cliente y cuánto deja? |
| Lic. Herrera | Abogado paranoico | ¿Qué podría terminar en una demanda o una multa? |
| La Sombra | Competidor | ¿Cómo lo saco del mercado? |
| Lupita | Operadora | ¿Quién hace esto el martes a las 8 de la mañana? |
| Leo | Optimista visionario | ¿Qué versión de este negocio sería 10 veces más grande? |

## Instalación

### Claude.ai o Cowork (sin nada técnico)

1. Descarga el archivo: [business-plan-panel.skill](https://github.com/alesys/business-plan-panel/raw/main/business-plan-panel.skill) (si alguien ya te lo pasó, sáltate este paso).
2. En Claude, ve a Settings > Capabilities > Skills y sube el archivo.
3. Listo. Dile a Claude "Evalúa mi plan de negocio" y pega o adjunta tu plan.

Si no ves la sección Skills, actívala primero en esa misma pantalla de Capabilities.

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

## Uso

Pídele a Claude algo como:

- "Evalúa mi plan de negocio en ./plan.md"
- "Destroza este pitch" (y pegas el texto)
- "Review my business plan"

Tu plan puede estar en cualquier forma: un documento, un PDF, un pitch deck, notas de voz transcritas, un Excel o unos párrafos sueltos. Claude te preguntará en qué etapa estás (idea, ya vendes, buscas inversión) si no queda claro, y ajusta la exigencia a eso.

El reporte empieza con un bloque "Si solo lees una cosa" con lo más urgente en lenguaje simple; el resto es para profundizar.

**Consumo:** son 9 evaluaciones más un reporte final. En el plan gratuito puede agotar tu límite de mensajes del día. Si quieres algo más ligero, pide "versión corta" y se usan 5 agentes.

En Claude Code y Cowork los 9 agentes corren en paralelo como subagentes y el reporte se guarda en `./evaluacion-plan.md`, con cada evaluación individual en `./evaluaciones/`. En Claude.ai las evaluaciones se generan una por una y el reporte llega en el chat.

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
