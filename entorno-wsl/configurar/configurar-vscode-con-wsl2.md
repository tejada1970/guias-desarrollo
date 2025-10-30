# 📚 Guía: configurar-vscode-con-wsl2

Esta guía explica cómo conectar **Visual Studio Code (VS Code)** instalado en **Windows** con tu entorno **Linux (Ubuntu en WSL2)**, para desarrollar directamente dentro de Linux sin salir de tu editor.  

Ideal para proyectos con **Laravel**, **Node.js**, **Docker**, **PHP**, y otros frameworks que funcionan mejor en entornos Linux.  

---

## ⚙️ 1. Requisitos previos

Antes de comenzar, asegúrate de tener instalado y configurado lo siguiente:

- ✅ **Visual Studio Code** en Windows.  
  - 📖 [instalar-vscode-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-vscode-en-windows.md)
  > ✍️ **Contenido de esta guía:** instalación de VSCode, extensiones recomendadas, WSL2, respaldo (backup) y terminal predeterminada.

- ✅ **WSL2** habilitado y **Ubuntu** instalado.  
  - 📖 [configurar-linux-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/configurar/configurar-linux-wsl2-en-windows.md)

- ✅ Extensión **"WSL"** de Microsoft instalada en VS Code.  

---

## 🧰 2. Instalar la extensión "WSL" en VS Code

1. Abre **VS Code** en Windows.  
2. Ve a la pestaña de **Extensiones** (icono de cuadraditos a la izquierda o `Ctrl + Shift + X`).  
3. Busca **"WSL"** y selecciona la extensión oficial de Microsoft.  
4. Instálala.  

🔹 Esta extensión permite a **VS Code** conectarse y trabajar directamente con el entorno **Linux de tu WSL2**.

---

## 🧱 3. Abrir un proyecto de WSL en VS Code

**Opcional:** crea una carpeta, por ejemplo `docker-projects`, para mantener organizados tus proyectos dentro de Ubuntu (WSL).

1. Abre tu terminal de Ubuntu (WSL):  
   ```bash
   cd ~/docker-projects/ejemplo-proyecto
   ```
2. Luego ejecuta:
   ```bash
   code .
   ```
3. Esto abrirá **Visual Studio Code en modo remoto (WSL)**, VS Code detectará automáticamente que estás dentro de Linux y mostrará algo como:

   ```
   Updating VS Code Server to version 03c265b1adee71ac88f833e065f7bb956b60550a
   Removing previous installation...
   Installing VS Code Server for Linux x64 (03c265b1adee71ac88f833e065f7bb956b60550a)
   Downloading: 100%
   Unpacking: 100%
   Unpacked 2265 files and folders to /home/usuario/.vscode-server/bin/03c265b1adee71ac88f833e065f7bb956b60550a.
   Looking for compatibility check script at /home/usuario/.vscode-server/bin/03c265b1adee71ac88f833e065f7bb956b60550a/bin/helpers/check-requirements.sh
   Running compatibility check script
   Compatibility check successful (0)
   ```

---

## 🧰 4. Instalación automática del VS Code Server

La primera vez que uses `code .` dentro de WSL, VS Code instalará un componente interno llamado **VS Code Server**.  

📦 Este servidor se instala en tu entorno Linux en la ruta:
```bash
~/.vscode-server/
```

### ❓ ¿Para qué sirve?
- Permite que VS Code (en Windows) ejecute procesos, tareas, IntelliSense, terminales y depuración directamente dentro de tu Linux (WSL).  
- No modifica tu proyecto ni tus repositorios.  
- Solo se instala **una vez** (o cuando VS Code se actualiza).

---

## ✅ 6. Verificar instalación del VS Code Server

**Puedes comprobar que el servidor está instalado ejecutando en tu terminal de Ubuntu:**

```bash
ls ~/.vscode-server/
```

**Deberías ver algo similar a:**
```kotlin
bin  data  extensions
```

