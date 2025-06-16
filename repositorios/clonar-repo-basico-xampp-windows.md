# 📥 Guía: Clonar repositorio básico en XAMPP (Windows)

Esta guía te ayudará a clonar un repositorio de un proyecto web estático **(HTML/CSS/JS) o (PHP)** y ejecutarlo localmente usando **XAMPP**.

> ✅ Asegúrate de tener instalados y configurados los requisitos previos indicados en el repositorio (por ejemplo, XAMPP, Git, Visual Studio Code).

---

## 🚀 Pasos para clonar el proyecto

Inicia el panel de **XAMPP** y enciende **Apache** (y **MySQL** si el proyecto usa base de datos).

### 🔧 Desde Git Bash

1. Abre la terminal **Git Bash** y navega a la carpeta `htdocs`:

> 🔹 Reemplaza `https://github.com/usuario/repo.git` por el enlace real del repositorio, y `nombre_del_proyecto` por el nombre real de la carpeta generada al clonar.

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
```

2. Abre tu navegador y escribe en la barra de direcciones: **`http://localhost/nombre_del_proyecto`** para ver el sitio.

> 🔹 Reemplaza `nombre_del_proyecto` por el nombre exacto de la carpeta clonada.

---

### 🔧 Desde Visual Studio Code

1. Abre la terminal **Git Bash** y navega a la carpeta `htdocs`:

> 🔹 Reemplaza `https://github.com/usuario/repo.git` por el enlace real del repositorio, y `nombre_del_proyecto` por el nombre real de la carpeta generada al clonar.

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
code .
```

2. Visualiza el sitio web:

* Haz clic en **"Go Live"** si tienes instalada la extensión **Live Server** (recomendado)
* O abre tu navegador y escribe en la barra de direcciones: **`http://localhost/nombre_del_proyecto`** para ver el sitio.

> 🔹 Reemplaza `nombre_del_proyecto` por el nombre exacto de la carpeta clonada.

---

*Fin documento*
