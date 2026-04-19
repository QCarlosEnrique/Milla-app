# Milla-app — Instrucciones para Claude Code

App de estudio para Millaray (nivel básico, currículum chileno).
Un solo archivo: `index.html` contiene todo el CSS, HTML y JS.

## Flujo de contenido nuevo

Cuando el usuario diga "procesa el contenido nuevo" o similar:

1. Listar archivos en `content/pendiente/`
2. Por cada archivo:
   - Si es PDF → usar skill `anthropic-skills:pdf` para extraer texto
   - Si es imagen (jpg, png, etc.) → leer directamente con Read tool (Claude es multimodal)
3. Identificar el tema y la materia según el contenido extraído
4. Generar preguntas nuevas en el formato existente del banco (ver abajo)
5. Insertar las preguntas en `index.html` dentro del bloque de datos correspondiente
6. Mover el archivo procesado de `content/pendiente/` a `content/procesado/`

## Estructura de preguntas en index.html

### Inglés — bloques en `ENG_BLOCKS`
```js
{
  icon: '🎯', title: 'Título del bloque',
  desc: 'Descripción breve',
  color: 'linear-gradient(135deg,#8e44ad,#2980b9)', shadow: '#5b2c6f',
  questions: [
    // Selección múltiple:
    { text: 'Pregunta o frase', type: 'mc', opts: ['A','B','C','D'], correct: 0 },
    // Verdadero/Falso:
    { text: 'Afirmación', type: 'tf', correct: true, explanation: 'Explicación breve' },
  ]
}
```

### Matemática — generadores en funciones `genMult`, `genDiv`, `genCombo`
Las preguntas se generan dinámicamente. Si el contenido nuevo incluye
un tipo de operación no cubierto, agregar un nuevo generador o ampliar
los templates existentes en la función correspondiente.

## Materias disponibles para activar (actualmente "Próximamente")
- Lenguaje (`card-lang`) — onclick apunta a `showComingSoon('lang')`
- Ciencias (`card-sci`) — onclick apunta a `showComingSoon('sci')`
- Historia (`card-hist`) — onclick apunta a `showComingSoon('hist')`

Para activar una materia:
1. Quitar `showComingSoon(...)` del onclick y el badge "Próximamente"
2. Crear pantalla de temas similar a la de Inglés
3. Agregar banco de preguntas en el JS

## Convenciones
- Todo el texto en español (excepto Inglés que es bilingüe)
- Tono motivador, nombre "Millaray" en los mensajes de feedback
- Mantener el estilo visual existente (colores por materia definidos en CSS)
- No crear archivos nuevos — todo va en `index.html`
