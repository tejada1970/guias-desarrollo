# 📚 Guía: Crear un proyecto estático desde cero

Esta guía te ayudará a crear un proyecto estático desde cero. Está pensada para ser reutilizada en distintos tipos de tecnologías estáticas como: **HTML, CSS, JavaScript, PHP** (sin uso de frameworks ni de base de datos).

La estructura básica del proyecto será la misma. Solo cambiará el archivo principal (por ejemplo: `index.html` o `index.php`) según la tecnología usada.

> ✅ Antes de continuar, asegúrate de tener instalados y configurados los requisitos necesarios.

---

## ⚙️ Requisitos previos

Para instalar y configurar un entorno óptimo de desarrollo en **Windows**, consulta las siguientes guías del índice principal:

- 📁 [Índice de Guías - Requisitos/Windows](https://github.com/tejada1970/guias-desarrollo#windows)

---

## 🛠 Consejos y buenas prácticas

> ✅ Si estás pensando en conservar el proyecto, te recomiendo consultar esta guía:

- 📄 [Consejo para organizar tus proyectos en XAMPP](https://github.com/tejada1970/guias-desarrollo/blob/master/consejos/consejo-para-organizar-tus-proyectos-en-xampp.md)

---

## ✅ Pasos para crear el proyecto

Inicia el panel de **XAMPP** como administrador y enciende **Apache**.

> 🔹 **Reemplaza donde corresponda:** `mi_proyecto` por el nombre real que quieras ponerle al proyecto.

1. Abre la terminal **`Git Bash`** y navega a la carpeta donde quieras guardar el proyecto, por ejemplo:

```bash
cd C:/xampp/htdocs
```

2. Crea una carpeta para tu proyecto, por ejemplo:

```bash
mkdir mi_proyecto
```

> 📄 Esta carpeta representará cualquier proyecto que estés desarrollando, ya sea con **HTML, JS o PHP**.

3. Accede al proyecto:

```bash
cd mi_proyecto
```

4. Abre el proyecto en **VS Code**:

```bash
code .
```

---

## 📂 Estructura del proyecto

La estructura base del proyecto será la siguiente, con solo un cambio según el tipo de tecnología usada:

🌐 Proyecto HTML o JavaScript

```pgsql
mi_proyecto/
│
├── index.html
├── style.css
└── script.js
```

🐘 Proyecto PHP

```pgsql
mi_proyecto/
│
├── index.php
├── style.css
└── script.js
```

> 📄 En ambos casos, `style.css` contiene los estilos y `script.js` los scripts JavaScript. Ahora puedes escribir un código mínimo para comprobar que tu proyecto se visualiza y funciona correctamente.

---

## 🔧 Código mínimo de prueba

HTML – `index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi Proyecto</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Hola Mundo</h1>
  <script src="script.js"></script>
</body>
</html>

PHP – `index.php`

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi Proyecto PHP</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1><?php echo "Hola desde PHP"; ?></h1>
  <script src="script.js"></script>
</body>
</html>
```

CSS – `style.css`

```css
body {
  background-color: #f0f0f0;
  font-family: Arial, sans-serif;
}
h1 {
    color: red;
}
```

JavaScript – `script.js`

```js
console.log("El script funciona correctamente.");
```

---

## 🌍 Ver el proyecto

### Desde Visual Studio Code

- Abre la terminal integrada en **VS Code** usando (`Ctrl + ñ`).

- Haz clic en **Go Live** si tienes instalada la extensión **Live Server** (recomendado solo para proyectos estáticos sin PHP).

> ⚠️ **Importante:** La extensión **Live Server** no interpreta archivos PHP. Si el proyecto incluye código PHP, **no uses Go Live**. En su lugar, accede a **`http://localhost/mi_proyecto`** desde el navegador para que **XAMPP** lo procese correctamente.

---

## ✅ Recomendación:

Esta guía es reutilizable para cualquier proyecto estático. Solo debes asegurarte de:

- Cambiar el archivo principal (por ejemplo: `index.html` por `index.php`).

- Mantener la estructura organizada.

- Asegurarte de que el servidor **Apache** esté corriendo en **XAMPP** para los archivos **PHP**.

---

*Fin del documento*