# Contexto para Claude Code

## Qué es esto

Proyecto Final de **Seguridad Informática** — UMNG, Ingeniería Multimedia, 2026-II.
**«Oráculo»**: app móvil Android de tarot conversacional con un LLM local (Ollama) como
función central. Ver `README.md` para el concepto y el estado.

## Reglas que no se negocian

Vienen del enunciado y de las confirmaciones firmadas en la ficha H0:

1. **No se desarrolla antes de la aprobación del docente (H0).** `app/`, `backend/` y
   `llm/` están vacías a propósito. No crear código en ellas hasta que el usuario confirme
   que H0 fue aprobado.
2. **Sin APIs de IA externas.** El modelo corre con Ollama en un equipo del grupo. Nunca
   proponer OpenAI, Anthropic, Gemini ni similares para el producto.
3. **Se califica la seguridad, no el arte.** Ante una disyuntiva entre pulir la experiencia
   y demostrar un control de seguridad, gana el control.
4. **Es app móvil, no webapp.** El enunciado rechaza explícitamente las aplicaciones
   tradicionales. El entregable del cliente es un APK con su hash SHA-256.
5. **El LLM no genera las cartas.** `SecureRandom` en el cliente fija la tirada; el modelo
   solo interpreta lo que ya salió. Ver `docs/decisiones.md`.

## Límite de lo que sabemos

**No tenemos el enunciado completo** (está en Moodle). Los requisitos de
`docs/requisitos.md` se derivaron de la ficha H0, y lo inferido está marcado como tal.
**No inventar requisitos del enunciado**: si algo no se puede sostener con la ficha, decirlo
y preguntar. Las preguntas abiertas para el docente están al final de ese archivo.

## Convenciones

- **Todo en español**, incluidos nombres de archivo, documentación y comentarios de código.
- Documentación en Markdown dentro de `docs/`.
- Las decisiones de diseño se registran en `docs/decisiones.md` con fecha y motivo, no se
  dejan implícitas en el código.
- La ficha del docente (`docs/h0/Registro_H0_ProyectoFinal.html`) es material de referencia:
  **no se modifica**. Nuestra respuesta vive en el JSON junto a ella.

## Datos del grupo pendientes

Código de grupo, nombres de los integrantes y el equipo donde corre el LLM siguen marcados
`«PENDIENTE»` en `docs/h0/GXX_H0_ProyectoFinal.json`. No inventarlos.
