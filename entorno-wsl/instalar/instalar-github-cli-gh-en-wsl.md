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

---

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

**Ejecuta el comando:**

```bash
gh auth login
```

**Durante el proceso:**

- Te preguntará GitHub.com o Enterprise → selecciona GitHub.com.
- Pregunta cómo deseas autenticarte → selecciona Web browser.
- Se abrirá tu navegador pidiéndote iniciar sesión en GitHub y autorizar gh.
- Una vez autorizado, la terminal mostrará algo como:

```pgsql
Logged in to GitHub as <tu_usuario>
```

**Verificar autenticación:**

```bash
gh auth status
```

**Deberías ver:**

```kotlin
github.com
  ✓ Logged in as tu_usuario
  ✓ Git operations for this host enabled
```

> ✍️ **Nota:** Si trabajas con varias cuentas, puedes usar gh auth logout y volver a iniciar sesión con otra.

---

## 📁 Crear un repositorio privado desde la terminal

Ejecutar desde tu carpeta base de proyectos, por ejemplo:

```bash
cd ~/docker-projects
gh repo create ejemplo-repo-docs --private --confirm
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

Agrega todos los archivos y sube la estructura inicial a GitHub:

```bash
git add .
git commit -m "Inicializar repositorio con estructura base de documentación"
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

> 💡 Ubicación recomendada:
> 
> Ejecuta todos los comandos desde tu carpeta base de proyectos, por ejemplo:
>
> ```bash
> cd ~/docker-projects
> ```

### 📁 Crear un repositorio privado desde la terminal

```bash
gh repo create my-microservices --private --confirm
```

🔍 **Salida esperada:** (ejemplo)

```bash
✓ Created repository tu_usuario/my-microservices on GitHub
```

> ✍️ **Nota:** Esto crea el repositorio remoto vacío en tu cuenta de GitHub, sin necesidad de abrir el navegador.

### 📥 Clonar y preparar el repositorio local

Clona el nuevo repositorio, entra en él y abrelo en **Visual Studio Code**:

```bash
git clone https://github.com/tu_usuario/my-microservices.git
cd my-microservices
code .
```

### 📝 Crear archivos base del repositorio

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

### 📁 3. Crear estructura base del proyecto

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

### 📁 4. Estructura resultante (ejemplo)

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

### 🚀 5. Primer commit y push inicial

```bash
git add .
git commit -m "Inicializar repositorio con estructura base de microservicios"
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

Si no tienes `tree` instalado, consulta la siguiente guía: 
- 📖 [instalar-tree-en-wsl]((https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/instalar/instalar-tree-en-wsl.md))

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

---

## ✅ Recomendaciones adicionales

| Recomendación                 | Descripción                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------|
| 🧱 Usa repositorios privados | Ideal para documentación o proyectos en desarrollo.                            |
| 🧩 Usa ramas temáticas       | Crea ramas por guía o módulo (`git checkout -b docs/pwa`).                     |
| ⚙️ Automatiza commits        | Usa `gh alias set` para crear comandos personalizados.                         |
| 🧠 Crea tokens limitados     | Si automatizas procesos, usa un token de acceso personal con permisos mínimos. |

---

## 🧰 Comandos útiles de GitHub CLI

| Acción                    | Comando                                |
| ------------------------- | -------------------------------------- |
| Ver ayuda general         | `gh help`                              |
| Crear un repositorio      | `gh repo create`                       |
| Listar tus repositorios   | `gh repo list`                         |
| Ver detalles de un repo   | `gh repo view nombre-repo`             |
| Crear un issue rápido     | `gh issue create`                      |
| Ver issues abiertos       | `gh issue list`                        |
| Crear un pull request     | `gh pr create`                         |
| Clonar un repo por nombre | `gh repo clone tu_usuario/nombre-repo` |

---

## ✨ Conclusión

Con esta guía, ahora puedes:
- Instalar y autenticarte con **GitHub CLI**.
- Crear y gestionar repositorios desde la terminal.
- Clonar repositorios en `~/docker-projects`.
- Hacer `commit` y `push` al repositorio remoto.
- Automatizar flujos de trabajo sin salir de tu entorno **WSL2**.

> ✍️ **Nota:** Puedes integrar `gh` con tus flujos de **Docker** o **Laravel** para crear repositorios y plantillas directamente desde la terminal.

---

*Fin del documento*
