# Requisitos del proyecto final

> **Origen y límite de este documento.** El enunciado completo del proyecto final (el que
> menciona la "Parte 2" con Nginx/CSP y la lista de controles de seguridad) **no está en
> nuestras manos**: vive en Moodle. Todo lo que sigue se derivó de la **ficha de registro
> H0** (`docs/h0/Registro_H0_ProyectoFinal.html`), que es la fuente de autoridad que sí
> tenemos. Lo marcado como *(inferido)* es interpretación nuestra y hay que confirmarlo
> contra el enunciado antes de construir.

## Requisitos explícitos (textuales en la ficha H0)

### Tipo de proyecto
- Debe ser un **videojuego** o una **app móvil**. **No se aceptan aplicaciones tradicionales**
  (una webapp o app convencional que no sea juego ni app móvil).
- Nuestro caso: **app móvil instalable (Android)**, donde *el diálogo con la IA es la función central*.
- Entregable del cliente: **APK + su hash SHA-256**.

### Inteligencia artificial
- El modelo lo monta el grupo con **Ollama**, en un host llamado `sg-<apellido>-ai`.
- **No se permiten APIs de IA externas.**
- Se requiere un equipo con **~8 GB de RAM libres** para correr el modelo.

### Infraestructura
- **Backend seguro** y **todos los controles de seguridad del enunciado** aplican igual a
  videojuego y a app móvil: lo único que cambia es el cliente.
- **Nginx** aparece en la ficha como el servidor del *build* web de Unity, y la **CSP**
  se menciona como parte de la "Parte 2" del enunciado.
  *(Inferido: siendo app móvil no servimos un build web, pero el backend seguro sigue
  detrás de Nginx; hay que confirmar qué pide exactamente la Parte 2 para nuestro caso.)*

### Alcance
- **Vertical slice de 5 a 10 minutos**: una sola escena o flujo completo, construido y demostrable.

### Proceso
- **Nadie empieza a desarrollar antes de la aprobación del docente (H0).**
- Entrega de H0: **JSON + PDF** de la ficha, cargados en **Moodle**. La retroalimentación se da allí.
- Se califica la **seguridad, no el arte**.

### Normativa citada por la ficha
- **Ley 1581 de 2012** (protección de datos personales, Colombia). La ficha cita
  explícitamente el **art. 7** (datos de niñas, niños y adolescentes) al preguntar por el
  público objetivo.

## Requisitos que el proyecto se autoimpone *(nuestra propuesta, no exigencia conocida)*

Nacen del dominio elegido: la app trata datos sensibles (art. 5, Ley 1581 — creencias
religiosas o filosóficas, vida íntima), y eso es justamente lo que da material de seguridad.

| Control | Por qué |
|---|---|
| Consentimiento informado explícito antes de la primera lectura | Tratamiento de datos sensibles requiere autorización expresa |
| Verificación de edad (18+) en el onboarding | Evita el régimen especial del art. 7 para menores |
| Minimización: no pedir nombre real, fecha de nacimiento ni contacto | Lo que no se recoge no se puede filtrar |
| Historial de lecturas cifrado en reposo en el dispositivo | Contenido íntimo en un equipo que se presta o se pierde |
| Borrado total verificable desde la app | Derecho de supresión, y es demostrable en la demo |
| TLS en el canal app ↔ backend | Las consultas viajan por la red local |
| El LLM no expuesto a Internet | Ollama solo accesible por el backend |
| Cartas generadas con `SecureRandom` en el cliente, no por el LLM | Integridad del juego: el modelo no puede fabricar la tirada |
| Guardarraíles del Oráculo probados contra *prompt injection* y *jailbreak* | Es el control de seguridad propio de una app con LLM |
| Sin consejo médico, legal ni financiero; derivación ante crisis | Responsabilidad del dominio |

## Preguntas abiertas para el docente

1. ¿Qué pide exactamente la **Parte 2** (Nginx/CSP) para un proyecto que es app móvil y no build web?
2. ¿El backend debe exponerse fuera de la red local o basta LAN para la demostración?
3. ¿Hay lista cerrada de controles de seguridad a evidenciar, o se evalúa la pertinencia de los elegidos?
4. ¿El hash SHA-256 del APK se entrega firmado de alguna forma, o basta el valor?
