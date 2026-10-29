> **Nota para Claude Code:** si esta carpeta es `_PLANTILLA UNIVERSAL - PROYECTO
> CLAUDE` (el repo maestro) y el usuario pide iniciar un proyecto nuevo, lee y
> ejecuta `COMO EMPEZAR UN PROYECTO NUEVO.md` en vez de editar este archivo aquí.
> El resto de este `CLAUDE.md` es la plantilla que se llena en la copia clonada,
> no en el maestro. Borra esta nota en la copia clonada una vez llenado.

# [NOMBRE DEL PROYECTO]

## Qué es
[Una o dos líneas: qué es este proyecto, para qué existe, para quién es]

## Tipo de proyecto
[Ej: código / investigación / escritura / gestión de conocimiento / negocio / mixto]

## Contexto esencial
[Los 3-5 datos que Claude NO puede inferir solo con ver los archivos:
stack técnico, metodología, personas involucradas, restricciones importantes, etc.]

## Estructura del proyecto
- [carpeta/] — qué contiene y para qué sirve
- [carpeta/] — qué contiene y para qué sirve
- Documentación de fondo: @docs/contexto-general.md

## Reglas por área (Claude las lee cuando reconoce que aplican — sin @, nunca se cargan solas)
- Trabajando en [área/tema 1] → lee `.claude/rules/ejemplo.md`
- Trabajando en [área/tema 2] → lee `.claude/rules/[otro-archivo].md`

> Sin `@`, estas rutas no se cargan automáticamente — quedan como instrucción para que
> Claude las lea solo si la situación lo amerita. Si necesitas que la activación sea
> realmente automática y no dependa de que Claude "se acuerde", conviértela en Skill
> (ver `.claude/skills/`).

## Comandos / flujos frecuentes
[Si aplica: comandos exactos de build/test/run.
Si no es un proyecto técnico: los pasos o rutinas que se repiten]

## Reglas inmutables
1. [Regla concreta y verificable] — por qué: [razón breve]
2. [Regla concreta y verificable] — por qué: [razón breve]
3. [Regla concreta y verificable] — por qué: [razón breve]

## Terminología del proyecto
- Usar "[término]" no "[alternativa]" — [por qué]

## Cómo prefiero que trabajes conmigo
- Comprende el contexto completo antes de proponer cambios
- Distingue claramente entre hechos, observaciones, inferencias y recomendaciones
- No inventes información; si falta un dato, pregúntalo
- Cambios mínimos necesarios, no reescrituras completas sin motivo
- Explica el razonamiento técnico o metodológico detrás de cada recomendación
