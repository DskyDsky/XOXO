# PLANTILLA UNIVERSAL DE PROYECTO PARA CLAUDE CODE

> Este archivo es una guía completa y autocontenida. Puedes pegarlo directamente en una
> conversación con Claude Code y pedirle: "lee esto y crea la estructura de carpetas
> y archivos que describe en mi proyecto actual". Sirve para CUALQUIER tipo de proyecto:
> código, investigación, escritura, gestión de conocimiento, negocio, lo que sea.

---

## 1. POR QUÉ EXISTE ESTA ESTRUCTURA

Cada sesión de Claude Code empieza con el contexto en cero. Solo hay dos formas de que
Claude recuerde algo entre sesiones sin que tú se lo repitas:

1. **Archivos `CLAUDE.md`** — instrucciones que tú escribes y que se cargan automáticamente
   al iniciar cada sesión.
2. **Auto memory** (`.claude/memory/`) — notas que Claude escribe solo, basadas en lo que
   aprende trabajando contigo (patrones, convenciones, decisiones).

El objetivo de esta plantilla es simple: que lo esencial se cargue siempre (barato, rápido),
y que todo lo demás se cargue solo cuando hace falta (evitando gastar tokens en cada turno
con información que no aplica a lo que estás haciendo en ese momento).

**Aclaración importante**: Claude Code no detecta automáticamente cuándo un archivo de
`.claude/rules/` es relevante y lo carga solo. Pero cuidado con la solución obvia:
`@archivo.md` dentro de `CLAUDE.md` NO es condicional, es una carga inmediata. Si
referencias una regla con `@`, esa regla se carga completa en cada sesión sin importar
si aplica o no — exactamente igual que si la hubieras pegado directo en `CLAUDE.md`. Eso
rompe el objetivo de esta sección.

Hay dos formas reales de lograr carga bajo demanda:
- **Skill** (`.claude/skills/`, con `SKILL.md` y frontmatter `description`): Claude decide
  solo, según la situación, si la activa. Es la única carga verdaderamente automática y
  condicional. Ver sección 6b.
- **Referencia en texto plano** (sin `@`) dentro de `CLAUDE.md`, del tipo "si trabajas en
  [área], lee `.claude/rules/archivo.md`": no se carga sola, pero avisa a Claude que el
  archivo existe para que lo lea cuando reconozca que aplica. Depende de que Claude note
  la instrucción — menos automático que una skill, pero evita el gasto de cargarla siempre.

Ver sección 4 para el detalle de cómo estructurar cada regla.

Regla de oro que rige todo lo demás: **un CLAUDE.md raíz de menos de 200 líneas**. Pasado
ese umbral, la adherencia de Claude a las instrucciones empieza a degradarse — es un
presupuesto, no una sugerencia.

---

## 2. ESTRUCTURA DE CARPETAS A CREAR

```
mi-proyecto/
├── CLAUDE.md                  # Contexto esencial. Se carga SIEMPRE.
├── CLAUDE.local.md            # Notas personales, no se comparte (gitignore si aplica)
├── .claude/
│   ├── rules/                 # Reglas específicas por tema/área. Carga solo si aplica.
│   │   └── ejemplo.md
│   ├── memory/
│   │   └── memory.md          # Bitácora manual (no es la auto-memoria real, ver sección 5)
│   └── skills/                # Solo si vas a crear skills invocables, ver sección 6b
├── docs/                      # Documentación de fondo, extensa. Se referencia, no se copia.
│   └── contexto-general.md
└── (contenido real del proyecto: código, textos, notas, datos...)
```

Instrucción para Claude Code: **crea exactamente esta estructura de carpetas y archivos
dentro del directorio actual**, usando el contenido de las secciones 3 a 6 como contenido
inicial de cada archivo.

---

## 3. CONTENIDO INICIAL DE `CLAUDE.md` (raíz)

```markdown
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
> (sección 6b) en vez de regla.

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
```

> Nota: esta última sección ("Cómo prefiero que trabajes conmigo") es opcional pero muy
> recomendable — es donde va tu forma de trabajo personal, y aplica igual sin importar
> el tipo de proyecto.

---

## 4. CONTENIDO INICIAL DE `.claude/rules/ejemplo.md`

```markdown
# Regla: [nombre del área o tema]

Aplica cuando: [en qué carpeta, tipo de archivo, o situación se activa esta regla]

## Detalle
[Instrucciones específicas de este tema/área que NO necesitan estar siempre cargadas,
solo cuando se está trabajando en esto]

## Ejemplos
- Correcto: [ejemplo concreto]
- Evitar: [ejemplo concreto]
```

