# 📚 Guía: Importar Base de Datos en phpMyAdmin - XAMPP

Esta guía explica cómo crear una base de datos e importar un archivo `.sql` en phpMyAdmin, útil para cualquier proyecto web que necesite base de datos, independientemente de la tecnología (PHP, Laravel, Node.js, etc.).

---

## ✅ Pasos para importar la base de datos

### 1. Accede a phpMyAdmin

- Abre el Panel de **XAMPP** como administrador.
- Enciende los servicios de **Apache** y **MySQL**.
- En tu navegador, navega a: `http://localhost/phpmyadmin`

### 2. Crea una nueva base de datos

- Haz clic en la pestaña **Bases de datos**.
- Escribe un nombre para la base de datos (ejemplo: `mi_base_de_datos`) que coincida con el usado en el proyecto.
- Selecciona el cotejamiento `utf8_general_ci`.
- Haz clic en **Crear**.

### 3. Importa el archivo `.sql`

- Una vez creada, haz clic en el nombre de la base de datos desde el panel lateral.
- Pulsa la pestaña **"Importar"** desde las opciones en la parte superior.
- Haz clic en **"Seleccionar archivo"** y elige tu archivo `.sql` local para usar en tu proyecto. (por ejemplo: `mi_base_de_datos.sql`).
- Pulsa en **"Continuar"** para ejecutar la importación.

> ✅ **phpMyAdmin** ejecutará automáticamente el contenido del archivo `.sql`, creando todas las tablas y registros necesarios. 

### 4. Verifica la conexión a la base de datos

Asegúrate que el archivo de configuración de tu proyecto (por ejemplo, `config.php`, `.env`, `database.php`, etc.) contenga los datos correctos.

- Ejemplo común para PHP

```php
$host = 'localhost';
$db = 'mi_base_de_datos'; // debe coincidir con el nombre creado
$user = 'root';
$pass = ''; // en XAMPP el usuario root por defecto no tiene contraseña
```

> ⚠️ **Nota:** En XAMPP, por defecto el usuario `root` no tiene contraseña. Cambia esto sólo si tú mismo configuraste una.

- Ejemplo en Laravel (.env)

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mi_base_de_datos
DB_USERNAME=root
DB_PASSWORD=
```

---

✅ ¡Listo! con esta guía podrás importar bases de datos para cualquier proyecto que lo necesite, desde PHP simple hasta frameworks como Laravel, Next.js (con backend), o cualquier otro que use MySQL/MariaDB.

---

*Fin del documento*
