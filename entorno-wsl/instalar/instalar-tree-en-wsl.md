# 📚 Guía: instalar-tree-en-wsl

Esta guía explica cómo usar el comando **`tree`** en Linux (WSL/Ubuntu) para visualizar la estructura de carpetas y archivos de tus proyectos, especialmente útil en proyectos grandes como **Laravel**.

---

## 🎯 Propósito

- Mostrar la estructura de tu proyecto de manera jerárquica y clara.  
- Evitar saturar la terminal con miles de archivos.  
- Facilitar la documentación y auditoría de proyectos.

---

## ❓ ¿Qué es `tree`?

`tree` es un comando de Linux que muestra la estructura completa de carpetas y archivos en forma de árbol, lo que es mucho más visual que `ls`.

🔍 **Salida típica (ejemplo):**

```text
.
├── app
├── bootstrap
├── config
├── database
├── public
├── resources
└── routes
```

Mucho más visual que `ls`, ¿verdad? 😎

---

## ✅ Comprobar si `tree` está instalado

```bash
tree --version
```

- Si está instalado, mostrará la versión (ej.: `tree v1.8.0`).  
- Si no está instalado, mostrará `command not found`.

---

## 🧰 Instalar `tree`

En **Ubuntu (WSL):**

```bash
sudo apt update && sudo apt install tree -y
```

> ✍️ **Nota:** 
>
> En **Git Bash (Windows)** no viene por defecto. Opciones:
>
> - Usar **WSL** para tus comandos de estructura (`ls`, `tree`, etc.).  
> - Instalar un paquete adicional de Unix utilities (más avanzado).

---

## 🌳 Uso práctico en Laravel

Los proyectos Laravel suelen tener miles de archivos en `vendor/` y `node_modules/`, por lo que es recomendable filtrar la salida.

### 📂 Mostrar solo directorios

```bash
tree -d -I "vendor|node_modules|storage|.git
```

🔍 **Ejemplo de salida:**

```text
.
├── app
│   ├── Console
│   ├── Exceptions
│   ├── Http
│   ├── Models
│   └── Providers
├── bootstrap
├── config
├── database
├── public
├── resources
└── routes
```

### 📂 Limitar profundidad del árbol

```bash
tree -d -L 2 -I "vendor|node_modules|storage|bootstrap|.git|public|tests"
```

🔍 **Ejemplo de salida resumida:**

```text
.
├── app
│   ├── Http
│   └── Models
├── config
├── database
└── routes
```

### 📂 Combinar opciones recomendadas

```bash
tree -d -L 2 -I "vendor|node_modules|storage.git"
```

- `-d` → solo directorios  
- `-L 2` → profundidad máxima 2 niveles  
- `-I` → ignorar carpetas grandes o irrelevantes

---

## 📝 Exportar la estructura a un archivo

```bash
tree -d -L 2 -I "vendor|node_modules|storage|.git" > estructura.txt
```

- Esto genera un archivo de texto plano con la estructura del proyecto. 

Abrir en VS Code:

```bash
code estructura.txt
```

> 💡 **Tip:**  
> Puedes acceder y copiar el archivo `estructura.txt` que has creado, desde el **Explorador de Windows**. Abre el explorador y pega esta ruta en la barra de direcciones:
> `\\wsl$\Ubuntu\home\tu_usuario\docker-projects\nombre-del-proyecto`. Cambia el nombre del proyecto para ver otro cualquiera.
> `\\wsl$\Ubuntu\home\tu_usuario\docker-projects` (para ver todos los proyectos)
> `\\wsl$\Ubuntu\home\tu_usuario\nombre-del-proyecto (si no tienes una carpeta personalizada donde guardar los proyectos de `docker`)

---

## 📝 Mostrar archivos específicos

Si quieres ver **solo archivos** pero mantener la jerarquía visual:

✅ **Recomendado para Laravel con profundidad:**

```bash
tree -L 3 -I "vendor|node_modules|storage|.git" -P "*.*" > estructura-ligera.txt
```

Explicación:
- `-P "*.*"` → muestra solo archivos con extensión  
- `-I` → ignora carpetas pesadas  
- Sin `-d` → muestra tanto carpetas como archivos

Esto:
- Muestra hasta 3 niveles.
- Solo archivos.
- Excluye dependencias pesadas.
- Guarda la salida lista para documentación.

### 📂 Ejemplo de estructura (resumida):

.
├── app
│   ├── Http
│   │   └── Controllers
│   │       └── AdminController.php
│   └── Models
│       └── User.php
├── config
│   └── app.php
└── routes
    └── web.php

👉 Mucho más visual y útil para documentación, porque conserva el formato "en árbol".

---

## 🌳 Ventajas de usar `tree`

- Ligero y visual  
- Evita saturar la terminal  
- Útil para documentación, auditorías o revisión de estructura  
- Fácil de abrir y versionar en VS Code

---

*Fin del documento*
