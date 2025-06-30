# 📚 Guía: Clonar proyecto estático en XAMPP

Esta guía te ayudará a clonar un proyecto web estático y ejecutarlo localmente con **XAMPP**, usando tecnologías como **HTML**, **CSS*, **JS** y **PHP** (sin uso de frameworks), con o sin base de datos.

> ✅ Antes de continuar, asegúrate de tener instalados y configurados los requisitos necesarios.

---

## ⚙️ Requisitos previos

Para instalar y configurar un entorno óptimo de desarrollo en **Windows**, consulta las siguientes guías del índice principal:

- 📁 [Índice de Guías - Requisitos/Windows](https://github.com/tejada1970/guias-desarrollo#windows)

---

## 🛠 Consejos y buenas prácticas

> ✅ Si estás pensando en conservar el proyecto, te recomiendo consultar estas guías:

- 📄 [Consejo antes de clonar](https://github.com/tejada1970/guias-desarrollo/blob/master/consejos/consejo-antes-de-clonar.md)
- 📄 [Consejo para organizar tus proyectos en XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/consejos/consejo-para-organizar-tus-proyectos-en-xampp.md)

---

## 📥 Pasos para clonar el proyecto

Inicia el panel de **XAMPP** como administrador y enciende **Apache** (y **MySQL** si el proyecto usa base de datos).

> 🔹 **Reemplaza donde corresponda:** `https://github.com/usuario/repo.git` por el enlace real del repositorio, y `nombre_del_proyecto` por el nombre real de la carpeta generada al clonar.

---

### 🔧 Desde Git Bash

1. Abre la terminal **Git Bash** y navega a la carpeta `htdocs`:

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
```

2. Abre tu navegador y escribe en la barra de direcciones **`http://localhost/nombre_del_proyecto`** para ver el sitio.

---

### 🔧 Desde Visual Studio Code

1. Abre la terminal **Git Bash** y navega a la carpeta `htdocs`:

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
code .
```

2. Visualiza el sitio web:

* Abre la terminal integrada en **VS Code** usando (`Ctrl + ñ`).
* Haz clic en **Go Live** si tienes instalada la extensión **Live Server** (recomendado solo para proyectos estáticos sin PHP).

> ⚠️ **Importante:** La extensión **Live Server** no interpreta archivos PHP. Si el proyecto incluye código PHP, **no uses Go Live**. En su lugar, accede a *`http://localhost/nombre_del_proyecto`* desde el navegador para que **XAMPP** lo procese correctamente.

---

### 🗄️ Importar base de datos en phpMyAdmin

Si el proyecto incluye un archivo `.sql`, consulta la siguiente guía para crear y cargar la base de datos en **phpMyAdmin**:

- 📄 [Importar Base de Datos en phpMyAdmin - XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/utilidades/importar-db-en-phpmyadmin-xampp.md)

---

*Fin del documento*
