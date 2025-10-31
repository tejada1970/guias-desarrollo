# 📚 Guía: configurar-git-en-wsl

Esta guía detalla los pasos para **instalar y configurar Git por primera vez en WSL (Ubuntu/Linux)**.

---

## ⚙️ Pasos para la configuración

💻 Abre tu terminal **WSL (Ubuntu)** y ejecuta los siguientes comandos:

---

### 🧰 Instalación de Git

```bash
sudo apt update
sudo apt install git -y
```

✅ Con esto Git quedará instalado en tu entorno WSL.

---

### 🧑‍ Configuración global de nombre de usuario y correo electrónico

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tucorreo@example.com"
```

> Reemplaza `"Tu Nombre"` y `"tucorreo@example.com"` con tu nombre real y tu correo asociado a GitHub.  
> Esto permitirá que tus commits tengan la identidad correcta.

---

### 🖊️ Configurar el editor por defecto (Visual Studio Code)

Si usas VS Code con **WSL Remote**, puedes configurar:

```bash
git config --global core.editor "code --wait"
```

---

### 🌈 Activar colores en la salida del terminal

```bash
git config --global color.ui true
```

Esto hace que los mensajes de Git sean más fáciles de leer.

---

### 🧱 Configuración de fin de línea (core.autocrlf)

El manejo de saltos de línea difiere entre sistemas:

- Windows usa `\r\n` (retorno de carro + salto de línea)  
- Linux/macOS/WSL usan `\n`

Para evitar problemas de compatibilidad al colaborar entre sistemas:

```bash
git config --global core.autocrlf input
```

> Esto convierte automáticamente los saltos de línea a `LF` al hacer commit, sin modificar los archivos locales de Linux.

---

## ✅ Resultado

Con esto, **Git quedará correctamente instalado y configurado en WSL**, listo para:

- Crear commits con tu identidad correcta  
- Hacer push/pull a GitHub sin problemas  
- Trabajar de manera multiplataforma con colaboradores que usen Windows o macOS

---

## 🐧 Configurar VS Code con WSL2 (opcinal pero recomendado)

Si trabajas en un entorno Linux, se recomienda conectar **Visual Studio Code (VS Code)** instalado en **Windows** con tu entorno **Linux (Ubuntu en WSL2)** usando la extensión (`Remote - WSL`), para desarrollar directamente dentro de Linux sin salir de tu editor.  

- 📖 [configurar-vscode-con-wsl2](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-vscode-con-wsl2.md)

Ideal para proyectos con **Laravel**, **Node.js**, **Docker**, y otros frameworks que funcionan mejor en entornos Linux.

---

*Fin del documento*
