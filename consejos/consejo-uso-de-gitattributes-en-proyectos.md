# 📚 Guía: Consejo para el uso de `.gitattributes` en tus proyectos

Esta guía te ayudará a evitar problemas con la opción `core.autocrlf` y a mantener consistencia en los finales de línea entre colaboradores en **Windows, Linux o macOS**.

---

## 📄 Uso de `.gitattributes` (recomendado)

Este archivo `.gitattributes` define cómo Git debe manejar los **finales de línea** y otros aspectos de los archivos, asegurando consistencia en todo el proyecto.

### 📝 Pasos para implementarlo

1. **Crear el archivo:**
    Crea un archivo llamado `.gitattributes` en la raíz de tu proyecto si aún no lo tienes.

2. **Agregar reglas básicas:**
    Ejemplo recomendado para proyectos en **Laravel, Next.js o documentación en Markdown**:

    ```ini
    # Forzar finales de línea LF en todo el repo
    * text=auto eol=lf

    # Markdown y archivos de texto
    *.md text eol=lf diff=markdown
    *.txt text eol=lf
    ```

3. **Beneficio**
    > ✅ Con esto, tu repositorio mantendrá un formato uniforme, evitando problemas de compatibilidad y advertencias al hacer `git add .`.

4. **Versionar el archivo**
    > 👉 No olvides agregarlo al repositorio y hacer commit para que todos los colaboradores adopten las mismas reglas:

    ```bash
    git add .gitattributes
    git commit -m "Agregar .gitattributes"
    ```

---

*Fin del documento*
