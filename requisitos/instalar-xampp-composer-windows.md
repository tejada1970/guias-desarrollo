# 🧰 Guía: Instalación de XAMPP y Composer en Windows

Esta guía te ayudará a instalar y configurar **XAMPP** y, opcionalmente, **Composer**, en un entorno Windows para proyectos PHP.
> **💡 Nota:** Aunque XAMPP está pensado principalmente para proyectos PHP, también puedes usarlo para **proyectos estáticos con HTML, CSS y JavaScript**.

---

## ✅ 1. Instalar XAMPP

Para configurar tu entorno de desarrollo con **XAMPP** (recomendado: compatible con **PHP 8.2** o superior) sigue estos pasos:

* 1. Visita 👉 [https://www.apachefriends.org/index.html](https://www.apachefriends.org/index.html)
* 2. Descarga la versión para **Windows**.
* 3. Ejecuta el instalador.
* 4. Sigue las instrucciones del asistente. Se recomienda **mantener la carpeta de destino por defecto**: `C:\xampp`.

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

## 📦 Instalar Composer (solo si usarás frameworks PHP modernos)

**Composer** es un gestor de dependencias para proyectos PHP. Solo necesitas instalarlo si vas a trabajar con frameworks como **Laravel, Symfony** u otros que usen paquetes externos.

> ⚠️ **Nota:** Si tu proyecto es un sitio PHP básico (sin frameworks), o estás desarrollando con tecnologías como **Next.js, React** u otros frameworks JavaScript, **NO necesitas Composer**.

### Pasos para instalar Composer (si es necesario):

* Visita [https://getcomposer.org/download/](https://getcomposer.org/download/).
* Descarga el instalador para Windows (`Composer-Setup.exe`).
* Ejecuta el instalador y sigue los pasos del asistente.
* Una vez finalizado, abre la terminal o símbolo del sistema y ejecuta:

```bash
composer --version
```

* Verás la versión instalada si todo está correctamente configurado.

---

*Fin del documento*
