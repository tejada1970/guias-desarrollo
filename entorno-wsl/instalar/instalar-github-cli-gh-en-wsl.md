# 📚 Guía: instalar-github-cli-gh-en-wsl

Esta guía explica cómo instalar y usar la herramienta **GitHub CLI (`gh`)** desde **Ubuntu (WSL)**.

---

## 🎯 Propósito

Configurar la herramienta **GitHub CLI (gh)** en **WSL (Ubuntu)** para trabajar con repositorios remotos desde la terminal, sin depender de la interfaz web de GitHub.

---

## ❓ ¿Qué es GitHub CLI?

**GitHub CLI (`gh`)** es la herramienta oficial de GitHub para la terminal. Permite realizar prácticamente todas las acciones de GitHub sin necesidad de abrir el navegador.

Con ella podrás:
- 📂 Crear repositorios desde la línea de comandos.  
- 🌿 Crear ramas, hacer commits, *pull requests*, issues, etc.  
- 🚀 Automatizar flujos de trabajo y despliegues.  
- 💬 Consultar notificaciones, releases o forks directamente desde la terminal.

---

## 🧰 Instalar GitHub CLI (gh)

> ✍️ **Nota importante:** Ejecuta todos los comandos dentro de tu entorno WSL (Ubuntu), no desde PowerShell ni CMD.

### ⚙️ Pasos recomendados (instalación oficial y actualizable)

Ejecuta los siguientes comandos en orden dentro de tu terminal **Ubuntu (WSL)**:

```bash
# 1️⃣ Instalar dependencias necesarias
sudo apt install -y curl gnupg

# 2️⃣ Agregar la clave GPG oficial de GitHub CLI
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | \
sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg

# 3️⃣ Agregar el repositorio oficial de GitHub CLI
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | \
sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# 4️⃣ Actualizar repositorios e instalar GitHub CLI
sudo apt update
sudo apt install gh -y

# 5️⃣ Verificar la versión instalada
gh --version
```

🔍 **Salida esperada:** (ejemplo)

```bash
gh version 2.82.1 (2025-10-22)
https://github.com/cli/cli/releases/tag/v2.82.1
```

> ⚠️ **Nota de seguridad:**
>
> Este proceso solo afecta la instalación de GitHub CLI.
No modifica ni interfiere con otros paquetes o repositorios del sistema.
>
> Se crea un repositorio exclusivo en `/etc/apt/sources.list.d/github-cli.list` y una clave GPG específica para validar el paquete de GitHub.

### 🔄 Actualizar GitHub CLI a la última versión

Una vez instalado con este método, podrás mantenerlo actualizado con un solo comando:

```bash
sudo apt update && sudo apt upgrade gh -y
```

Esto:
- Verifica si hay nuevas versiones publicadas por GitHub.
- Descarga e instala automáticamente la más reciente.
- No requiere volver a agregar claves ni repositorios.

### 💡 Tip adicional

Si alguna vez quieres comprobar la versión más reciente disponible manualmente:

Visita 👉 https://github.com/cli/cli/releases/latest

---

## 🔐 Autenticarse en GitHub

### 1. 🌐 Preparar WSL para abrir enlaces en navegador

Antes de ejecutar `gh auth login`, asegúrate de tener las utilidades necesarias:

```bash
sudo apt install wslu xdg-utils -y
```

Esto permite a WSL abrir URLs en tu navegador de Windows cuando GitHub CLI solicita autenticación por web.

**Ejecuta el comando:**

```bash
gh auth login
```

**Durante el proceso:** (usa las flechas y presiona Enter)

Responde así:
- GitHub.com o Enterprise → Selecciona GitHub.com
- Protocolo para Git → Selecciona HTTPS
- ¿Autenticar Git con tus credenciales? → Presiona `Y`, luego `Enter`
- Método de autenticación de GitHub CLI → Selecciona Login with a web browser

Te pedirá iniciar sesión en GitHub y autorizar `gh`:

```sql
! First copy your one-time code: 9A2B-D33F
Press Enter to open https://github.com/login/device in your browser...
```

Pulsa `Enter` para abrir la web de GitHub desde WLS.

#### 🚨 Errores comunes
Si por algún motivo te aparece un error abriendo el navegador, consulta esta guía:
- 📖 [solucionar-error-openbrowser-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/errores/solucionar-error-openbrowser-en-wsl.md)

### 2. ⚙️ Pasos para autenticación

