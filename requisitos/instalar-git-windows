# 🧰 Guía: Instalación y Configuración de Git en Windows

**Git** es una herramienta esencial para el control de versiones en proyectos de desarrollo. Esta guía, detalla los pasos para la instalación y configuración inicial en Windows.

---

## 🔽 Descargar e Instalar Git

* Visita 👉 [https://git-scm.com/](https://git-scm.com/)
* Descarga la versión más reciente para **Windows**.
* Ejecuta el instalador.
* Durante la instalación, puedes aceptar las opciones por defecto del asistente.

---

## ⚙️ Configurar Git por primera vez

Abre la terminal **Git Bash** (búscalo en el menú de inicio) y ejecuta las siguientes configuraciones:

### 🧑‍ Configuración global de nombre de usuario y correo electrónico

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tucorreo@example.com"
```

### 🖊️ Configurar el editor por defecto (Visual Studio Code)

```bash
git config --global core.editor "code --wait"
```

### 🌈 Activar colores en la salida del terminal

```bash
git config --global color.ui true
```

### 🧱 Configuración de fin de línea (`core.autocrlf`)

El manejo de saltos de línea puede variar entre sistemas operativos:

* En **Windows**, se usan `\r\n` (retorno de carro y salto de línea).
* En **Linux/macOS**, solo se usa `\n`.

Para evitar problemas de compatibilidad al clonar, subir o colaborar en proyectos entre sistemas diferentes, ajusta la conversión automática de saltos de línea:

#### En **Windows**:

```bash
git config --global core.autocrlf true
```

#### En **Linux/macOS**:

```bash
git config --global core.autocrlf input
```

---

### 💡 Resultado:

Con esto, Git quedará correctamente instalado y configurado para trabajar en cualquier entorno de desarrollo multiplataforma.

---

*Fin del documento*
