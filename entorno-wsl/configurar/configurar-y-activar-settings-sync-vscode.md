# 📚 Guía: configurar-y-activar-settings-sync-vscode

Esta guía explica cómo configurar y activar **Settings Sync** en **Visual Studio Code (VS Code)** para realizar **backup y sincronización de tus configuraciones, extensiones y preferencias**, incluyendo su funcionamiento con **WSL (Windows Subsystem for Linux)**.

---

## ❓ ¿Qué es Settings Sync?

**Settings Sync** (sincronización de configuración) es una función de VS Code que guarda en la nube —vinculada a tu cuenta de Microsoft o GitHub— tus:

- Configuraciones (`settings.json`)  
- Teclas personalizadas  
- Fragmentos de código (snippets)  
- Extensiones instaladas  
- Temas, iconos, y más  

Esto permite **restaurar tu entorno en otro equipo o tras reinstalar VS Code**, manteniendo tus preferencias y extensiones exactamente iguales.

---

## ☁️ Activar Settings Sync (backup opcional y recomendado)

1. En VS Code, haz clic en el icono de usuario → **Turn On Settings Sync...**  
2. Marca ✅ "Extensions" y ✅ "Settings".  
3. Inicia sesión con tu cuenta de **Microsoft** o **GitHub**.

> ✍️ **Nota:** No necesitas estar conectado todo el tiempo para trabajar con VS Code en tu WSL. La sesión solo se utiliza para **guardar y sincronizar tu configuración en la nube**.

---

## 🤔 ¿Cómo funciona Settings Sync con WSL?

Cuando trabajas con VS Code y WSL, existen **dos entornos de extensiones separados**:

| Entorno          | Dónde corre VS Code | Dónde se instalan extensiones      | Descripción                                           |
|------------------|---------------------|------------------------------------|-------------------------------------------------------|
| 🪟 Windows      | En tu PC            | `%USERPROFILE%\.vscode\extensions` | Extensiones locales del editor.                       |
| 🐧 WSL (Ubuntu) | Dentro de Ubuntu    | `~/.vscode-server/extensions`      | Extensiones que se ejecutan dentro del entorno Linux. |

- ✅ Settings Sync sincroniza la lista de extensiones y la configuración entre ambos entornos.
- 🚫 No copia automáticamente las extensiones de Windows a WSL, porque algunas deben ejecutarse dentro de Linux (PHP, Docker, ESLint…). Pero mantiene tu entorno sincronizado y te ofrecerá instalarlas cuando entres a un entorno remoto.

---

## 🧩 Uso práctico en WSL

1. Abre un proyecto en WSL.  
2. VS Code compara las extensiones instaladas en Windows y las de WSL.  
3. Si faltan extensiones en WSL, aparecerá una notificación:

  - > "La extensión 'Prettier' está instalada localmente. ¿Deseas instalarla en WSL: Ubuntu?"

4. Al aceptar, VS Code instalará la extensión solo dentro del entorno WSL.

---

## ✅ Resumen de acciones

| Acción                  | Qué hace                                                   |
|-------------------------|------------------------------------------------------------|
| Activar Settings Sync   | Sincroniza preferencias, lista de extensiones, temas, etc. |
| Abrir proyecto en WSL   | Detecta qué extensiones faltan en WSL.                     |
| Aceptar las sugerencias | Instala las extensiones necesarias dentro de WSL.          |

---

## ✍️ Nota importante

- La cuenta de **Microsoft/GitHub** solo se necesita para **backup y sincronización**, no para trabajar con WSL.  
- Las extensiones ya instaladas en **WSL** funcionan **offline** sin conexión ni login a tú cuenta.  
- La sincronización es **opcional pero recomendada** para mantener tu entorno consistente entre PCs o tener un respaldo de tus configuraciones y extensiones.

✅ Con esto, tu entorno **VS Code + WSL** estará respaldado, sincronizado y listo para desarrollo con **Docker, Laravel, Node.js** y cualquier otra tecnología.

---

## 🛠️ Consejos y buenas prácticas

- 📖 [consejo-para-gestionar-extensiones-en-vscode](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/consejos/consejo-para-gestionar-extensiones-en-vscode.md)

---

*Fin del documento*
