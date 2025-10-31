# 📚 Guía: solucionar-error-openbrowser-en-wsl

Esta guía te ayudará a solucionar el error que aparece al intentar autenticarte con **GitHub CLI (`gh`)** desde **WSL (Ubuntu)**, cuando el comando intenta abrir el navegador automáticamente y falla.

---

## ❓ ¿Qué significa este error?

Al ejecutar:

```bash
gh auth login
```

y elegir el método de autenticación por navegador (**Login with a web browser**), puede aparecer el siguiente mensaje de error:

```sql
! Failed opening a web browser at https://github.com/login/device
  exec: "xdg-open,x-www-browser,www-browser,wslview": executable file not found in $PATH
  Please try entering the URL in your browser manually
```

Esto significa que GitHub CLI no puede abrir el navegador automáticamente desde WSL, porque no encuentra las utilidades necesarias (`xdg-open` o `wslview`) para hacerlo.

### 🤔 ¿Por qué sucede?

Por defecto, WSL no tiene un entorno gráfico (no hay navegador instalado dentro de Linux).
Cuando `gh` intenta abrir la página de autenticación en tu navegador, busca alguno de los comandos:

```bash
xdg-open
x-www-browser
www-browser
wslview
```

Si ninguno está disponible en `$PATH`, se produce el error anterior.

---

## ✅ Solución rápida

Instala las utilidades necesarias:

```bash
sudo apt install -y wslu xdg-utils
```

### 🤔 ¿Qué hacen?

| Paquete       | Función                                                                               |
|---------------|---------------------------------------------------------------------------------------|
| **wslu**      | Añade el comando `wslview`, permite abrir enlaces web en tu navegador de Windows.     |
| **xdg-utils** | Añade `xdg-open`, usado por muchos programas (como `gh`) para abrir URLs por defecto. |

---

## ⚙️ Reautenticación con `gh`

Una vez instaladas las utilidades:

1. Ejecuta nuevamente:

```bash
gh auth login
```

2. Responde así durante el asistente:

| Pregunta                                            | Respuesta                | Descripción                                  |
|-----------------------------------------------------|--------------------------|----------------------------------------------|
| Where do you use GitHub?                            | GitHub.com               | Conecta con la plataforma principal.         |
| What is your preferred protocol for Git operations? | HTTPS                    | Recomendado, más fácil y seguro.             |
| Authenticate Git with your GitHub credentials?      | Y (sí)                   | Permite usar las mismas credenciales en Git. |
| How would you like to authenticate GitHub CLI?      | Login with a web browser | Usa tu navegador de Windows.                 |

El asistente te mostrará algo como:

```sql
! First copy your one-time code: 9A2B-D33F
Press Enter to open https://github.com/login/device in your browser...
```

✅ Ahora sí, al pulsar Enter, se abrirá tu navegador correctamente.

### ⚙️ Pasos para autenticación

1. Copia el código de un solo uso que muestra `gh`:

```sql
! First copy your one-time code: 9A2B-D33F
```

2. Inicia sesión en GitHub.  
3. Device Activation → **Continue**  
4. Introduce el código de un solo uso → **Continue**  
5. Authorize GitHub CLI → **Authorize GitHub**  
6. Mensaje esperado: **Congratulations, you're all set!** 🎉  
7. Regresa a la terminal WSL y verifica:

```sql
! First copy your one-time code: 5F43-5665
Press Enter to open https://github.com/login/device in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
! Authentication credentials saved in plain text
✓ Logged in as tu_usuario
```

8. Verifica que todo esté correcto:

```bash
gh auth status
```

🔍 **Salida esperada:**

```kotlin
github.com
  ✓ Logged in to github.com account tu_usuario (/home/tu_usuario/.config/gh/hosts.yml)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'
```

---

## 🧭 Si no se abre automáticamente

1. Copia el código que muestra `gh`, por ejemplo: `9A2B-D33F`.  
2. Abre manualmente tu navegador y entra en: [https://github.com/login/device](https://github.com/login/device)  
3. Repite los pasos de autenticación (del 2 al 8).

---

> 💡 Tip: Mantén el navegador actualizado y permite pop-ups de GitHub si es necesario.

---

*Fin del documento*
