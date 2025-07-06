# 📚 Guía: Configurar archivo `php.ini` en XAMPP

Esta guía, te ayudará a habilitar extensiones necesarias (como `zip` o `gd`) y realizar otras configuraciones en el archivo `php.ini`.

---

## ⚙️ Accede al archivo de configuración `php.ini` en XAMPP

* Abre el Panel de Control de **XAMPP** como administrador y enciende **Apache**.
* Haz clic en "**Config**" junto a **Apache**.
* Selecciona "**PHP (php.ini)"**.
* Una vez dentro del archivo, puedes modificar la configuración según tus necesidades.

---

## 🗜️ Habilita la extensión ZIP de PHP

La **extensión ZIP de PHP** permite a los scripts PHP **leer, crear, extraer y manipular archivos** `.zip`, que son archivos comprimidos muy comunes. Es decir, esta extensión proporciona una forma integrada en PHP de trabajar con archivos comprimidos sin necesitar herramientas externas.

Asegurarte de que la **extensión ZIP de PHP** esté habilitada:

* Accede al archivo de configuración `php.ini`.
* Dentro del archivo `php.ini`, busca la línea: `;extension=zip`.
* Elimina el punto y coma (;) al inicio para habilitarla.
* Guarda los cambios, cierra el archivo, reinicia **Apache** para aplicar la configuración.

---

## 🖼️ Habilita la extensión GD

Si tu proyecto utiliza imágenes (subidas, redimensionado, miniaturas, etc.), puede ser necesario habilitar la extensión **GD**:

* Accede al archivo de configuración `php.ini`.
* Dentro del archivo `php.ini`, busca la línea: `;extension=gd`.
* Elimina el punto y coma (;) al inicio para habilitarla.
* Guarda los cambios, cierra el archivo, reinicia **Apache** para aplicar la configuración.

> ⚠️ **Nota:** Aunque tu proyecto actual no dependa directamente de **GD**, es muy común en proyectos PHP **(como blogs en Laravel)**. Activarla puede evitar errores futuros si se trabaja con imágenes.

---

*Fin del documento*