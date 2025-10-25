# 📚 Guía: Clonar proyecto Next.js en XAMPP

Esta guía te ayudará a clonar un proyecto **Next.js** y ejecutarlo localmente, utilizando **XAMPP** únicamente para el servicio de base de datos **MySQL/MariaDB** (si el proyecto lo requiere).

> ✅ Antes de continuar, asegúrate de tener instalados y configurados los requisitos necesarios.

---

## ⚙️ Requisitos previos

Para instalar y configurar un entorno óptimo de desarrollo en **Windows**, consulta:
- 📂 [Windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/README.md#-instalar)

---

### 🗄️ Crear/Importar base de datos en phpMyAdmin - XAMPP (si aplica)

Si el proyecto incluye un archivo `.sql`, consulta esta guía para importar la base de datos en **phpMyAdmin**:

- 📄 [Crear/Importar Base de Datos en phpMyAdmin - XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/crear/crear-importar-db-en-phpmyadmin-xampp.md)

---

## 🛠 Consejos y buenas prácticas

> ✅ Si estás pensando en conservar el proyecto, te recomiendo consultar estas guías:

- 📄 [Consejo antes de clonar](https://github.com/tejada1970/guias-desarrollo/blob/master/consejos/entorno-windows/consejo-antes-de-clonar.md)
- 📄 [Consejo para organizar tus proyectos en XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/consejos/entorno-windows/consejo-para-organizar-tus-proyectos-en-xampp.md)

---

## 📥 Pasos para clonar el proyecto

Inicia el panel de **XAMPP** como administrador y enciende **Apache** (y **MySQL** si el proyecto usa base de datos).

> 🔹 **Reemplaza donde corresponda:** la **URL** de ejemplo **`https://github.com/usuario/repo.git`** por la **URL** real del repositorio, y `nombre_del_proyecto` por el nombre real de la carpeta generada al clonar.

---

### 🔧 Clonar con Git Bash

Abre la terminal **`Git Bash`** y ejecuta de uno en uno los siguientes comandos para guardar, clonar, acceder y abrir el proyecto en **Visual Studio Code**:

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
code .
```

---

### 🚀 Ejecutar el proyecto Next.js

Abre la terminal integrada en **VS Code** usando (`Ctrl + ñ`):

1. Instala las dependencias:

```bash
npm install
```

2. Inicia el servidor de desarrollo:

```bash
npm run dev
```

3. Abre el navegador y accede a: **`http://localhost:3000`**

---

*Fin del documento*