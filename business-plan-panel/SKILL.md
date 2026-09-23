---
name: business-plan-panel
description: Evalúa un plan de negocio con un panel de 9 agentes con personalidades distintas (inversionista escéptica, contador, cliente, emprendedor veterano, marketing, abogado, competidor, operaciones y visionario) que corren en paralelo, y luego un evaluador final ("El Consejo") condensa todo en un reporte con veredicto, consensos, riesgos y plan de acción. Usa este skill siempre que el usuario pida evaluar, revisar, criticar, validar, auditar o "destrozar" un plan de negocio, pitch, business plan, modelo de negocio, one-pager, idea de startup o propuesta comercial, aunque no mencione agentes ni panel. También cuando pida feedback de "inversionistas", "expertos" o "diferentes perspectivas" sobre un negocio. Also triggers in English (review my business plan, evaluate my pitch, poke holes in my startup idea).
---

# Panel de evaluación de planes de negocio

Este skill simula un panel de 9 evaluadores con perfiles y sesgos distintos. El valor está en que cada uno ve problemas diferentes y en que sus opiniones chocan. Un solo evaluador "neutral" tiende a ser demasiado amable; nueve sesgados y aislados, sintetizados después, producen crítica útil.

## Flujo

### 1. Conseguir el plan
- Si el usuario adjuntó o indicó un archivo, léelo completo.
- Si pegó el plan en el chat, úsalo tal cual.
- Si no hay plan, pídelo. Si solo hay una idea de dos líneas, avisa que la evaluación será superficial y procede igual si el usuario quiere.
- No resumas el plan antes de pasarlo a los agentes. Cada uno necesita el texto íntegro para citar evidencia concreta.

### 2. Lanzar los 9 agentes
Lee `references/personas.md`: contiene los 9 personajes, las reglas comunes y el formato de salida obligatorio.

**Si tienes subagentes (Claude Code, Cowork):** lanza los 9 en un solo turno, en paralelo, con la herramienta Agent (antes Task). Cada prompt de subagente lleva: el bloque del personaje, las reglas comunes, el formato de salida y el plan completo. Ningún subagente ve la respuesta de otro; el aislamiento evita que se contagien y converjan a una opinión tibia.

**Si no tienes subagentes (Claude.ai):** genera las 9 evaluaciones tú mismo, una por una, entrando de lleno en cada personaje. Antes de cada una, deja de lado lo que concluiste en las anteriores y evalúa solo desde ese perfil. Es menos aislado que en paralelo, así que compénsalo siendo deliberadamente fiel al sesgo de cada personaje.

### 3. Debate (opcional)
Hazlo solo si el usuario lo pide o si el plan es serio (por ejemplo, va a levantar capital). Toma las 2 o 3 objeciones más graves de Valeria y La Sombra, pídele a Leo que las rebata, y luego pide a Valeria y La Sombra una réplica breve. Incluye el resultado en la sección de contradicciones del reporte.

### 4. El Consejo
Lee `references/consejo.md` y produce el reporte final con esa estructura. El Consejo sintetiza; no repite lo que dijo cada agente.

### 5. Entrega
- En Claude Code o Cowork: guarda el reporte en `./evaluacion-plan.md` y cada evaluación individual en `./evaluaciones/<nombre-agente>.md`. Muestra en el chat el veredicto general, la tabla de calificaciones y el plan de acción.
- En Claude.ai: entrega el reporte del Consejo en la respuesta. Ofrece las 9 evaluaciones individuales completas si el usuario las quiere ver.

## Reglas de estilo
- Escribe en el idioma del usuario (por defecto español).
- No uses em dashes (—) en ningún texto generado. Usa dos puntos, comas o paréntesis.
- Cada crítica debe anclarse en algo del plan. Si falta información, se reporta como hueco; nunca se inventan datos del negocio.
- Sé específico: "No hay estimación de CAC para Instagram" sirve; "el marketing es débil" no.

## Personalización
Si el usuario pide agregar, quitar o cambiar agentes (por ejemplo, un experto sectorial en restaurantes o en SaaS), ajusta el panel en esa ejecución siguiendo el mismo formato de personaje: nombre, personalidad, sesgo, enfoque y pregunta guía.
