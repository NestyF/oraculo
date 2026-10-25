# Hito H0 — Registro del proyecto

## Archivos

| Archivo | Qué es |
|---|---|
| `Registro_H0_ProyectoFinal.html` | **Ficha del docente**, copia local del original. No se modifica. |
| `GXX_H0_ProyectoFinal.json` | **Nuestra respuesta.** Es lo que se importa en la ficha y se entrega. |

Original publicado por el docente:
`https://mirai.com.co/wp-content/uploads/2026/10/Registro_H0_ProyectoFinal.html`

La ficha es un formulario HTML autónomo: autoguarda en `localStorage` del navegador
(clave `umng_si_h0_v1`), exporta/importa JSON y genera el PDF por impresión.

## Antes de entregar: completar 3 datos

En `GXX_H0_ProyectoFinal.json`, buscar `«PENDIENTE»` y `GXX`:

1. **`grupo`** — código real del grupo (formato `GXX`)
2. **`integrantes`** — nombre completo y rol de cada uno (2 a 3). Hay tres roles
   propuestos: cliente Flutter / backend y Ollama / pruebas de seguridad y documentación.
3. **`hostLLM`** — nombre del integrante dueño del equipo y su apellido, para `sg-<apellido>-ai`

Al renombrar el archivo, usar el código real: `G07_H0_ProyectoFinal.json`, por ejemplo.
El exportador de la ficha lo nombra así automáticamente.

## Procedimiento de entrega

1. Abrir `Registro_H0_ProyectoFinal.html` en el navegador (el archivo local sirve).
2. Botón **⬆️ Importar JSON** → elegir `GXX_H0_ProyectoFinal.json`.
3. Revisar los 7 bloques en pantalla. El medidor debe marcar **100%** y las 5
   confirmaciones deben quedar marcadas.
4. Botón **🖨️ Imprimir / PDF** → guardar como PDF. La vista de impresión genera una ficha
   formal distinta del formulario, con tablas y espacio de firma.
5. Botón **⬇️ Exportar JSON** → guarda el JSON con el nombre correcto según el código de grupo.
6. Cargar **JSON + PDF** en **Moodle**. La retroalimentación del docente llega por ahí.

> El JSON de este repositorio y el exportado por la ficha son el mismo formato
> (`{fields, checks}`), así que se puede editar aquí e importar allá, o al revés.

## Verificación hecha

Los valores de lista del JSON se compararon contra las opciones del HTML
(`plataforma`, `framework`, `buildApp`, `interaccion`, `genero`, `tipo`): coinciden
exactamente, de modo que al importar se seleccionan solos en lugar de quedar vacíos.
Los 9 campos obligatorios que la ficha exige están llenos.

## Recordatorio

La confirmación `c_dev` de la ficha compromete al grupo a **no empezar a desarrollar antes
de la aprobación del docente**. Por eso `app/`, `backend/` y `llm/` están vacías.
