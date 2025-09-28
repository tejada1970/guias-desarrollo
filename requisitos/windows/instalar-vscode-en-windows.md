# 📚 Guía: Instalación de Visual Studio Code en Windows

**Visual Studio Code** (VS Code) es un editor de código ligero, potente y altamente extensible, ideal para proyectos en múltiples lenguajes y tecnologías como PHP, JavaScript, Laravel, Docker, entre otros.

---

## 🧰 Instalar Visual Studio Code

1. Visita 👉 [https://code.visualstudio.com/](https://code.visualstudio.com/).
2. Descarga la versión para **Windows**.
3. Ejecuta el instalador y sigue los pasos del asistente.
4. Se recomienda aceptar las opciones predeterminadas durante la instalación.
5. ⚠️ **Importante**: Asegúrate de marcar la opción **"Agregar al PATH"** y **"Registrar como editor predeterminado"** si aparecen durante el proceso.

---

## ✅ Verificar instalación

Abre la terminal integrada con `Ctrl + ñ` y ejecuta:

```bash
code --version
```

Deberías ver la versión instalada.

---

## ⚙️ Configurar `Git Bash` como terminal predeterminada en Visual Studio Code (opcional pero recomendado)

Para evitar errores comunes al usar **PowerShell**, se recomienda configurar **`Git Bash`** como la terminal predeterminada en **Visual Studio Code (VS Code)**.

- 📄 [Configurar Git Bash en VSCode (recomendado)](https://github.com/tejada1970/guias-desarrollo/blob/master/configuraciones/configurar-git-bash-en-vscode.md)

---

## 🧩 Extensiones Recomendadas

Las extensiones enriquecen la experiencia de desarrollo. A continuación se presentan las más recomendadas:

### 🔧 Generales

- **Spanish Language Pack for Visual Studio Code** – Microsoft  
  Traduce la interfaz de VS Code al español.

- **Prettier – Code Formatter** – Prettier  
  Formateador universal de código para JS, CSS, HTML, etc.

- **Live Server** – Ritwick Dey  
  Lanza un servidor local para ver cambios en tiempo real en HTML/CSS/JS.

- **Auto Rename Tag** – Jun Han  
  Cambia simultáneamente las etiquetas de apertura y cierre en archivos HTML, JSX, etc.

---

### 🌐 HTML / CSS

- **VSCode W3C Web Validator** – IBM
  Valida archivos HTML y CSS directamente en el editor, asegurando el cumplimiento de los estándares del W3C.

---

### 🧵 CSS, Tailwind y Alpine.js

- **Tailwind CSS IntelliSense** – Tailwind Labs  
  Autocompletado para clases Tailwind.

- **Alpine.js IntelliSense** – Adrian Wilczyński  
  Autocompletado y documentación para Alpine.js.

---

### 📦 JavaScript / TypeScript

- **ESLint** – Microsoft  
  Linter para JavaScript/TypeScript que ayuda a mantener un código limpio y consistente.

- **Pretty TypeScript Errors** – yoavbls  
  Mejora la visualización de errores de compilación en TypeScript.

- **ES7+ React/Redux/React-Native/JS Snippets** – dsznajder  
  Snippets modernos para JavaScript, React, Redux y otras tecnologías. Incluye funciones de ES6+ y versiones posteriores.

---

### 🐘 Desarrollo PHP / Laravel

- **Laravel Blade Formatter** – Shuhei Hayashibara  
  Formatea archivos `.blade.php`.

- **Laravel Blade Snippets** – Winnie Lin  
  Snippets útiles para Blade.

- **Laravel Goto View** – codingyu  
  Navegación entre controladores y vistas Blade.

- **Laravel Snippets** – Winnie Lin  
  Snippets para funciones y estructuras comunes de Laravel.

- **PHP Intelephense** – Ben Mewburn  
  IntelliSense avanzado para PHP.

---

### 🗄️ Bases de Datos (si usas microservicios y distintas BD)

- **Database Client** – Database Client
Conexiones y consultas a PostgreSQL y MySQL directamente desde VS Code.

- **MongoDB for VS Code** – MongoDB
Herramientas para conectarte, explorar y administrar bases de datos MongoDB.

#### 🔧 Configuración de extensiones en VS Code para bases de datos

Las extensiones de VS Code como "Database Client" (para PostgreSQL/MySQL) o "MongoDB for VS Code" (para MongoDB) facilitan el trabajo con tus bases de datos desde el editor.

Una vez instaladas, deberás crear una conexión. Para ello te recomiendo consultar este tutorial:

- 📄 [Probar Conexiones a BD](https://youtu.be/ekM3S2DX19k?list=PLlerKZbEcUVR6lPYQcFb77CsJVPZpWyFK)

---

### 🐳 Contenedores, WSL y DevOps

- **Dev Containers** – Microsoft  
  Trabaja con entornos aislados usando contenedores de desarrollo.

- **WSL** – Microsoft  
  Soporte para integrar proyectos con Windows Subsystem for Linux.

- **Docker** – Microsoft  
  Control y manejo de contenedores Docker.

- **Docker DX** – Docker  
  Interfaz visual mejorada para manejo de contenedores.

---

### 📄 Lectura de Documentación

- **vscode-pdf** – tomoki1207
  Permite abrir y visualizar archivos PDF directamente en Visual Studio Code. Ideal para revisar manuales, guías u hojas de especificación sin salir del editor.

- **Markdown PDF** – yzane
  Convierte archivos Markdown a PDF (y otros formatos como HTML o PNG) de forma sencilla, manteniendo el formato y facilitando la exportación de documentación.

  💡 **Ejemplo para convertir archivos Markdown a PDF**
  1. Abre tu archivo `.md`.
  2. Haz clic derecho en el contenido del archivo y selecciona la opción **Markdown PDF: Export (pdf)** en el menú contextual.
  3. La extensión generará un PDF con todo tu contenido (incluyendo código, diagramas y emojis) en la raíz del proyecto.

---

### 🤖 Inteligencia Artificial (opcional)

- **GitHub Copilot** – GitHub  
  Asistente de código impulsado por IA (requiere cuenta GitHub Copilot).

---

*Fin del documento*