1. Copia el código de un solo uso que muestra `gh`:

```sql
! First copy your one-time code: 9A2B-D33F
```

2. Inicia sesión en GitHub.  
3. Device Activation → **Continue**  
4. Introduce el código de un solo uso → **Continue**  
5. Authorize GitHub CLI → **Authorize GitHub**  
6. Mensaje esperado: **Congratulations, you're all set!** 🎉  
7. Regresa a la terminal WSL y verifica:

```sql
! First copy your one-time code: 5F43-5665
Press Enter to open https://github.com/login/device in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
! Authentication credentials saved in plain text
✓ Logged in as tu_usuario
```

8. Verifica que todo esté correcto:

```bash
gh auth status
```

**Deberías ver algo así:**

```kotlin
github.com
  ✓ Logged in to github.com account tu_usuario (/home/tu_usuario/.config/gh/hosts.yml)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'
```

> ✍️ **Nota:** Si trabajas con varias cuentas, puedes usar `gh auth logout` y volver a iniciar sesión con otra.

---

## 🔒 Cerrar sesión en GitHub

**No es obligatorio cerrar sesión** desde la terminal una vez que terminas de usar GitHub CLI (`gh`).

El inicio de sesión se mantiene localmente en WSL mediante un token guardado en:

```arduino
~/.config/gh/hosts.yml
```

Esto significa que:
- Tu sesión **permanece activa** mientras ese token exista.
- No representa un riesgo de seguridad mientras **solo tú tengas acceso** a tu entorno WSL.
- Así, no necesitas volver a autenticarte cada vez que uses `gh` o Git con HTTPS.

Si por seguridad o limpieza prefieres cerrar sesión, puedes hacerlo fácilmente con:

```bash
gh auth logout
```

Luego elige el host (`github.com`) cuando te lo pida.

También puedes hacerlo de manera forzada (sin confirmación):

```bash
gh auth logout -h github.com --hostname github.com
```

Esto:
- Elimina el token del archivo de configuración.
- Hace que el próximo uso de `gh` te pida volver a autenticarte.

### ✅ Recomendación práctica
- **Si estás en tu propio equipo**, puedes mantener la sesión abierta sin problema.
- **Si usas un entorno compartido, público o temporal (por ejemplo, una VM o servidor ajeno), sí conviene cerrar sesión** al terminar.

---

## 📁 Crear un repositorio privado desde la terminal

Ejecutar desde tu carpeta base de proyectos, por ejemplo:

```bash
cd ~/docker-projects
gh repo create ejemplo-repo-docs --private
```

🔍 **Salida esperada:** (ejemplo)

```kotlin
✓ Created repository tu_usuario/ejemplo-repo-docs on GitHub
```

> ✍️ **Nota:** Este comando crea el repositorio remoto vacío en tu cuenta de GitHub `https://github.com/tu_usuario/ejemplo-repo-docs`, sin necesidad de abrir la web.

---

## 📥 Clonar y preparar el repositorio local

Clona el nuevo repositorio, entra en él y abrelo en **Visual Studio Code**:

```bash
cd ~/docker-projects
git clone https://github.com/tu_usuario/ejemplo-repo-docs.git
cd ejemplo-repo-docs
code .
```

---

## 📝 Crear archivos base del repositorio

Crea los archivos esenciales antes del primer commit:

```bash
touch .gitignore .gitattributes README.md LICENSE
```

> ✍️ **Nota:** Esto garantiza que defines tú mismo la estructura inicial antes de sincronizar con GitHub y evitas conflictos posteriores.

Puedes editar el `README.md` desde tu terminal **Ubuntu (WSL)**, con:

```bash
sudo nano README.md
```

O abrirlo directamente en VS Code:

```bash
code README.md
```

---

## 📁 Crear una estructura inicial de documentación

Ejemplo de estructura típica para proyectos documentados:

```bash
mkdir -p docs/guias docs/referencias docs/maestros docs/exportaciones
touch docs/introduccion.md
touch docs/guias/guia-inicio.md
touch docs/referencias/referencia-api.md
touch docs/maestros/doc-maestro.md
```

> ✍️ **Nota:** Esto es solo un ejemplo general. Ajusta la estructura a tus necesidades (guías, referencias, documentación técnica, etc.).

---

## 🚀 Primer commit y push inicial

> ⚠️ **Importante:** 
>
> Antes de realizar el primer commit y push, asegúrate de tener **Git instalado y configurado en WSL**. Consulta la guía:
>
> - 📖 [configurar-git-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-git-en-wsl.md)

