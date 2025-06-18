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

Asegurarte de que la extensión **ZIP** de **PHP** esté habilitada:

* Abre el Panel de Control de **XAMPP** y enciende **Apache**.
* Haz clic en "**Config**" junto a **Apache**.
* Selecciona "**PHP (php.ini)"**.
* Dentro del archivo `php.ini`, busca la línea `;extension=zip`.
* Elimina el punto y coma (;) al inicio para habilitarla.
* Guarda los cambios y cierra el archivo.
* Reinicia **Apache** para aplicar la configuración.

---

*Fin del documento*
