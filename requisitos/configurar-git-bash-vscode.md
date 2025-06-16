# 🖥️ Guía: Configurar Git Bash como Terminal Predeterminada en Visual Studio Code

Para evitar errores comunes al usar PowerShell (como *"la ejecución de scripts está deshabilitada en este sistema"*), se recomienda configurar **Git Bash** como la terminal predeterminada en **Visual Studio Code (VS Code)**.

---

## 🧪 ¿Qué es Git Bash?

**Git Bash** es una terminal que simula un entorno Linux (Bash) en Windows. Permite usar comandos como `ls`, `cd`, `touch`, `rm`, entre otros.

Esto es útil para trabajar con herramientas modernas como **Laravel**, **Node.js**, **Docker**, etc., especialmente para quienes vienen de entornos Linux/macOS.

---

### ✅ Pasos para configurarla

1. Abre **Visual Studio Code**.

2. Ve a la configuración:
   
- Usa el atajo: `Ctrl + ,`
- O desde el menú: `Archivo → Preferencias → Configuración`

4. En la barra de búsqueda, escribe:

```
terminal predeterminada
```

4. Haz clic en **Editar en settings.json** (puede aparecer como *Edit in settings.json*).

5. Dentro del archivo `settings.json`, agrega las siguientes líneas al final (sin borrar lo que ya existe):

```json
{
    // otras configuraciones...

    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.profiles.windows": {
        "Git Bash": {
            "source": "Git Bash"
        }
    }
}
```

> ⚠ **Importante:** Asegúrate de no eliminar otras configuraciones existentes en el archivo JSON.

6. Guarda los cambios (`Ctrl + S`), luego **cierra y vuelve a abrir VS Code**.

---

### 💡 Resultado:

A partir de ahora, al abrir la terminal (`Ctrl + ñ`) en VS Code, se utilizará **Git Bash por defecto**, lo cual te ofrece:

- ✅ Una experiencia más consistente
- ✅ Evita errores relacionados con permisos de ejecución
- ✅ Acceso a comandos Bash familiares estilo Linux

---

*Fin del documento*
