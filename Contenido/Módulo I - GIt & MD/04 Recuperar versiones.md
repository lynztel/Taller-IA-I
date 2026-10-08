---
tags:
  - taller-ia
  - modulo-1
  - git
modulo: 1
aliases:
  - Deshacer cambios en Git
  - Viajar en el tiempo
---

> [!info] Qué resuelve esta nota
> Git conserva todo el historial, así que casi siempre se puede volver atrás. Esta nota agrupa los comandos según **qué quieres deshacer**: inspeccionar el pasado, descartar cambios sin commit o deshacer commits ya hechos. Requiere conocer [[02 Comandos básicos]].

## 1. Inspección del historial

- **`git log`**: imprime el historial cronológico inverso de commits de la rama actual, con el hash SHA-1 (necesario para viajar en el tiempo), autor, fecha y mensaje.
- **`git log --oneline`**: variante compacta con solo el hash abreviado y la primera línea del mensaje de cada commit; útil para identificar rápidamente a qué punto regresar.

## 2. Viajar en el tiempo (inspección)

- **`git checkout <commit-hash>`**: mueve `HEAD` directamente al commit indicado y deja el repositorio en estado **detached HEAD** (desacoplado de cualquier rama). El directorio de trabajo se sincroniza con el *snapshot* exacto de ese commit; los cambios posteriores no se borran, solo quedan fuera de la vista actual.
- **`git checkout main`** (o `master`): vuelve a acoplar `HEAD` a la punta de la rama principal y devuelve los archivos a la versión más reciente.

> [!note] Nota técnica
> En versiones modernas de Git, para cambiar de rama también existe el comando especializado `git switch <rama>`.

## 3. Descartar cambios locales (sin commit)

- **`git restore <archivo>`** (clásico: `git checkout -- <archivo>`): descarta las modificaciones no confirmadas del directorio de trabajo, sobrescribiendo el archivo con la última versión registrada en el commit actual o en el área de preparación.
- **`git restore --staged <archivo>`** (clásico: `git reset HEAD <archivo>`): quita un archivo del *staging area* (donde entra con `git add`) y lo regresa a "cambios no preparados", sin borrar su contenido en disco.

> [!warning] `git restore <archivo>` no tiene vuelta atrás
> Los cambios sin commit que se descartan no están en el historial, por lo que no se pueden recuperar.

## 4. Deshacer commits existentes

- **`git reset --hard HEAD~1`** (o apuntando al hash anterior): «elimina» el último commit. Retrocede el puntero de la rama y `HEAD` al commit anterior, **borrando** el commit del historial visible y los cambios que traía en el directorio de trabajo.
- **`git reset --soft HEAD~1`**: retrocede la rama al commit anterior pero preserva los cambios de ese commit en el *staging area*, listos para volver a ejecutar `git commit` (ideal para corregir un mensaje o agrupar cambios).
- **`git reset --mixed HEAD~1`** (comportamiento por defecto de `git reset`): retrocede la rama y saca los cambios del *staging*, manteniéndolos en disco como modificaciones pendientes de preparar.
- **`git revert <commit-hash>`**: alternativa segura para repositorios compartidos. En lugar de reescribir la historia eliminando commits, genera un **nuevo commit** que aplica la operación inversa de los cambios introducidos por el commit seleccionado.

> [!danger] `git reset --hard` descarta cambios en el directorio de trabajo
> Sobrescribe los archivos con el estado del commit destino, así que **los cambios sin commit en archivos con seguimiento se pierden** y no hay forma de recuperarlos (los archivos *untracked* no se tocan).
>
> Lo que sí se puede recuperar es el *commit* «eliminado»: Git conserva su objeto un tiempo y el `reflog` registra dónde estuvo `HEAD`.
>
> ```bash
> git reflog                  # lista los movimientos recientes de HEAD
> git reset --hard HEAD@{1}   # vuelve al estado previo al reset (o usa el hash que muestre el reflog)
> ```
>
> El `reflog` es local y sus entradas caducan (por defecto, a los 30 o 90 días según el caso), por lo que no sustituye a un respaldo en [[03 Github]].

> [!warning] Reescribir historia en repositorios compartidos
> `git reset` mueve la rama hacia atrás y cambia el historial. Si ya hiciste `push`, otras personas pueden quedar con commits que ya no existen en tu rama. En ese caso usa `git revert`.

### Resumen: ¿qué comando uso?

| Comando                  | Historial (commits) | Staging area | Archivos en disco |
| ------------------------ | :-----------------: | :----------: | :---------------: |
| `git reset --soft HEAD~1`  | Retrocede           | Conserva cambios | Conserva cambios |
| `git reset --mixed HEAD~1` | Retrocede           | Se vacía     | Conserva cambios  |
| `git reset --hard HEAD~1`  | Retrocede           | Se vacía     | Se borran cambios |
| `git revert <hash>`        | Agrega commit inverso | —          | Aplica la inversa |

## Siguiente

Con el historial local dominado, continúa con [[03 Github]] para respaldarlo en la nube.

← [[00 Módulo I - Índice]]