Agrega todos los archivos y sube la estructura inicial a GitHub:

```bash
git init
git add .
git commit -m "Inicializar repositorio con estructura base de documentación"
git branch -M master
git push -u origin master
```

🔍 **Salida esperada:** (ejemplo)

```bash
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
To https://github.com/tu_usuario/ejemplo-repo-docs.git
 * [new branch] master -> master
```

### 📂 Tu repositorio debería tener esta estructura en GitHub:

```text
ejemplo-repo-docs/
│
├── .gitignore
├── .gitattributes
├── README.md
├── LICENSE
│
└── docs/
    ├── introduccion.md
    ├── guias/
    │   └── guia-inicio-proyecto.md
    ├── referencias/
    │   └── referencia-api.md
    ├── maestros/
    │   └── doc-maestro.md
    └── exportaciones/
```

---

## 📁 Crear repositorios para microservicios Laravel

Ejecuta todos los comandos desde tu carpeta base de proyectos, por ejemplo:

```bash
cd ~/docker-projects
```

### 1. 📁 Crear un repositorio privado desde la terminal

```bash
gh repo create my-microservices --private
```

🔍 **Salida esperada:** (ejemplo)

```bash
✓ Created repository tu_usuario/my-microservices on GitHub
```

> ✍️ **Nota:** Esto crea el repositorio remoto vacío en tu cuenta de GitHub, sin necesidad de abrir el navegador.

### 2. 📥 Clonar y preparar el repositorio local

Clona el nuevo repositorio, entra en él y abrelo en **Visual Studio Code**:

```bash
git clone https://github.com/tu_usuario/my-microservices.git
cd my-microservices
code .
```

### 3. 📝 Crear archivos base del repositorio

Crea los archivos esenciales antes del primer commit:

```bash
touch .gitignore .gitattributes README.md LICENSE
```

> ✍️ **Nota:** Esto garantiza que defines tú mismo la estructura inicial antes de sincronizar con GitHub y evitas conflictos posteriores.

Puedes editar el `README.md` desde tu terminal **Ubuntu (WSL)**, con:

```bash
sudo nano README.md
```

O abrirlo directamente en VS Code:

```bash
code README.md
```

### 📁 4. Crear estructura base del proyecto

Ejemplo de estructura para proyectos de microservicios:

```bash
mkdir -p k8s/user-service k8s/order-service k8s/gateway
touch k8s/namespace.yaml
touch k8s/databases.yaml
touch k8s/user-service/{deployment.yaml,service.yaml,configmap.yaml}
touch k8s/order-service/{deployment.yaml,service.yaml,configmap.yaml}
touch k8s/gateway/{deployment.yaml,service.yaml,configmap.yaml}
mkdir -p user-service order-service
touch user-service/Dockerfile order-service/Dockerfile
```

### 📁 5. Estructura resultante (ejemplo)

```text
my-microservices/
|
├── .gitignore
├── .gitattributes
├── README.md
├── LICENSE
|
├── k8s/
│   ├── namespace.yaml
│   ├── databases.yaml
│   ├── user-service/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── configmap.yaml
│   ├── order-service/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── configmap.yaml
│   └── gateway/
│       ├── deployment.yaml
│       ├── service.yaml
│       └── configmap.yaml
├── user-service/
│   └── Dockerfile
└── order-service/
    └── Dockerfile
```

> ✍️ **Nota:** Esto es solo un ejemplo general. Ajusta la estructura a tus necesidades.

### 🚀 6. Primer commit y push inicial

> ⚠️ **Importante:** 
>
> Antes de realizar el primer commit y push, asegúrate de tener **Git instalado y configurado en WSL**. Consulta la guía:
>
> - 📖 [configurar-git-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-git-en-wsl.md)

```bash
git init
git add .
git commit -m "Inicializar repositorio con estructura base de microservicios"
git branch -M develop
git push -u origin develop
```

🔍 **Salida esperada:** (ejemplo)

```bash
Enumerating objects: 50, done.
Counting objects: 100% (50/50), done.
To https://github.com/tu_usuario/my-microservices.git
 * [new branch] develop -> develop
```

### ✅ Resultado final

Has creado un repositorio privado con una estructura base para desplegar microservicios.

