# 📚 Guía: instalar-nodejs-nvm-en-windows

Esta guía te ayudará a instalar `Node.js` en **Windows** utilizando **NVM (Node Version Manager)**, una herramienta que permite gestionar fácilmente múltiples versiones de `Node.js` en un mismo equipo. Es especialmente útil si trabajas con distintos proyectos que requieren versiones diferentes de Node.

> ✅ **Ideal** para entornos de desarrollo modernos como `Next.js`, donde es común que cada proyecto tenga una versión específica de `Node.js` recomendada.

> ⚠️ **Importante**: No instales `Node.js` directamente desde `nodejs.org` si vas a usar **NVM**. Instalar `Node.js` de forma directa puede causar conflictos y hacer que **NVM** no funcione correctamente. Usa siempre **NVM** para instalar y cambiar versiones.

---

## 🧰 Instalar NVM

1. Ve a esta página oficial: 👉 [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases).
2. Busca la última versión, accede a **Assets** y descarga este archivo: `nvm-setup.exe`.
3. Ejecuta el instalador. Puedes dejar las opciones por defecto (ruta de instalación, etc.).

---

## ✅ Verifica que NVM esté instalado

Abre una terminal (PowerShell o Git Bash) y escribe:

```bash
nvm version
```

Deberías ver la versión de **NVM** instalada, por ejemplo:

```plaintext
1.1.12
```

👉 También puedes ejecutar:

```bash
where nvm
```

Para confirmar que la ruta está en el **PATH** del sistema.

---

## 🧰 Instalar una versión específica de Node.js

Por ejemplo, para Next.js 15 necesitas Node.js `20.13.1`:

```bash
nvm install 20.13.1
```

👉 Si necesitas una versión distinta para otro proyecto, por ejemplo `18.17.0`:

```bash
nvm install 18.17.0
```

> ⚠️ Si tienes problemas con una versión muy reciente, prueba instalar una versión LTS (Long Term Support).

---

## ✅ Cambiar entre versiones según el proyecto

Cuando vayas a trabajar en un proyecto, activa la versión que necesites.

Ejemplos:

```bash
nvm use 20.13.1
```

```bash
nvm use 18.17.0
```

👉 Verifica la versión activa con:

```bash
node -v
```

---

## ✅ Ver versiones instaladas

Ejecuta el siguiente comando para listar todas las versiones que tienes instaladas actualmente:

```bash
nvm list
```

Te mostrará algo así:

```plaintext
* 20.13.1 (Currently using 64-bit executable)
18.17.0
```

El asterisco `*` indica cuál está activa.

---

> ✅ Con esto ya tienes **NVM** instalado y podrás gestionar varias versiones de Node.js fácilmente.

---

*Fin del documento*