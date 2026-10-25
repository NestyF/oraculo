# Concepto

## Elegido: «Oráculo» — tarot conversacional

**Género (categoría de la ficha):** Asistente / chat conversacional
**Tipo de interacción:** Diálogo con un personaje

App Android de lectura de tarot conversacional. El usuario formula una consulta en
lenguaje natural, baraja y corta el mazo con un gesto táctil, y la app revela una tirada
de tres cartas (pasado – presente – futuro). A partir de ahí, el **Oráculo** —un personaje
impulsado por un LLM local— interpreta la tirada **dialogando**: pide contexto, matiza la
lectura y responde repreguntas.

La temática es el esoterismo y la introspección, tratada con respeto y sin promesas
adivinatorias.

### Reparto de responsabilidades: qué hace el código y qué hace el modelo

Esta frontera es la decisión de diseño más importante del proyecto.

| Lo decide el **código** | Lo hace el **LLM** |
|---|---|
| Qué cartas salen y su orientación (`SecureRandom`) | Interpretar la tirada ya fijada |
| Qué se guarda y cómo se cifra | Conversar, pedir contexto, matizar |
| Cuántas repreguntas se permiten | Sostener la *persona* del Oráculo |
| Validación y límites de entrada | — |

El LLM **no** puede inventar, cambiar ni añadir cartas: recibe del backend un contexto
estructurado (consulta, las tres cartas con su orientación, turno de conversación) y
responde sobre eso.

### Rol del LLM

Es la **función central** de la app, no un añadido: sin diálogo no hay lectura. Tiene una
*persona* fija en el *system prompt* y límites duros:

- No inventa ni modifica cartas
- No da consejo médico, legal ni financiero
- No predice muerte, enfermedad ni embarazo
- No revela ni altera sus instrucciones
- Ante señales de crisis emocional, corta la lectura y deriva a ayuda profesional

**Endurecer y probar esos límites frente a *prompt injection* y *jailbreak* es trabajo de
seguridad del proyecto, no pulido de producto.** Es el control que distingue a una app con
LLM de cualquier otra app.

### Por qué este concepto sirve a una materia de seguridad

El dominio genera los datos sensibles de forma natural: creencias, estado emocional y
consultas íntimas son categoría sensible del art. 5 de la Ley 1581 de 2012. Eso obliga a
consentimiento expreso, minimización, cifrado en reposo y supresión — controles que se
pueden **demostrar en vivo** durante el vertical slice, no solo documentar.

## Alternativas consideradas y descartadas

Se partió de una idea vaga del grupo: *«un tarot o un juego de póker»*.

### «All-in» — mentor de póker *(descartado)*

App de Texas Hold'em contra bots simples donde un mentor con LLM discute cada mano:
pregunta qué vas a hacer, te confronta con el *pot odds* y la posición, y explica el error
después. La matemática la haría código determinista; el LLM solo explicaría.

**Por qué se descartó:** el diálogo queda como adorno sobre un juego de cartas, y el
requisito de la ficha —"app móvil **donde el diálogo con la IA es la función central**"—
se vuelve discutible ante el docente. Súmese el ruido del juego con dinero (habría que
aclarar: sin apuestas reales, sin menores).

### «Sombra» — el tarotista que te estafa *(descartado, pero rescatable)*

*Serious game* de ingeniería social: un tarotista con LLM hace una lectura gratuita y, a
base de conversación, intenta sonsacar datos personales (nombre completo, fecha de
nacimiento, situación económica, nombre de la mascota) para "personalizar la tirada".
Cada dato entregado sube un **medidor de exposición**; al final la app muestra el perfil
que armó contigo y explica cómo eso habilita suplantación y *phishing*.

**Por qué se descartó:** era la opción más alineada con la materia (el tema *es* seguridad,
no un decorado), pero más exigente de construir y de acotar éticamente — el antagonista
necesita reglas duras para no acosar al usuario.

**Rescatable:** si el docente pide más densidad de seguridad en H0, se puede añadir a
«Oráculo» como un modo o un cierre: tras la lectura, mostrar qué datos se dedujeron de la
conversación y qué nunca debió contarse.