Usa un archivo separado por cada área temática grande del proyecto (ej: si es código,
uno por módulo/backend/frontend; si es un libro, uno por línea narrativa o personaje;
si es investigación, uno por metodología o fuente). Así solo se carga lo relevante al
trabajo del momento, no todo junto.

Estas reglas se referencian en texto plano desde `CLAUDE.md` (nunca con `@`), para que la
carga dependa de que Claude reconozca la situación, no de una importación automática. Si
una regla se activa todo el tiempo, o necesitas que dispare sola sin depender de que Claude
la recuerde, muévela a `.claude/skills/` como Skill (sección 6b) — ese es el mecanismo con
activación automática real.

---

## 5. CONTENIDO INICIAL DE `.claude/memory/memory.md`

**Aclaración importante**: esto NO es el sistema real de auto-memoria de Claude Code.
La auto-memoria real de Claude vive fuera de este proyecto, en una carpeta global del
usuario (organizada por tipo: user/feedback/project/reference, con su propio índice
`MEMORY.md`), y se revisa con el comando `/memory` dentro de una sesión. Ese sistema
existe independientemente de si creas o no esta carpeta.

Lo que va aquí es un **registro manual/simulado**, mantenido por ti (o por Claude a tu
pedido explícito, nunca solo), pensado como bitácora de decisiones propias de este
proyecto en particular — útil, pero distinto de la memoria automática real. El archivo
lo deja explícito para no confundir ambas cosas:

```markdown
# Bitácora de decisiones — [nombre del proyecto]

> Esto es un registro MANUAL, no la auto-memoria real de Claude Code (esa vive en la
> carpeta global del usuario y se revisa con /memory). Aquí se anota, a pedido explícito,
> decisiones o aprendizajes propios de este proyecto que quieras dejar por escrito.

| Fecha | Decisión / aprendizaje | Por qué |
|-------|-------------------------|---------|
|       |                         |         |
```

Instrucción para Claude Code: no llenes esta tabla al crear la estructura; déjala vacía.
Solo se actualiza cuando el usuario pida explícitamente "anota esto en la bitácora".

---

## 6. CONTENIDO INICIAL DE `docs/contexto-general.md`

```markdown
# Contexto general — [nombre del proyecto]

[Aquí va toda la documentación de fondo extensa: historia del proyecto, decisiones
de arquitectura o metodología, referencias externas, glosario completo, etc.
Todo lo que sea importante pero NO necesite estar cargado en cada sesión.
El CLAUDE.md raíz solo referencia este archivo con @docs/contexto-general.md,
nunca copia su contenido.]
```

---

## 6b. `.claude/skills/` — solo si quieres skills invocables de verdad

Esta carpeta en el árbol de la sección 2 es opcional. Hay dos formas de usarla:

**Opción A — solo carpeta de referencia** (más simple): guardas ahí notas o
procedimientos que tú o Claude leen manualmente cuando hace falta. No requiere nada
especial, pero tampoco Claude la detecta ni la invoca solo.

**Opción B — skills invocables de verdad**: para que Claude Code reconozca y active un
procedimiento por su cuenta cuando la situación coincide, cada skill necesita su propio
`SKILL.md` con frontmatter obligatorio:

```markdown
---
name: nombre-de-la-skill
description: "Descripción de cuándo activar esta skill — sé específico con las frases
o situaciones que deben dispararla, porque Claude decide si usarla basándose en esta
descripción, no en el nombre."
---

# [Nombre de la skill]

[Contenido: el procedimiento paso a paso que Claude debe seguir cuando esta skill
se activa]
```

Instrucción para Claude Code: si el usuario no especifica cuál opción quiere, pregunta
antes de crear archivos dentro de `.claude/skills/` — la diferencia entre A y B cambia
si hace falta escribir frontmatter o no.

---

## 7. INSTRUCCIÓN FINAL PARA CLAUDE CODE

Al recibir este archivo, Claude Code debe:

1. Preguntar el nombre y tipo del proyecto si no se ha indicado.
2. Crear la estructura de carpetas de la sección 2.
3. Rellenar cada archivo con las plantillas de las secciones 3 a 6, sustituyendo los
   placeholders `[...]` con la información que el usuario proporcione o, si falta algo,
   dejando el placeholder visible y preguntando antes de inventar contenido.
4. No sobrescribir archivos existentes sin confirmación explícita.
5. Confirmar al final qué se creó y sugerir el siguiente paso: correr `/memory` tras
   unas sesiones de trabajo real para revisar qué aprendió solo y así poder podar el
   CLAUDE.md de cualquier cosa redundante.
