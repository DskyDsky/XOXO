# Cómo empezar un proyecto nuevo desde esta plantilla

Esta carpeta es el repo maestro: **https://github.com/DskyDsky/plantilla-universal-claude-code**

Nunca se trabaja directamente aquí — se clona una copia nueva por cada proyecto
y se desvincula del repo maestro antes de empezar.

---

## Instrucción para Claude Code

Si el usuario pide arrancar un proyecto nuevo desde esta plantilla (ej. "monta un
proyecto nuevo con la plantilla", "clona la plantilla para X"), Claude debe
**ejecutar los pasos de abajo por su cuenta**, sin que el usuario tenga que
copiar y pegar comandos:

1. Preguntar (si no se dio ya) el nombre del proyecto y su ubicación de destino.
2. Clonar, desvincular, `git init` y hacer el primer commit — pasos 1 y 2 de abajo.
3. Llenar `CLAUDE.md` con los datos reales que el usuario dé; si falta algo,
   dejar el placeholder visible y preguntar — nunca inventar.
4. Confirmar al final qué se creó y dónde.

**Regla dura: nunca modificar, commitear ni hacer push dentro de
`_PLANTILLA UNIVERSAL - PROYECTO CLAUDE`** (el repo maestro) al montar un
proyecto nuevo. Todo el trabajo pasa a la copia clonada — el maestro se queda
intacto como punto de partida para el siguiente proyecto. Si el usuario pide
explícitamente cambiar la plantilla misma (no un proyecto nuevo), eso sí se
hace aquí, pero es un pedido distinto y debe quedar claro que es sobre el
maestro.

---

## Pasos

1. **Clonar** en la ubicación del proyecto nuevo:
   ```powershell
   git clone https://github.com/DskyDsky/plantilla-universal-claude-code "C:\Users\jotae\Desktop\NOMBRE DEL PROYECTO"
   ```

2. **Desvincular la copia del repo maestro** — para que sea su propio repo
   independiente, no un clon que apunta de vuelta a la plantilla:
   ```powershell
   cd "C:\Users\jotae\Desktop\NOMBRE DEL PROYECTO"
   Remove-Item -Recurse -Force .git
   git init
   git add -A
   git commit -m "Proyecto nuevo desde plantilla universal"
   ```

3. **Llenar `CLAUDE.md`** con los datos reales del proyecto (nombre, tipo, contexto,
   reglas) — Claude debe preguntar esto si no se lo das, nunca inventarlo.

4. **Trabajar solo en la copia**, nunca en `_PLANTILLA UNIVERSAL - PROYECTO CLAUDE`.
   Esa carpeta se queda intacta como punto de partida para el siguiente proyecto.

---

## Si además quieres un remoto en GitHub para el proyecto nuevo

Los pasos de arriba dejan el proyecto nuevo como repo local únicamente (sin
remoto — se desvinculó del repo maestro a propósito). Si quieres que el
proyecto nuevo también tenga su propio repo en GitHub, pídemelo aparte —
implica crear un repositorio nuevo en tu cuenta, así que se confirma antes de
hacerlo (nombre y visibilidad: público o privado).
