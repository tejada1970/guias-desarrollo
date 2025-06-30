# 📚 Guía: Clonar proyecto Next.js en XAMPP

Esta guía te ayudará a clonar un proyecto **Next.js** y ejecutarlo localmente, utilizando **XAMPP** únicamente para el servicio de base de datos **MySQL/MariaDB** (si el proyecto lo requiere).

> ✅ Antes de continuar, asegúrate de tener instalados y configurados los requisitos necesarios.

---

## ⚙️ Requisitos previos

Para instalar y configurar un entorno óptimo de desarrollo en **Windows**, consulta las siguientes guías del índice principal:

- 📁 [Índice de Guías - Requisitos/Windows](https://github.com/tejada1970/guias-desarrollo#windows)

### 🧱 Requisitos mínimos para Next.js
- Node.js y npm
- Git
- Visual Studio Code
- XAMPP (solo si se usa MySQL)

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

### 🔧 Clonar con Git Bash

Abre la terminal **Git Bash** y navega a la carpeta `htdocs` para guardar el proyecto. Escribe al final `code .` para abrir el proyecto en **Visual Studio Code**:

```bash
cd C:/xampp/htdocs
git clone https://github.com/usuario/repo.git
cd nombre_del_proyecto
code .
```

> 💡 Puedes clonar fuera de `htdocs` si no necesitas usar **Apache**. Solo usa `htdocs` si quieres tener todo junto y organizado o si el proyecto también tiene partes en **PHP**.

---

### 🚀 Ejecutar el proyecto Next.js

1. Instala las dependencias:

```bash
npm install
```

2. Inicia el servidor de desarrollo:

```bash
npm run dev
```

3. Abre el navegador y accede a:

```arduino
http://localhost:3000
```

---

### 🗄️ Importar base de datos en phpMyAdmin (si aplica)

Si el proyecto incluye un archivo `.sql`, consulta esta guía para importar la base de datos en **phpMyAdmin**:

- 📄 [Importar Base de Datos en phpMyAdmin - XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/utilidades/importar-db-en-phpmyadmin-xampp.md)

---

*Fin del documento*