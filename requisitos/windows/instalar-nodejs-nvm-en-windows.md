# 📚 Guía: Instalación de Node.js (NVM) en Windows

Esta guía te ayudará a instalar `Node.js` en **Windows** utilizando **NVM (Node Version Manager)**, una herramienta que permite gestionar fácilmente múltiples versiones de `Node.js` en un mismo equipo. Es especialmente útil si trabajas con distintos proyectos que requieren versiones diferentes de Node.

> ✅ **Ideal** para entornos de desarrollo modernos como `Next.js`, donde es común que cada proyecto tenga una versión específica de `Node.js` recomendada.

> ⚠️ **Importante**: No instales `Node.js` directamente desde `nodejs.org` si vas a usar **NVM**. Instalar `Node.js` de forma directa puede causar conflictos y hacer que **NVM** no funcione correctamente. Usa siempre **NVM** para instalar y cambiar versiones.

---

## 🧰 Instalar NVM

- Ve a esta página oficial: 👉 [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)
- Busca la última versión y descarga este archivo: `nvm-setup.exe`
- Ejecuta el instalador. Puedes dejar las opciones por defecto (ruta de instalación, etc.).

---

## ✅ Verifica que NVM esté instalado
- Abre una terminal (PowerShell o Git Bash) y escribe:

```bash
nvm version
```

- Deberías ver la versión de NVM instalada, por ejemplo:

```plaintext
1.1.12
```

---

## 🧰 Instalar una versión específica de Node.js

- Por ejemplo, para Next.js 15 necesitas Node.js `20.13.1`:

```bash
nvm install 20.13.1
```

- Y si también necesitas una versión distinta para otro proyecto, por ejemplo `18.17.0`:

```bash
nvm install 18.17.0
```

---

## ✅ Cambiar entre versiones según el proyecto

- Cuando vayas a trabajar en un proyecto, activa la versión que necesites.

Ejemplos:

```bash
nvm use 20.13.1
```

```bash
nvm use 18.17.0
```

- Verifica la versión activa con:

```bash
node -v
```

---

## ✅ Ver versiones instaladas

- Ejecuta el siguiente comando para listar todas las versiones que tienes instaladas actualmente:

```bash
nvm list
```

- Te mostrará algo así:

```plaintext
* 20.13.1 (default)
18.17.0
```

- El asterisco `*` indica cuál está activa.

---

*Fin del documento*