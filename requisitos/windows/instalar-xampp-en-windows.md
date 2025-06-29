# 📚 Guía: Instalación de XAMPP en Windows

Esta guía te ayudará a instalar y configurar **XAMPP**, en un entorno **Windows**.

---

## 🧰 Instalar XAMPP

Para configurar tu entorno de desarrollo con **XAMPP**:

* Visita 👉 [https://www.apachefriends.org/index.html](https://www.apachefriends.org/index.html)
* Descarga la versión para **Windows**.
* Ejecuta el instalador.
* Sigue las instrucciones del asistente. Se recomienda **mantener la carpeta de destino por defecto**: `C:\xampp`.

---

## ⚙️ Habilitación de la Extensión ZIP de PHP

La **extensión ZIP de PHP** permite a los scripts PHP **leer, crear, extraer y manipular archivos** `.zip`, que son archivos comprimidos muy comunes. Es decir, esta extensión proporciona una forma integrada en PHP de trabajar con archivos comprimidos sin necesitar herramientas externas.

Asegurarte de que la **extensión ZIP de PHP** esté habilitada:

* Abre el Panel de Control de **XAMPP** y enciende **Apache**.
* Haz clic en "**Config**" junto a **Apache**.
* Selecciona "**PHP (php.ini)"**.
* Dentro del archivo `php.ini`, busca la línea `;extension=zip`.
* Elimina el punto y coma (;) al inicio para habilitarla.
* Guarda los cambios y cierra el archivo.
* Reinicia **Apache** para aplicar la configuración.

---

## 🖼️ Extensión GD (opcional pero recomendada)

Si tu proyecto utiliza imágenes (subidas, redimensionado, miniaturas, etc.), puede ser necesario habilitar la extensión **GD**:

* En el archivo `php.ini`, busca esta línea: `;extension=gd`.
* Elimina el punto y coma (;) al inicio para habilitarla.
* Guarda los cambios y reinicia Apache.

> ⚠️ Nota: Aunque tu proyecto actual no dependa directamente de **GD**, es muy común en proyectos PHP (como blogs en Laravel). Activarla puede evitar errores futuros si se reusa parte del código o si se trabaja con imágenes.

---

*Fin del documento*
