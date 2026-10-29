# Plantilla Universal de Proyecto para Claude Code

Repo maestro. **No se trabaja aquí directamente** — se clona una copia por cada
proyecto nuevo y se desvincula del repo maestro antes de empezar (ver
[`COMO EMPEZAR UN PROYECTO NUEVO.md`](COMO%20EMPEZAR%20UN%20PROYECTO%20NUEVO.md)).

Sirve para **cualquier tipo de proyecto** — código, investigación, escritura,
gestión de conocimiento, negocio, lo que sea. No está atada a ningún stack ni
dominio en particular.

---

## Por qué existe

Cada sesión de Claude Code empieza con el contexto en cero. Solo hay dos formas
de que Claude recuerde algo entre sesiones sin que se lo repitas cada vez:

1. **`CLAUDE.md`** — instrucciones que tú escribes y que se cargan automáticamente
   al iniciar cada sesión.
2. **Auto-memoria real de Claude Code** — notas que Claude escribe solo, basadas
   en lo que aprende trabajando contigo. Vive fuera de este repo, en una carpeta
   global del usuario, y se revisa con `/memory`.

Esta plantilla organiza lo primero (`CLAUDE.md` y los archivos que lo acompañan)
siguiendo una regla simple: **lo esencial se carga siempre, todo lo demás se
carga solo cuando hace falta**. Eso evita gastar tokens en cada turno con
información que no aplica a lo que se está haciendo en ese momento.

Regla de oro: un `CLAUDE.md` raíz de **menos de 200 líneas**. Pasado ese umbral,
la adherencia de Claude a las instrucciones empieza a degradarse — es un
presupuesto, no una sugerencia.

---

## Estructura del repo

```
_PLANTILLA UNIVERSAL - PROYECTO CLAUDE/
├── README.md                          # Este archivo
├── CLAUDE.md                          # Contexto esencial del proyecto. Se carga SIEMPRE.
├── CLAUDE.local.md                    # Notas personales, no se comparte (en .gitignore)
├── COMO EMPEZAR UN PROYECTO NUEVO.md  # Flujo clonar → desvincular → trabajar
├── .gitignore
├── .claude/
│   ├── rules/
│   │   └── ejemplo.md                 # Regla de ejemplo — cargar solo cuando aplica
│   ├── memory/
│   │   └── memory.md                  # Bitácora manual de decisiones (NO es la auto-memoria real)
│   └── skills/
│       └── README.md                  # Explica cuándo usar referencia simple vs skill invocable
└── docs/
    ├── contexto-general.md            # Placeholder para documentación de fondo extensa
    └── PLANTILLA-PROYECTO-CLAUDE.md   # Guía completa: por qué y cómo de cada pieza
```

---

## Piezas clave y para qué sirve cada una

### `CLAUDE.md`
Se carga en cada sesión. Trae los placeholders (`[NOMBRE DEL PROYECTO]`, etc.)
sin rellenar a propósito — al clonar la plantilla para un proyecto real, hay que
completarlos con los datos de ese proyecto, nunca inventarlos.

### `.claude/rules/`
Reglas específicas por área o tema que **no** necesitan estar cargadas todo el
tiempo. Se referencian en **texto plano, sin `@`**, desde la sección "Reglas por
área" de `CLAUDE.md` — así Claude las lee solo cuando reconoce que la situación
aplica.

> **Importante:** `@archivo.md` dentro de `CLAUDE.md` NO es condicional — carga
> el archivo completo en cada sesión, sin importar si aplica. Usar `@` en una
> regla anula el propósito de tenerla separada. El detalle completo está en
> `docs/PLANTILLA-PROYECTO-CLAUDE.md`, sección 1.

### `.claude/memory/memory.md`
Una bitácora **manual** de decisiones propias del proyecto, mantenida por ti o
por Claude solo cuando se lo pides explícitamente. No es la auto-memoria real
de Claude Code (esa vive fuera del repo y se revisa con `/memory`) — el archivo
lo deja explícito para no confundir ambas cosas.

### `.claude/skills/`
Opcional. Solo tiene sentido si necesitas que Claude **active un procedimiento
por su cuenta** según la situación (a diferencia de las reglas, que dependen de
que Claude decida leerlas). Cada skill real necesita su propio `SKILL.md` con
frontmatter `name` + `description`. Ver `.claude/skills/README.md` antes de
crear la primera.

### `docs/`
Documentación de fondo que **no** debe cargarse en cada sesión. Se referencia
desde `CLAUDE.md` con `@docs/contexto-general.md` (aquí sí conviene `@`, porque
se quiere que cargue siempre que se abra `CLAUDE.md` — es la excepción a la
regla de las rules). `PLANTILLA-PROYECTO-CLAUDE.md` es la guía original,
completa, de por qué y cómo está armada toda la plantilla.

---

## Cómo usar esta plantilla

1. Clona el repo en la carpeta del proyecto nuevo.
2. Borra el `.git` de la copia y corre `git init` fresco — la copia debe ser un
   repo propio, no un clon que sigue apuntando a este repo maestro.
3. Llena `CLAUDE.md` con los datos reales (nombre, tipo, contexto, reglas).
4. Trabaja solo en la copia. Esta plantilla se queda intacta para el siguiente
   proyecto.

Instrucciones completas, con los comandos exactos, en
[`COMO EMPEZAR UN PROYECTO NUEVO.md`](COMO%20EMPEZAR%20UN%20PROYECTO%20NUEVO.md).
