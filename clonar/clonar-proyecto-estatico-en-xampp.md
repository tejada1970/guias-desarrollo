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

Si el proyecto incluye un archivo `.sql` (por ejemplo: `small_pets.sql`) o con cualquier otro nombre, sigue estos pasos para crear y cargar la base de datos en **phpMyAdmin**:

#### Accede a phpMyAdmin

* Abre el Panel de **XAMPP** como administrador.

* Enciende **Apache y MySQL**.

* En tu navegador, ve a 👉 `http://localhost/phpmyadmin`

#### Crea una nueva base de datos

* Haz clic en la pestaña **"Bases de datos"**.

* Escribe un nombre (por ejemplo: `small_pets`) que coincida con el usado en el código del proyecto.

* Selecciona `utf8_general_ci` como cotejamiento.

* Haz clic en **"Crear"**.

#### Importa el archivo .sql

* Una vez creada, haz clic en el nombre de la base de datos desde el panel lateral.

* Pulsa la pestaña **"Importar"** desde las opciones en la parte superior.

* Haz clic en **"Seleccionar archivo"** y elige el archivo `.sql` proporcionado con el proyecto (por ejemplo: `small_pets.sql`).

* Pulsa en **"Continuar"**.

> ✅ **phpMyAdmin** ejecutará automáticamente el contenido del archivo `.sql`, creando todas las tablas y registros necesarios.

#### Verifica la conexión a la base de datos

Asegúrate de que el archivo de conexión del proyecto (por ejemplo: `conexion.php`, `config.php`, `.env.php` o el que proceda) tenga los siguientes datos correctamente definidos de forma similar a este ejemplo:

```
$host = 'localhost';
$db = 'small_pets'; // este debe coincidir con el nombre creado para la base de datos
$user = 'root';
$pass = '';
```

> ⚠️ En **XAMPP**, por defecto el **usuario root** no tiene contraseña. No es necesario modificar nada salvo que lo hayas cambiado manualmente.

Con esto tu proyecto debería estar correctamente conectado a la base de datos y listo para usarse desde `http://localhost/nombre_del_proyecto`.

---

*Fin del documento*
