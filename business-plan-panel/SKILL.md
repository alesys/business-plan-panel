---
name: business-plan-panel
description: Evalúa un plan de negocio con un panel de 9 agentes con personalidades distintas (inversionista escéptica, contador, cliente, emprendedor veterano, marketing, abogado, competidor, operaciones y visionario) que corren en paralelo, y luego un evaluador final ("El Consejo") condensa todo en un reporte con veredicto, consensos, riesgos y plan de acción. Usa este skill cuando el usuario pida evaluar, criticar, validar o "destrozar" un plan de negocio, pitch, business plan, modelo de negocio, idea de startup o la viabilidad de un negocio concreto, o pida feedback de "inversionistas", "expertos" o "diferentes perspectivas" sobre su negocio. No lo uses para revisar documentos que no describen un negocio completo (un correo, un texto de marketing, un documento de estrategia suelto). Also triggers in English (review my business plan, evaluate my pitch, poke holes in my startup idea).
---

# Panel de evaluación de planes de negocio

Este skill simula un panel de 9 evaluadores con perfiles y sesgos distintos. El valor está en que cada uno ve problemas diferentes y en que sus opiniones chocan. Un solo evaluador "neutral" tiende a ser demasiado amable; nueve sesgados y aislados, sintetizados después, producen crítica útil.

## Flujo

### 1. Conseguir el plan
- Si el usuario adjuntó o indicó un archivo, léelo completo.
- Si pegó el plan en el chat, úsalo tal cual.
- Sirve cualquier forma de plan: documento, PDF, pitch deck, notas de voz transcritas, un Excel de números, unos párrafos sueltos. Si el material cubre solo una parte (por ejemplo, solo un Excel de gastos sin describir el negocio), dilo antes de empezar: el panel no podrá opinar de mercado ni de clientes, y conviene que el usuario agregue dos o tres párrafos sobre qué vende y a quién.
- Si no hay plan, pídelo. Si solo hay una idea de dos líneas, avisa que la evaluación será superficial y procede igual si el usuario quiere.
- No resumas el plan antes de pasarlo a los agentes. Cada uno necesita el texto íntegro para citar evidencia concreta.

### 2. Determinar la etapa
El rigor depende de en qué punto está el negocio. Si el plan lo deja claro, dedúcelo; si no, pregúntalo en una línea antes de lanzar el panel:

| Etapa | Qué exige el panel |
|---|---|
| **Idea** (todavía no vende) | Un plan de validación barato (entrevistas, preventas, prueba piloto). No se castiga la falta de proyecciones detalladas; se castiga no saber cómo comprobar la demanda. |
| **Operando** (ya vende, no busca inversión) | Números reales: ventas, márgenes, clientes que repiten. La pregunta es si funciona y cómo mejora, no si escala para un inversionista. |
| **Busca inversión** | Rigor máximo: tracción medida, unit economics, equipo, defensibilidad. El Consejo cierra con un sí o no a levantar capital hoy. |

Pasa la etapa a cada agente junto con el plan.

### 3. Lanzar los 9 agentes
Lee `references/personas.md`: contiene los 9 personajes, las reglas comunes y el formato de salida obligatorio.

**Si tienes una herramienta para lanzar subagentes (Agent, antes Task):** lanza los 9 en un solo turno, en paralelo. Usa un subagente genérico que arranque sin contexto (en Claude Code, `general-purpose`); nunca `fork` ni un tipo que herede la conversación, porque eso rompe el aislamiento. Cada prompt se arma así, en este orden:

```
[bloque del personaje, copiado de personas.md]

REGLAS COMUNES:
[reglas comunes, copiadas de personas.md]

FORMATO DE SALIDA:
[formato de salida obligatorio, copiado de personas.md]

ETAPA DEL NEGOCIO: [idea / operando / busca inversión]

PLAN COMPLETO:
[texto íntegro del plan]
```

Ningún subagente ve la respuesta de otro; el aislamiento evita que se contagien y converjan a una opinión tibia.

**Si no tienes subagentes (Claude.ai):** genera las 9 evaluaciones tú mismo, una por una, entrando de lleno en cada personaje. Antes de cada una, deja de lado lo que concluiste en las anteriores y evalúa solo desde ese perfil. Es menos aislado que en paralelo, así que compénsalo siendo deliberadamente fiel al sesgo de cada personaje.

**Modo corto:** si el usuario pide algo más ligero o le preocupa el consumo, usa 5 agentes: Don Ernesto, Mike, Rafa, Camila y La Sombra.

### 4. Debate (opcional)
Hazlo solo si el usuario lo pide o si la etapa es "busca inversión". Toma las 2 o 3 objeciones más graves de Valeria y La Sombra, pídele a Leo que las rebata, y luego pide a Valeria y La Sombra una réplica breve. Pásale el debate completo al Consejo junto con las evaluaciones.

### 5. El Consejo
Lee `references/consejo.md` y produce el reporte final con esa estructura. El Consejo sintetiza; no repite lo que dijo cada agente.

### 6. Entrega
- Si puedes escribir archivos: guarda el reporte en `./evaluacion-plan.md` y cada evaluación individual en `./evaluaciones/<nombre-agente>.md`. Muestra en el chat el bloque "Si solo lees una cosa", el veredicto general y la tabla de calificaciones.
- Si no puedes escribir archivos: entrega el reporte del Consejo en la respuesta. Ofrece las evaluaciones individuales completas si el usuario las quiere ver.

## Reglas de estilo
- Escribe en el idioma del usuario (por defecto español).
- No uses em dashes (—) en ningún texto generado. Usa dos puntos, comas o paréntesis.
- Cada crítica debe anclarse en algo del plan. Si falta información, se reporta como hueco; nunca se inventan datos del negocio.
- Sé específico: "No hay estimación de CAC para Instagram" sirve; "el marketing es débil" no.
- La primera vez que aparezca un término técnico (CAC, LTV, runway, punto de equilibrio), explícalo entre paréntesis en pocas palabras.

## Personalización
Si el usuario pide agregar, quitar o cambiar agentes (por ejemplo, un experto sectorial en restaurantes o en SaaS, o un experto técnico que audite la viabilidad del producto), ajusta el panel en esa ejecución siguiendo el mismo formato de personaje: nombre, personalidad, sesgo, enfoque y pregunta guía.
