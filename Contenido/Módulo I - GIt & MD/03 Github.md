---
tags:
  - taller-ia
  - modulo-1
  - github
modulo: 1
aliases:
  - GitHub
  - Conectar con GitHub
---

> [!info] Qué es GitHub
> Plataforma web de alojamiento remoto para repositorios Git. Mientras Git es la herramienta de control de versiones distribuido que opera en tu máquina local, GitHub actúa como el servidor centralizado en la nube.

## Funciones principales

- **Respaldo y sincronización:** mantiene una copia remota del historial completo de confirmaciones (*commits*), independiente de tu equipo.
- **Colaboración y control de cambios:** permite flujos de trabajo en equipo mediante ramas (*branches*), solicitudes de integración (*pull requests*) y revisión de código (*code review*).
- **Trazabilidad y gestión:** integra seguimiento de incidencias (*issues*), tableros de gestión de proyectos y automatización de flujos de trabajo (*GitHub Actions / CI/CD*).

> [!warning] El historial remoto no es inmutable
> Que GitHub guarde una copia no significa que no se pueda alterar. Un `git push --force` desde un clon local puede **sobrescribir** el historial de la rama remota y hacer desaparecer commits. En repositorios compartidos conviene activar la protección de ramas (*branch protection rules*) para bloquear los *force push* sobre `main`. Ver también [[04 Recuperar versiones]].

> [!note] Requisito previo
> Para subir un proyecto necesitas un repositorio local con al menos un commit. Ver [[02 Comandos básicos]].

---

## Conexión vía SSH

La conexión mediante claves SSH (*Secure Shell*) usa criptografía de clave pública para autenticar la terminal sin pedir credenciales en cada interacción.

### 1. Generar el par de claves en local

Abre la terminal y crea un par de claves con algoritmo Ed25519:

```bash
ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"
```

Presiona Enter para aceptar la ruta por defecto (`~/.ssh/id_ed25519`) y define una contraseña opcional.

### 2. Copiar la clave pública

Muestra el contenido del archivo `.pub` para copiarlo al portapapeles:

- **Linux / Git Bash:** `cat ~/.ssh/id_ed25519.pub`
- **Windows (PowerShell):** `Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard`

### 3. Registrar la clave en GitHub

1. Entra a tu cuenta en GitHub → **Settings** → **SSH and GPG keys**.
2. Haz clic en **New SSH key**.
3. Asigna un título descriptivo (por ejemplo, `laptop-trabajo`), pega el contenido de la clave pública y guarda.

### 4. Verificar la conexión

```bash
ssh -T git@github.com
```

Debe responder confirmando que te autenticaste correctamente (`Hi username! You've successfully authenticated...`).

### 5. Vincular y subir el repositorio local

En la raíz del proyecto local:

```bash
# 1. Asegurar la rama principal (main)
git branch -M main

# 2. Agregar el enlace remoto con la sintaxis SSH
git remote add origin git@github.com:usuario/nombre-del-repo.git

# 3. Subir el historial y fijar el upstream
git push -u origin main
```

> [!note] ¿Por qué `git branch -M main`?
> `-M` renombra (y fuerza el renombrado de) la rama actual a `main`. Se usa porque `git init` puede haber creado la rama como `master`, mientras que los repositorios nuevos de GitHub usan `main`. Si tu rama ya se llama `main`, el comando no cambia nada. Detalle en [[02 Comandos básicos]] (nota sobre `main` y `master`).

---

## Conexión vía HTTPS

El flujo sustituye las claves SSH por un **Personal Access Token (PAT)** o por el asistente integrado **Git Credential Manager (GCM)**, ya que GitHub no admite contraseñas de cuenta convencionales para operaciones de Git en terminal desde agosto de 2021.

### 1. Generar un Personal Access Token (PAT)

Si tu sistema no abre automáticamente una ventana de navegador para autenticarte vía OAuth, necesitarás un token con permisos de repositorio:

1. En GitHub, ve a tu avatar (esquina superior derecha) → **Settings**.
2. Desplázate al final de la barra lateral izquierda y entra a **Developer settings**.
3. Selecciona **Personal access tokens** → **Tokens (classic)**.
4. Haz clic en **Generate new token** → **Generate new token (classic)**.
5. Configura los parámetros:
    - **Note:** un identificador descriptivo (por ejemplo, `laptop-personal`).
    - **Expiration:** la duración (30, 60, 90 días o sin expiración, según tus políticas de seguridad).
    - **Select scopes:** marca la casilla principal **`repo`** (otorga control total sobre repositorios privados y públicos).
6. Haz clic en **Generate token** al final de la página.
7. **Copia y guarda el token de inmediato** (empieza por `ghp_...`).

> [!warning] El token se muestra una sola vez
> Por seguridad, GitHub no vuelve a mostrar la cadena una vez que cierras o recargas la pestaña. Trátalo como una contraseña: no lo subas a ningún repositorio.

### 2. Configurar el origen remoto en local

Abre la terminal en la raíz de tu proyecto local y vincula la URL HTTPS de tu repositorio:

```bash
# Si configuras el remoto por primera vez:
git remote add origin https://github.com/usuario/nombre-del-repo.git

# O si ya tenías SSH configurado y quieres cambiarlo a HTTPS:
git remote set-url origin https://github.com/usuario/nombre-del-repo.git
```

**Comprobación:** ejecuta `git remote -v`. Debe mostrar la URL iniciando con `https://github.com/...` tanto para `fetch` como para `push`.

### 3. Autenticación y primer despliegue

Envía los commits de tu rama local a GitHub:

```bash
git branch -M main
git push -u origin main
```

Según tu sistema operativo y versión de Git, ocurrirá uno de estos dos escenarios:

- **Escenario A (Git Credential Manager / ventana gráfica):** se abre un cuadro de diálogo del sistema o una pestaña del navegador con el botón **Sign in with your browser**. Autorizas el acceso y Git guarda las credenciales en el administrador seguro del sistema (Windows Credential Manager, macOS Keychain o libsecret en Linux).
- **Escenario B (terminal interactiva):** la terminal solicita las credenciales directamente:
    - `Username for 'https://github.com':` escribe tu usuario de GitHub.
    - `Password for 'https://usuario@github.com':` **pega el token `ghp_...` generado en el paso 1**. La terminal no muestra caracteres ni asteriscos mientras pegas; presiona Enter directamente.

**Comprobación del resultado:** la terminal imprime la transferencia de objetos y termina con:

```text
To https://github.com/usuario/nombre-del-repo.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main'
```

---

## SSH vs. HTTPS

| Criterio           | SSH                                                                      | HTTPS                                                                       |
| ------------------ | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| **Mecanismo**      | Criptografía asimétrica (llave pública en servidor, privada en cliente). | Tokens de acceso personal (PAT) u OAuth mediante GCM.                       |
| **Puertos de red** | Puerto 22 (algunos firewalls corporativos o redes públicas lo bloquean). | Puerto 443 (tráfico web estándar, compatible con cualquier proxy/firewall). |
| **Expiración**     | Las llaves no caducan a menos que las revoques manualmente.              | Los tokens suelen tener expiración periódica configurable.                  |

## Siguiente

Si algo sale mal después de subir cambios, revisa [[04 Recuperar versiones]]. Enlaces útiles: [[Git, GitHub y Markdown]].

← [[00 Módulo I - Índice]]
