# Oráculo — lectura de tarot conversacional con IA local

Proyecto Final de **Seguridad Informática** · Universidad Militar Nueva Granada (UMNG) · Ingeniería Multimedia · 2026-II

App móvil Android donde el usuario formula una consulta, la app revela una tirada de
tres cartas (pasado – presente – futuro) y un personaje llamado **el Oráculo**, impulsado
por un LLM que corre **localmente** (Ollama), interpreta la tirada dialogando.

Las cartas las decide el cliente con un generador aleatorio criptográfico; el LLM solo
interpreta una tirada ya fijada y no puede inventar, cambiar ni añadir cartas.

> **Lo que se califica es la seguridad, no el arte.** El tema del tarot no es decorado:
> la app trata **datos personales sensibles** (creencias, estado emocional, consultas
> íntimas), categoría sensible según el art. 5 de la Ley 1581 de 2012. De ahí salen los
> controles que el proyecto debe demostrar.

## Estado actual

| Hito | Estado |
|------|--------|
| **H0 — Registro y aprobación del proyecto** | Ficha redactada, **faltan 3 datos del grupo** |
| Desarrollo | **Bloqueado** hasta la aprobación del docente (compromiso firmado en la ficha H0) |

### Pendientes para cerrar H0

1. **Código de grupo** — en `docs/h0/GXX_H0_ProyectoFinal.json` dice `GXX`
2. **Integrantes** (2 a 3) — nombre completo y rol; hay tres roles propuestos marcados `«PENDIENTE»`
3. **Host del LLM** — nombre del integrante dueño del equipo y su apellido, para `sg-<apellido>-ai`

Luego: importar el JSON en la ficha, exportar el PDF y subir **JSON + PDF** a Moodle.
El procedimiento exacto está en [`docs/h0/README.md`](docs/h0/README.md).

## Decisiones tomadas

| Qué | Decisión |
|-----|----------|
| Tipo de proyecto | App móvil (no videojuego, no webapp) |
| Plataforma | Android — entregable: APK + hash SHA-256 |
| Framework | Flutter (Dart) |
| LLM | Llama 3.2 3B Instruct Q4_K_M en Ollama; alternativas a medir: Qwen2.5 3B, Gemma 2 2B |
| Dónde corre el LLM | Equipo de un integrante, Ollama nativo, ~8 GB RAM libres, host `sg-<apellido>-ai` |
| APIs de IA externas | **Prohibidas** por el enunciado |
| Público | Adultos 18+, con verificación de edad en el onboarding |

El razonamiento detrás de cada una está en [`docs/decisiones.md`](docs/decisiones.md).

## Estructura

```
oraculo/
├── docs/
│   ├── h0/            Ficha de registro H0 (ficha del docente + nuestra respuesta en JSON)
│   ├── concepto.md    Concepto elegido y las alternativas descartadas, con razones
│   ├── requisitos.md  Requisitos del proyecto (derivados de la ficha H0)
│   └── decisiones.md  Registro de decisiones
├── app/               Cliente Flutter · vacío hasta la aprobación H0
├── backend/           Backend seguro · vacío hasta la aprobación H0
└── llm/               System prompt y Modelfile de Ollama · vacío hasta la aprobación H0
```

Las carpetas `app/`, `backend/` y `llm/` existen solo para fijar la estructura: están
vacías a propósito, porque el grupo se comprometió a no desarrollar antes de H0.

## Vertical slice (5–10 min)

Una lectura completa, de inicio a fin:

1. Onboarding con advertencia de contenido, verificación de edad y **consentimiento informado** explícito
2. El usuario escribe su consulta en lenguaje natural
3. Baraja y corta con gesto táctil; la app revela 3 cartas con `SecureRandom`
4. El Oráculo interpreta la tirada conversando; hasta 3 repreguntas
5. La lectura se guarda en el **historial local cifrado**
6. El usuario abre el historial y ejecuta el **borrado total** (derecho de supresión), verificando que no queda rastro

Fuera de alcance: cuentas de usuario, tiradas de más de 3 cartas, las 78 cartas completas,
pagos, compartir en redes y notificaciones.

## Aviso

Este proyecto es un ejercicio académico de seguridad informática. La lectura de tarot es
ficción interactiva: el Oráculo no da consejo médico, legal ni financiero, no predice
muerte, enfermedad ni embarazo, y deriva a ayuda profesional ante señales de crisis.
