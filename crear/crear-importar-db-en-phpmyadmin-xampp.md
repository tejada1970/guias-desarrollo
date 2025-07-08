# 📚 Guía: Crear/Importar Base de Datos en phpMyAdmin - XAMPP

Esta guía, explica cómo **crear una base de datos para un nuevo proyecto** o **importar una base de datos para un proyecto existente que incluya un archivo `.sql`** en phpMyAdmin.

> ✅ **Útil para cualquier proyecto web que necesite base de datos, independientemente de la tecnología** (`PHP`, `Laravel`, `Node.js`, `Next.js`, etc.).

---

## 📁 Pasos para crear una base de datos (para un nuevo proyecto)

1. Abre el **Panel de Control de XAMPP** como administrador.
2. Activa los servicios de **Apache** y **MySQL**.
3. En tu navegador, accede a: [http://localhost/phpmyadmin](http://localhost/phpmyadmin).
4. Haz clic en la pestaña **Bases de datos**.
5. Escribe un nombre para tu base de datos (por ejemplo: `mi_base_de_datos`).
6. Selecciona el cotejamiento **`utf8_general_ci`**.
7. Haz clic en **Crear**.

### ℹ️ ¿Y luego qué?

El proceso anterior **solo crea la base de datos vacía**. La creación de **tablas, relaciones, claves foráneas, índices y lógica de negocio** se explica en esta guía complementaria que te ayudará a definir correctamente la estructura interna de cualquier base de datos, sin importar la tecnología del proyecto:

- 📄 [Fases para Diseñar una Base de Datos (Tecnología Agnóstica)](https://github.com/tejada1970/guias-desarrollo/blob/master/utilidades/fases-para-disenar-una-bd.md)

---

## 📁 Pasos para importar una base de datos (si el proyecto incluye un archivo .sql)

1. Crea una nueva base de datos (**repite los pasos del apartado de arriba**).
2. Una vez creada, haz clic en el **nombre de la base de datos** desde el panel lateral izquierdo.
3. Haz clic en la pestaña **Importar** desde las opciones en la parte superior.
4. Haz clic en **"Seleccionar archivo"** y elige tu archivo `.sql` local para usar en tu proyecto. (por ejemplo: `mi_base_de_datos.sql`).
5. Pulsa **Continuar** para ejecutar la importación.

> ✅ **phpMyAdmin** ejecutará automáticamente el contenido del archivo .sql, creando todas las tablas y registros necesarios.

---

## 🔌 Verifica la conexión a la base de datos

Asegúrate que el archivo de configuración de tu proyecto (por ejemplo, `config.php`, `.env`, `database.php`, etc.) contenga los datos correctos.

### 🐘 Ejemplo común para PHP

```php
$host = 'localhost';
$db = 'mi_base_de_datos'; // debe coincidir con el nombre creado
$user = 'root';
$pass = ''; // en XAMPP el usuario root por defecto no tiene contraseña. Cambia esto sólo si tú mismo configuraste una.
```

### 🎯 Ejemplo en Laravel (.env)

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mi_base_de_datos
DB_USERNAME=root
DB_PASSWORD=
```

### ⚛️ Ejemplo en Next.js (.env.local)

Si usas **Prisma, mysql2, Drizzle ORM**, u otra librería que utilice variables de entorno para conectarse a una base de datos **MySQL**, puedes añadir lo siguiente en el archivo `.env.local`:

```env
DATABASE_URL="mysql://root:@localhost:3306/mi_base_de_datos"
```

En proyectos con **Prisma**, este valor se utiliza en `prisma/schema.prisma` así:

```prisma
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

---

> ✅ **¡Listo!** Con esta guía podrás crear, importar y conectar bases de datos en cualquier tipo de proyecto web que utilice **MySQL/MariaDB**, ya sea con **PHP simple, Laravel, Next.js (con backend)**, u otros frameworks o entornos que lo requieran.

---

*Fin del documento*
