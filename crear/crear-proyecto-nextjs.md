# 📚 Guía: Crear proyecto Next.js

Esta guía te ayudará a crear un nuevo proyecto con Next.js desde cero.

> ✅ Antes de continuar, asegúrate de tener instalados y configurados los requisitos necesarios.

---

## ⚙️ Requisitos previos

Para instalar y configurar un entorno óptimo de desarrollo en **Windows**, consulta las siguientes guías del índice principal:

- 📁 [Índice de Guías - Requisitos/Windows](https://github.com/tejada1970/guias-desarrollo#windows)

---

## 🚀 Crear un nuevo proyecto con la última versión de Next.js

- Abre la terminal Git Bash y navega a la carpeta donde quieras crear el proyecto, por ejemplo:

```bash
cd C:/xampp/htdocs
```

- Crea un nuevo proyecto con `create-next-app@latest`:

```bash
npx create-next-app@latest ejemplo-i18n
```

- Durante la configuración:

    - Presiona **Enter** en todas las opciones para aceptar la configuración recomendada e instalar todas las dependencias: **TypeScript**, **ESLint**, **Tailwind CSS**, **src**, **App Router**, **Turbopack** y **import alias**

    - Cuando te pregunte si deseas personalizar el **import alias** responde **Yes** y luego presiona **Enter** para aceptar la sugerencia por defecto **@/**

- Accede a la carpeta del proyecto:

```bash
cd ejemplo-i18n
```

- Instala next-intl:

```bash
npm install next-intl
```

- Abre el proyecto con VS Code:

```bash
code .
```

- > ✅ De esta forma, te aseguras de que todas las dependencias estén correctamente instaladas antes de abrir el editor de código.

- Ejecuta el proyecto:

```bash
npm run dev
```

Abre tu navegador en [http://localhost:3000](http://localhost:3000) para comprobar que Next.js funciona y se visualiza correctamente.

> 💡 Recuerda instalar la versión **NVM** correspondiente para Next.js v15 o superior. Puedes consultar la guía:

- 📄 [Instalar Node.js (NVM) en Windows](https://github.com/tejada1970/guias-desarrollo/blob/master/requisitos/windows/instalar-nodejs-nvm-en-windows.md)

---

*Fin del documento*