- **bin/** → contiene las versiones del servidor de VS Code.  
- **data/** → guarda configuraciones y logs internos.  
- **extensions/** → contiene las extensiones instaladas dentro del entorno WSL.

**Puedes listar las extensiones instaladas dentro de WSL con:**

```bash
code --list-extensions
```

- Ejemplo de salida:

   ```
   bmewburn.vscode-intelephense-client-1.14.4
   bradlc.vscode-tailwindcss-0.14.28
   esbenp.prettier-vscode-11.0.0
   ms-azuretools.vscode-docker-2.0.0
   ```

- Cada carpeta tiene el formato `autor.extension-versión`.

**Puedes ver más detalles con:**

```bash
ls -lt ~/.vscode-server/extensions
```

**Y si necesitas eliminar manualmente una extensión (no recomendado salvo que sepas lo que haces):**

```bash
rm -rf ~/.vscode-server/extensions/nombre.extension
```

> ⚠️ **Importante:** Lo más seguro es desinstalarla desde **VS Code → Extensiones → botón de desinstalar**.

---

## 🔄 7. Sincronización de extensiones entre Windows y WSL

Cuando trabajas con VS Code y WSL, existen **dos entornos de extensiones separados**:

| Entorno          | Dónde corre VS Code | Dónde se instalan extensiones      | Descripción                                           |
|------------------|---------------------|------------------------------------|-------------------------------------------------------|
| 🪟 Windows      | En tu PC            | `%USERPROFILE%\.vscode\extensions` | Extensiones locales del editor.                       |
| 🐧 WSL (Ubuntu) | Dentro de Ubuntu    | `~/.vscode-server/extensions`      | Extensiones que se ejecutan dentro del entorno Linux. |

### 🤔 ¿Por qué tengo menos extensiones en WSL?

- No todas las extensiones se instalan automáticamente dentro de Ubuntu.  
- VS Code suele mostrar una notificación preguntando si deseas instalar también las extensiones locales en WSL, pero si cerraste o ignoraste esa notificación, ya no vuelve a aparecer.

### 🧰 Instalar extensiones manualmente en WSL (VS Code)

1. Abre un proyecto dentro de WSL (verás `WSL: Ubuntu` en la esquina inferior izquierda).
2. Abre la paleta de comandos (`Ctrl + Shift + P` o `F1`).
3. Escribe: `Remote: Show Installed Extensions`.
4. Verás dos listas:  
   - **Local – Installed on Windows**  
   - **WSL: Ubuntu – Installed in WSL**
5. En cada extensión faltante, haz clic en ⚙️ → **“Install in WSL: Ubuntu”**.

### 💻 Alternativa por terminal

1. **Listar extensiones instaladas dentro de WSL:**

```bash
code --list-extensions
```

2. **Instalar una extensión manualmente en WSL:**

```bash
code --install-extension nombre.extension
```

- Ejemplo:

```bash
code --install-extension ms-azuretools.vscode-docker
```

---

## ☁️ Activar sincronización automática (Settings Sync)

**backup opcional y recomendado.**

Esta guía explica cómo configurar y activar **Settings Sync** en VS Code para realizar **backup y sincronización de tus configuraciones, extensiones y preferencias**, incluyendo su funcionamiento con **WSL (Windows Subsystem for Linux)**.

- 📖 [configurar-y-activar-settings-sync-vscode](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-y-activar-settings-sync-vscode.md)

---

## 🧩 8. Problemas comunes

| ⚠️ Problema                                                         | 💡 Solución                                                                                         |
|----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| VS Code muestra "Reinstalando VS Code Server" cada vez que abres WSL | Es normal tras una actualización de VS Code. Se reinstala automáticamente.                          |
| "No se puede abrir carpeta en WSL"                                   | Verifica que la extensión **WSL** esté habilitada.                                                  |
| El proyecto abre en Windows en lugar de Ubuntu                       | Asegúrate de ejecutar `code .` **dentro de la terminal de Ubuntu**, no desde PowerShell o Git Bash. |
| Lentitud al acceder a archivos                                       | No trabajes desde rutas montadas como `/mnt/c/`, usa rutas nativas de Linux (`/home/usuario/`).     |

---

## 🧠 9. Conceptos clave

| Concepto                   | Descripción                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| **VS Code (Windows)**      | La interfaz principal que ves en pantalla.                                  |
| **VS Code Server (Linux)** | Componente que se ejecuta dentro de WSL2 y procesa tus archivos y comandos. |
| **Extensión WSL**          | El puente que conecta ambos entornos.                                       |
| **`code .`**               | Comando que abre la carpeta actual en VS Code desde Linux.                  |

---

## ✅ Resumen

Con esta configuración, ya puedes:

- Ejecutar `code .` desde tu terminal de Ubuntu.  
- Usar todas las extensiones y funcionalidades de VS Code directamente en Linux.  
- Integrar herramientas como **Docker**, **Composer**, **Node.js**, y **PHP** sin conflictos entre Windows y Linux.  

✅ **Resultado:** un entorno de desarrollo híbrido, rápido y 100 % compatible con entornos de producción Linux.

---

## 🛠️ Consejos y buenas prácticas

- 📖 [consejo-para-gestionar-extensiones-en-vscode](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/consejos/consejo-para-gestionar-extensiones-en-vscode.md)

- 📖 [consejo-para-trabajar-con-vscode-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/consejos/consejo-para-trabajar-con-vscode-wsl.md)

---

## 🔗 Recursos adicionales

- 🔗 [Documentación oficial de Remote - WSL (VS Code)](https://code.visualstudio.com/docs/remote/wsl)  

---

*Fin del documento*
