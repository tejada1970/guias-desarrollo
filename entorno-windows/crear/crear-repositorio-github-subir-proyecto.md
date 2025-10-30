# 📚 Guía: crear-repositorio-github-subir-proyecto

Esta guía, te ayudará paso a paso a crear un repositorio en **GitHub** y subir tu proyecto local (desde cero).

---

## 🧾 Crear una cuenta en GitHub

Si no tienes una cuenta:

- Ve a https://github.com/
- Haz clic en **Sign up** (Registrarse).
- Rellena el formulario.
- Sigue los pasos para verificar tu cuenta y completar el registro.

---

## 📁 Crear un nuevo repositorio

1. Inicia sesión en GitHub.
2. Haz clic en el botón + (esquina superior derecha) → New repository.
3. Completa los campos:
    - **Repository name:** Nombre del proyecto (ej. mi-proyecto).
    - (opcional) **Description:** Puedes añadir una breve descripción sobre tu proyecto.
    - Marca la opción **Public** o **Private** según prefieras.
    - (Opcional) Marca **Add a README file** si quieres iniciar con un archivo README.

    > ⚠️ **Importante:** Si tu proyecto local ya tiene un archivo `README.md`, **no marques esta opción**. De lo contrario, al subir tu proyecto, podrías recibir un error de **merge**. Para evitar ese problema, te recomiendo consultar esta guía antes de continuar:

    - 📖 [consejo-para-evitar-conflicto-readme-en-github](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/consejos/consejo-para-evitar-conflicto-readme-en-github.md)

4. Haz clic en **Create repository**.

---

## 💻 Inicializar Git en tu proyecto local (si aún no lo has hecho)

> 🔹 **Reemplaza:** la **URL** de ejemplo **`https://github.com/tu-usuario/mi-proyecto.git`** en `git remote add origin` por la **URL** real del repositorio que creaste. Verifica también antes de hacer `git push` si tu rama es **master**, **main** u otra.

Abre una terminal en la raíz de tu proyecto local (ejemplo: `Git Bash` en VS Code) y ejecuta de uno en uno los siguientes comandos:

```bash
git init
git add .
git commit -m "Primer commit"
git remote add origin https://github.com/tu-usuario/mi-proyecto.git
git push -u origin master
```

---

## ✅ Verifica que tu proyecto esté en GitHub

Ve a tu repositorio en **GitHub** y confirma que los archivos del proyecto aparecen correctamente.

---

*Fin del documento*