Para aprender cómo implementar esta estructura con **Laravel** + **Kubernetes**, o una similar con **Next.js** + **kubernetes**, consulta:
- 📖 [configurar-laravel-k8s-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-laravel-k8s-en-wsl.md)
- 📖 [configurar-pwa-nextjs-k8s-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-pwa-nextjs-k8s-en-wsl.md)

---

## 🌳 Visualizar la estructura de tu proyecto con `tree`

El comando `tree` permite ver la estructura de carpetas y archivos de tu proyecto de forma jerárquica, como un árbol, lo que es mucho más visual que `ls`.

🔍 **Salida típica (ejemplo):**

```text
.
├── app
├── bootstrap
├── config
├── database
├── public
├── resources
└── routes
```

Mucho más visual que `ls`, ¿verdad? 😎

🌳 Si no tienes `tree` instalado, consulta la siguiente guía: 
- 📖 [instalar-tree-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/instalar/instalar-tree-en-wsl.md)

---

## 🗑️ Eliminar repositorio en GitHub

🔐 1.  Primero, asegúrate de que estás autenticado correctamente:

```bash
gh auth status
```

- Si no lo estás, autentícate con:

```bash
gh auth login
```

🔥 2. Ejecuta el siguiente comando para eliminar tu repositorio remoto (por ejemplo):

```bash
gh repo delete tu_usuario/my-microservices
```

- El CLI te pedirá confirmación:

```text
? Are you sure you want to delete the repository tu_usuario/my-microservices? (y/N)
```

- Escribe `y` para confirmar y eliminarlo.
- Si deseas **evitar la confirmación**, añade la bandera `--yes`:

```bash
gh repo delete tu_usuario/my-microservices --yes
```

> ⚠️ Esto **solo elimina el repositorio en GitHub**, no la carpeta local en tu máquina.
>

🔥 3. Ejecuta el siguiente comando para eliminar la carpeta local (opcional), por ejemplo:

```bash
cd ~/docker-projects
rm -rf my-microservices
```

> ⚠️ Este comando **elimina definitivamente la carpeta**. Asegúrate de estar en el directorio correcto antes de ejecutarlo.
>

✅ **Listo:** tu repositorio ha sido eliminado tanto en GitHub como (opcionalmente) de tu entorno local.

---

## 🧰 Comandos útiles de GitHub CLI

| Acción                           | Comando                                         |
| -------------------------------- | ------------------------------------------------|
| Ver ayuda general                | `gh help`                                       |
| Crear un repositorio público     | `gh repo create nombre-repo --public`           |
| Crear un repositorio privado     | `gh repo create nombre-repo --private`          |
| Listar tus repositorios          | `gh repo list`                                  |
| Ver detalles de un repo          | `gh repo view nombre-repo`                      |
| Crear un issue rápido            | `gh issue create`                               |
| Ver issues abiertos              | `gh issue list`                                 |
| Crear un pull request            | `gh pr create`                                  |
| Clonar un repo por nombre        | `gh repo clone tu_usuario/nombre-repo`          |
| Verificar sesión                 | `gh auth status`                                |
| Iniciar sesión                   | `gh auth login`                                 |
| Eliminar repo remoto             | `gh repo delete usuario/repositorio`            |
| Sin confirmación al eliminar     | `gh repo delete usuario/repositorio --yes`      |

✅ Puedes usar `gh help <comando>` para obtener más información sobre cualquiera de estos comandos.

---

## ✅ Recomendaciones adicionales

| Recomendación                 | Descripción                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------|
| 🧱 Usa repositorios privados | Ideal para documentación o proyectos en desarrollo.                            |
| 🧩 Usa ramas temáticas       | Crea ramas por guía o módulo (`git checkout -b docs/pwa`).                     |
| ⚙️ Automatiza commits        | Usa `gh alias set` para crear comandos personalizados.                         |
| 🧠 Crea tokens limitados     | Si automatizas procesos, usa un token de acceso personal con permisos mínimos. |

---

## ✨ Conclusión

Con esta guía, ahora puedes desde la terminal:
- Instalar y autenticarte con **GitHub CLI**.
- Crear, gestionar y eliminar repositorios.
- Clonar repositorios en `~/docker-projects`.
- Hacer `commit` y `push` al repositorio remoto.
- Automatizar flujos de trabajo sin salir de tu entorno **WSL2**.

> ✍️ **Nota:** Puedes integrar `gh` con tus flujos de **Docker** o **Laravel** para crear repositorios y plantillas directamente desde la terminal.

---

*Fin del documento*
