# Registro de decisiones

Formato: qué se decidió, cuándo, por qué, y qué habría que revisar si cambia el contexto.

## 2026-10-24 — App móvil en lugar de videojuego

La ficha H0 permite videojuego (Unity 6 / UE5) o app móvil. Se eligió **app móvil** porque
el concepto es conversacional: la lectura de tarot *es* diálogo, y la ficha exige que en
una app móvil "el diálogo con la IA sea la función central". Un videojuego habría obligado
a construir un vertical slice jugable de 5–10 min con motor, arte y mecánicas, trabajo que
no aporta nota en una materia que **califica la seguridad, no el arte**.

**Costo asumido:** se renuncia al ejercicio de CSP sobre un build WebGL servido por Nginx,
que era el camino más directo para esa parte del enunciado. Hay que confirmar con el
docente qué pide la Parte 2 para una app móvil (ver `requisitos.md`).

## 2026-10-24 — Concepto «Oráculo» (tarot conversacional)

Sobre la idea original del grupo (*tarot o póker*) se evaluaron tres conceptos. Se eligió
el tarot conversacional directo: el póker dejaba a la IA como adorno, y el *serious game*
de ingeniería social («Sombra») era más fuerte temáticamente pero más caro de construir y
de acotar éticamente. El detalle de la comparación está en `concepto.md`.

## 2026-10-24 — Las cartas las genera el cliente, no el LLM

La tirada se determina con un generador aleatorio criptográfico (`SecureRandom`) en el
cliente y se pasa al modelo como dato ya fijado. El LLM solo interpreta.

**Por qué:** si el modelo "saca" las cartas, la integridad del juego depende de un
componente no determinista e influenciable por la entrada del usuario — un usuario podría
pedir su carta favorita. Separar *azar* de *narración* hace el azar auditable y convierte
cualquier intento de manipular la tirada en un fallo detectable, no en un comportamiento
plausible del modelo.

## 2026-10-24 — Flutter (Dart) + Android

Frente a Kotlin nativo, React Native y multiplataforma Android+iOS:

- **Flutter:** un solo lenguaje, APK directo, y soporte razonable para los controles que
  necesitamos (almacenamiento cifrado, *certificate pinning*).
- **Kotlin nativo** daría mejores controles de plataforma de fábrica
  (`EncryptedSharedPreferences`, Keystore, Network Security Config) a cambio de más código.
- **iOS** se descartó: exige Mac y cuenta de desarrollador, y duplica la superficie de
  entrega sin sumar nota.

**Revisar si:** el grupo ya domina Kotlin, o si el docente exige controles específicos de
plataforma Android — en ese caso Kotlin nativo es la mejor apuesta.

## 2026-10-24 — Llama 3.2 3B Instruct Q4_K_M como modelo propuesto

Cabe en ~8 GB de RAM con margen, responde aceptablemente en español y está en el catálogo
de Ollama. Se registran **Qwen2.5 3B Instruct** y **Gemma 2 2B** como alternativas, con la
decisión final sujeta a medir calidad en español y latencia en el equipo real del grupo.
La ficha H0 se redactó dejando esa medición explícita, para no quedar amarrados a un modelo
antes de probarlo.

## 2026-10-24 — Público adulto (18+) con verificación de edad

Evita el régimen especial del **art. 7 de la Ley 1581 de 2012** (tratamiento de datos de
menores), que habría abierto un frente de cumplimiento adicional sobre un contenido que
además no es apropiado para menores. La verificación de edad entra en el onboarding.

## 2026-10-24 — LLM en el equipo de un integrante, Ollama nativo

Frente a aislarlo en una VM (Multipass/VirtualBox): se prioriza simplicidad y rendimiento
—una VM se come RAM que el modelo necesita— aceptando que el aislamiento es más débil. El
host se nombra `sg-<apellido>-ai` como pide la ficha y **no se expone a Internet**: solo el
backend lo consume.

**Revisar si:** el enunciado exige aislamiento del servicio de IA; entonces toca VM o
contenedor.
