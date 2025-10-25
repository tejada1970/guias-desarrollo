# 📚 Guía: Configurar archivo `php.ini` en XAMPP

Esta guía, te ayudará a habilitar extensiones necesarias (como `zip`) u otras extensiones (como `gd`, `pgsql`, `pdo_pgsql` o `mongodb`).

---

## ⚙️ Accede al archivo de configuración `php.ini` en XAMPP

Puedes hacerlo de dos maneras:

1. Desde el explorador de archivos: `C:/xampp/php/php.ini` (puedes abrir el archivo con el Bloc de notas o tu editor preferido).
2. Desde el Panel de Control de **XAMPP** (ejecutado como administrador): enciende **Apache**, haz clic en "**Config**" junto a **Apache**, y selecciona "**PHP (php.ini)**".

> 🔹 **Nota:** Recuerda guardar los cambios después de modificar el archivo y reiniciar **Apache** para que la nueva configuración tenga efecto (para reiniciar Apache haz click en **Stop** y luego en **Start**).

---

## 🗜️ Habilitar la extensión ZIP

La **extensión ZIP de PHP** permite a los scripts PHP **leer, crear, extraer y manipular archivos `.zip`**, que son archivos comprimidos muy comunes. Es decir, esta extensión proporciona una forma integrada en PHP de trabajar con archivos comprimidos sin necesitar herramientas externas.

Asegurarte de que la **extensión ZIP de PHP** esté habilitada: 

1. Abre el archivo `php.ini`.  
2. Busca la línea:  
   ```ini
   ;extension=zip
   ```  
3. Elimina el `;` al inicio para habilitarla:  
   ```ini
   extension=zip
   ```  
4. Guarda los cambios y reinicia **Apache**.  
5. Abre la consola CMD o PowerShell y verifica con:  
   ```bash
   php -m | findstr zip
   ```
   ✅ Debe mostrar:  
   ```
   zip
   ```

---

## 🖼️ Habilitar la extensión GD

Si tu proyecto utiliza imágenes (subidas, redimensionado, miniaturas, etc.), puede ser necesario habilitar la extensión **GD**:

1. Abre el archivo `php.ini`.  
2. Busca la línea:  
   ```ini
   ;extension=gd
   ```  
3. Elimina el `;` al inicio para habilitarla:   
   ```ini
   extension=gd
   ```  
4. Guarda los cambios y reinicia **Apache**.  
5. Abre la consola CMD o PowerShell y verifica con:  
   ```bash
   php -m | findstr gd
   ```
   ✅ Debe mostrar:  
   ```
   gd
   ```

---

## 🗄️ Habilitar PostgreSQL (`pgsql` y `pdo_pgsql`)

Si piensas trabajar con bases de datos PostgreSQL, necesitas habilitar las extensiones correspondientes.

🔹 Nota: Si usas VS Code y quieres gestionar PostgreSQL o MySQL visualmente, puedes instalar la extensión "Database Client" de (Database Client). Esto es opcional y no sustituye la habilitación de extensiones en `php.ini`.

1. Abre el archivo `php.ini`.  
2. Busca las líneas:  
   ```ini
   ;extension=pgsql
   ;extension=pdo_pgsql
   ```  
3. Elimina el `;` al inicio en ambas para habilitarlas:  
   ```ini
   extension=pgsql
   extension=pdo_pgsql
   ```  
4. Guarda los cambios y reinicia **Apache**.  
5. Abre la consola CMD o PowerShell y verifica con:  
   ```bash
   php -m | findstr pgsql
   ```
   ✅ Debe mostrar:  
   ```
   pdo_pgsql
   pgsql
   ```

---

## 🍃 Habilitar MongoDB

XAMPP incluye MySQL/MariaDB por defecto, pero no trae soporte para **MongoDB**. Para usarlo en Laravel/PHP necesitas instalar manualmente la extensión.

> 🔹 Nota: Para usar MongoDB en Laravel/PHP, además de habilitar la extensión, necesitas instalar con Composer alguno de estos paquetes: `jenssegers/mongodb` → integración con Eloquent o `mongodb/mongodb` → cliente oficial para PHP para trabajar con colecciones (Recomendado para microservicios).

> 🔹 Nota: Si usas VS Code, puedes instalar la extensión oficial "MongoDB for VS Code" de (MongoDB) para explorar tus bases de datos desde el editor (opcional).

### 1. Verifica tu versión de PHP

En CMD o PowerShell:  
```bash
cd C:\xampp\php
php -v
```
👉 Apunta estos datos:  
- Versión de PHP (ej. 8.2.12 → se usa "8.2").  
- Thread safety (`ZTS` o `NTS`).  
- Arquitectura (`x64` o `x86`).

### 2. Descarga el driver de MongoDB

- Ve a la página oficial: [PECL MongoDB builds](https://downloads.php.net/~windows/pecl/releases/mongodb/1.17.0/?utm_source=chatgpt.com).  
- Te llevará a la página: Index of /~windows/pecl/releases/mongodb/1.17.0
- Descarga el `.zip` correspondiente a tu versión. Si tienes por ejemplo PHP 8.2, 64 bits, Thread Safe (ZTS), buscas algo como: `php_mongodb-1.17.0-8.2-ts-vs16-x64.zip`.
- Si fuese NTS, bajas el que diga nts.

### 3. Copia el `.dll`

- Descomprime el `.zip`.
- Copia el archivo `php_mongodb.dll` en la carpeta de extensiones de PHP en XAMPP:  
  ```
  C:\xampp\php\ext
  ```

### 4. Edita el archivo `php.ini`

Abre `C:\xampp\php\php.ini` con un editor de texto (puedes abrirlo con el block de notas).

Busca la sección de extensiones (;extension=...).
;;;;;;;;;;;;;;;;;;;;;;
; Dynamic Extensions ;
;;;;;;;;;;;;;;;;;;;;;;

Agrega esta línea, por ejemplo después de `extension=zip` o al final de esa lista:  
```ini
extension=mongodb
```
Guarda los cambios y reinicia **Apache**. 

### 5. Verifica la instalación

En CMD o PowerShell:  
```bash
php -m | findstr mongodb
```  
✅ Debe mostrar:  
```
mongodb
```

---

> 🔹 Nota: En Linux/Mac, sí puedes usar: `pecl install mongodb` y ya te instala el driver.

---

### 💡 Tip

Las extensiones de VS Code como "Database Client" (para PostgreSQL/MySQL) o "MongoDB for VS Code" (para MongoDB) facilitan el trabajo con tus bases de datos desde el editor.

Una vez instaladas, deberás crear una conexión. Para ello te recomiendo consultar este tutorial sobre la configuración de extensiones en VS Code para bases de datos:

- 📄 [Probar Conexiones a BD](https://youtu.be/ekM3S2DX19k?list=PLlerKZbEcUVR6lPYQcFb77CsJVPZpWyFK)

---

*Fin del documento*
