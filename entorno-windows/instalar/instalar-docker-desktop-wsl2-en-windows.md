# 📚 Guía: instalar-docker-desktop-wsl2-en-windows

Esta guía te ayudará a instalar **Docker Desktop** en Windows 11 usando **WSL2**.  

🔹 **¿Qué es Docker y por qué lo necesitamos?**  
Docker permite crear y ejecutar aplicaciones dentro de contenedores.  
Un contenedor es como una mini-computadora con todo lo que necesita tu aplicación (PHP, MySQL, Node, etc.).  

Gracias a Docker:  
- No necesitas instalar MySQL, PHP, Redis, etc. directamente en Windows.  
- Todo vive dentro de contenedores aislados, fáciles de borrar o reiniciar.  
- En Windows 11, Docker Desktop usa WSL2 como motor, por eso es el segundo requisito después de instalar Ubuntu con WSL2.

---

## ⚙️ Pasos para la instalación

### 🧰 Instalar Docker Desktop

1. Ve a la página oficial 👉 [Docker Desktop para Windows](https://www.docker.com/products/docker-desktop/)  
2. Descarga el instalador para Windows 11 (x86_64 o ARM64 según tu PC):

   - 🤔 ¿Cómo saber si tu equipo es x86_64 o ARM64?

   - Abre PowerShell y ejecuta:  

    ```powershell
    $env:PROCESSOR_ARCHITECTURE
    ```

   - 👉 Lo más común es AMD64 (la mayoría de PCs Windows 11).  

3. Ejecuta el archivo descargado.
4. Durante la instalación:  
   - Asegúrate de que está marcada la opción **Use WSL 2**.  
   - Haz clic en **Next** y termina la instalación.  
   - Reinicia tu PC si lo pide.
5. Finalizada la instalación, haz clic en **Close and log out** (para reiniciar Windows).
6. Después de reiniciar, continuará el proceso mostrando una ventana en la que debes aceptar el acuerdo de licencia.
7. A continuación, selecciona si Docker es para **"Work"** o **"Personal"**:
    - Si es para uso personal, elige **"Personal"**.
    - Si es para trabajo o empresa, selecciona **"Work"**.
    - Ambas opciones requieren iniciar sesión con una cuenta de Docker.

---
  
### 💻 Cómo crear una cuenta de Docker correctamente

1. Si inicias sesión con **Google**, Docker te pedirá que configures un nombre de usuario.
2. Elegir un buen nombre de usuario:
    - Debe ser único (si el nombre ya está en uso, te pedirá otro).
    - Puede contener letras, números y guiones bajos (_).
    - No uses espacios ni caracteres especiales.
    - Ejemplos válidos:
      - `miusuario123`
      - `juan_dev`
      - `dockerfan2024`
3. Si el nombre que intentas ya está tomado, prueba variaciones hasta encontrar uno disponible.

---

### ⚙️ Pasos finales

1. Docker te pedirá acceso a una app, una vez le permitas, te mostrará dos pasos para escoger una opción en cada uno.
2. Finalmente, te mostrará la interfaz del panel de Docker.

---

## 💡 Tip

Aunque puedas usar Docker Desktop sin iniciar sesión para cosas básicas, la integración con WSL y ciertas funciones avanzadas funcionan mejor cuando estás logueado.

Esto también puede ayudar a que desaparezcan errores de arranque y problemas de terminal negra en Ubuntu.

---

## ✅ Recomendaciones

**Desde Docker Desktop/Settings/General:**

- Desactiva "Start Docker Desktop when you sign in to your computer" para evitar errores de arranque, y activa "Open Docker Dashboard when Docker starts".

- Si quieres arranque automático, añade un retraso de 15–30s usando el "Programador de tareas" de Windows.

- Choose container terminal -> Integrated

**Desde Docker Desktop/Settings/Software updates:**

- Desactiva la casilla "Automatically check for updates" y marca las casillas "Always downdolad updates" y "Automatically update components" para tener tu **Docker Desktop** siempre actualizado y al día.

**Desde Docker Desktop/Settings/Resources/WSL Integration**:

- Asegurate de tener activada la casilla "Enable integration with my default WSL distro". Esto garantiza que Docker solo se integre con tu distro predeterminada y evita conflictos.

- Siempre que hagas cambios en la integración WSL, cierra y vuelve a abrir Ubuntu.

---

## 💡 Probar Docker

⚠️ **Importante:** Antes de probar Docker desde **Ubuntu en WSL**, asegúrate de tener instalado el cliente de Docker (`docker-cli`) dentro de tu distribución WSL.

**Consulta la guía:**
- 📖 [instalar-docker-cli-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/instalar/instalar-docker-cli-en-wsl.md)

**Pasos para probar Docker:**

1. Abre **WSL (Ubuntu)** o una terminal de tu preferencia (Git Bash, PowerShell, CMD). 

2. Ejecuta:  

```bash
docker --version
```

3. Deberías ver algo como:  

```
Docker version 27.0.2, build 123abc
```

4. Mostrar información de Docker:

```bash
docker info
```

5. Prueba ejecutando un contenedor:

```bash
docker run hello-world
```

   - Esto descargará una imagen pequeña y mostrará un mensaje de éxito:

   - **Hello from Docker!**
   - **This message shows that your installation appears to be working correctly.**

   - ✅ Deberías ver que Docker se conecta correctamente al daemon de Windows.

6. Opcional: listar contenedores e imágenes

```bash
docker ps -a
docker images
```

---

### 🚨 Errores comunes
- 📖 [solucionar-error-catastrofico-en-terminal-wsl2](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/errores/solucionar-error-catastrofico-en-terminal-wsl2.md)

---

*Fin del documento*