# 📚 Guía: consejo-para-gestionar-extensiones-en-vscode

Esta guía ofrece buenas prácticas para **optimizar el rendimiento y la productividad** en Visual Studio Code mediante una gestión inteligente de las extensiones para trabajar optimamente con múltiples lenguajes o proyectos distintos (por ejemplo: PHP, React, Python, Docker, etc.).

---

## 🛠️ Consejos y buenas prácticas

### ⚙️ Contexto

**Visual Studio Code** es multilenguaje por diseño: cada lenguaje o tecnología tiene sus propias extensiones.

Con el tiempo, puedes acumular muchas extensiones activas simultáneamente, lo que a menudo genera:
  - ⏳ Lentitud al iniciar VS Code  
  - 🧩 Conflictos entre extensiones  
  - 💾 Mayor consumo de memoria  

---

### ⚙️ Estrategias recomendadas

#### 🔧 Opción 1: Desactivar extensiones por tipo de archivo o proyecto

A veces, no necesitas tener todas las extensiones activas en todos tus proyectos.
Puedes desactivar extensiones específicas solo en el proyecto actual sin afectar a los demás.

📘 **Cómo hacerlo:**
1. Abre la **paleta de comandos** con:
   - **`Ctrl + Shift + P`**
2. Escribe:  
   - **`Extensions: Disable (Workspace)`**
3. Selecciona la extensión que quieras desactivar (por ejemplo, Python o PHP Intelephense).

🔍 **Qué ocurre:**
VS Code desactiva esa extensión **solo dentro del proyecto actual (workspace)**.
Cuando abras otro proyecto, la extensión volverá a estar disponible.

##### 💡 Ejemplo práctico

Supón que tienes tres proyectos en tu entorno local:

```text
C:\xampp\htdocs\laravel-api
C:\xampp\htdocs\frontend-react
C:\xampp\htdocs\python-scripts
```

Y tienes instaladas estas extensiones globales:
- PHP Intelephense
- ESLint
- Python
- Docker

🔹 Cuando trabajes en `frontend-react`, puedes desactivar:
- PHP Intelephense
- Python

🔹 Cuando trabajes en `laravel-api`, puedes desactivar:
- ESLint
- Python

🔹 Y cuando trabajes en `python-scripts`, puedes desactivar:
- PHP Intelephense
- ESLint

De esta forma, V**S Code carga más rápido** y consume menos recursos en cada entorno.

---

#### 🧩 Opción 2: Crear perfiles de trabajo personalizados

Si trabajas en proyectos muy diferentes, crea perfiles de VS Code independientes:

1. Abre la paleta de comandos (`Ctrl + Shift + P`).
2. Escribe "Profiles: Create Profile".
3. Crea un perfil con nombre, por ejemplo:
    - 🧱 Laravel Backend
    - ⚛️ Frontend React
    - 🐍 Python & DevOps

Cada perfil puede tener su propio conjunto de extensiones, temas y configuraciones.

---

#### 📊 Comparativa rápida

| Acción                  | Alcance                                             | Cuándo usarla                                  |
| ----------------------- | --------------------------------------------------- | ---------------------------------------------- |
| **Disable (Workspace)** | Desactiva una extensión solo en el proyecto actual  | Cuando una extensión no se usa en ese proyecto |
| **Disable (Global)**    | Desactiva una extensión en todos los proyectos      | Cuando ya no la necesitas                      |
| **Enable (Workspace)**  | Activa una extensión solo en un proyecto específico | Si solo la usas ahí                            |
| **Enable (Global)**     | Activa una extensión para todos los proyectos       | Para herramientas comunes como Git o Docker    |
| **Perfiles (Profiles)** | Define conjuntos completos de extensiones           | Ideal si alternas entre stacks muy distintos   |

---

### ✅ Beneficio

Esta estrategia te permitirá:
- 🚀 Acelerar el arranque de VS Code  
- 💼 Mantener entornos organizados  
- 🧘‍♂️ Evitar conflictos entre frameworks o lenguajes

---

### ✅ Recomendación final

Mantén solo las extensiones necesarias activas por proyecto o perfil.

Así mejorarás la velocidad de inicio, rendimiento general y estabilidad de VS Code.

---

*Fin del documento*