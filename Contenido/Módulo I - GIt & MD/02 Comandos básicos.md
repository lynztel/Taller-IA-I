---
tags:
  - taller-ia
  - modulo-1
  - git
modulo: 1
aliases:
  - Comandos Git
  - Git básico
---

> [!info] Flujo básico de Git
> Los cambios viajan por tres zonas: **directorio de trabajo** → **área de preparación** (*staging area*) → **historial del repositorio**. `git add` mueve cambios de la primera a la segunda; `git commit` los registra en la tercera.

> [!warning] Antes del primer commit
> Configura tu identidad con `git config` (comando 8). Sin ella, Git puede rechazar el commit o firmarlo con datos inferidos del sistema.

## 1. `git init`

**Función:** inicializa un repositorio Git nuevo en la raíz del proyecto actual.

```bash
git init
```

- **Mecanismo:** crea un subdirectorio oculto `.git/` donde se alojan la base de datos de objetos (*blobs*, *trees*, *commits*), las configuraciones locales y los punteros de ramas. Desde este comando, la carpeta pasa de ser un directorio ordinario a un árbol de trabajo bajo control de versiones.

> [!note] `main` vs. `master`
> Una rama es un puntero móvil a un commit; el nombre de la rama principal es solo una **convención**, Git no le da un trato especial.
>
> - **`master`** es el nombre que Git usa históricamente para la rama inicial. Según su documentación, `git init` todavía crea `master` por defecto, y ese valor cambiará a `main` cuando se publique Git 3.0.
> - **`main`** es el nombre que GitHub asigna a los repositorios **nuevos** desde el 1 de octubre de 2020. Los repositorios existentes no cambiaron.
> - Consecuencia práctica: un repositorio creado con `git init` puede tener `master` en local mientras GitHub espera `main`. Por eso en [[03 Github]] se ejecuta `git branch -M main` antes del primer `push`.
>
> ```bash
> git branch --show-current                      # ¿cómo se llama tu rama actual?
> git init -b main                               # crear el repositorio ya con rama main
> git config --global init.defaultBranch main    # main por defecto en todos tus repos nuevos
> ```
>
> En estas notas se usa `main`. Si tu repositorio usa `master`, sustituye el nombre en los comandos.

## 2. `git status`

**Función:** inspecciona el estado del árbol de trabajo en comparación con el índice y el último commit.

- **Mecanismo:** clasifica los archivos detectados en tres estados:
    - **Untracked (sin seguimiento):** archivos nuevos que Git aún no vigila.
    - **Modified (modificados):** archivos bajo seguimiento con cambios no preparados.
    - **Staged (preparados):** modificaciones listas para formar parte de la siguiente instantánea.

## 3. `git add`

**Función:** mueve las modificaciones seleccionadas del directorio de trabajo al área de preparación (*staging area*).

- **Mecanismo:** toma una copia exacta del archivo tal como está en ese instante y la indexa.
    - `git add <archivo>`: agrega un archivo o ruta específica de manera granular.
    - `git add .`: agrega recursivamente todos los cambios, adiciones y eliminaciones del directorio actual hacia abajo.

## 4. `git commit -m "<mensaje>"`

**Función:** registra de forma permanente los cambios del área de preparación en el historial del repositorio.

- **Mecanismo:** genera un objeto de confirmación (*commit*) con un identificador único (hash criptográfico), fecha, autor, referencia al commit predecesor y la estructura de archivos indexada.
    - La bandera `-m` asigna un mensaje descriptivo breve que documenta el propósito o la unidad lógica del cambio, sin abrir el editor de texto interactivo por defecto.

## 5. `git log`

**Función:** muestra el historial cronológico inverso de las confirmaciones registradas en la rama actual.

- **Mecanismo:** recorre la cadena de commits siguiendo los punteros a los padres desde la posición de `HEAD`.
    - Variantes útiles:
        - `git log --oneline`: compacta cada commit en una línea con su hash corto y mensaje.
        - `git log --graph`: dibuja la bifurcación visual de las ramas.

## 6. `git diff`

**Función:** muestra las diferencias exactas, a nivel de líneas y caracteres, entre los distintos estados de los archivos.

- **Mecanismo:**
    - `git diff`: diferencias entre el directorio de trabajo y el área de preparación (*cambios no indexados*).
    - `git diff --staged` (o `--cached`): diferencias entre el área de preparación y el último commit (*lo que efectivamente entrará en el próximo commit*).

## 7. `git checkout`

*Navegación en el historial y entre ramas.*

**Función:** mueve el puntero `HEAD` para situarse en un commit antiguo específico o volver a una rama.

- **Mecanismos mostrados:**
    - `git checkout <hash>`: "viaje en el tiempo". Sitúa el directorio de trabajo exactamente en el estado de esa confirmación previa (modo *detached HEAD*), lo que permite inspeccionar o probar el código tal como estaba.
    - `git checkout main` (o `master`, según el nombre de tu rama principal): vuelve a la punta de la rama principal y restaura los archivos a su versión de desarrollo más reciente.

> [!tip] Profundiza
> El detalle de cómo regresar a versiones anteriores y deshacer cambios está en [[04 Recuperar versiones]].

## 8. `git config`

*Configuración de identidad.*

**Función:** establece las variables que identifican quién realiza los cambios, antes de ejecutar el primer commit.

- **Mecanismo:**

    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu_correo@ejemplo.com"
    ```

    Git incrusta estos metadatos en cada firma de commit que generes en el sistema.

## Siguiente

Para conectar tu repositorio local con la nube, continúa con [[03 Github]]. Referencia oficial de comandos: [[Git, GitHub y Markdown]].

← [[00 Módulo I - Índice]]
