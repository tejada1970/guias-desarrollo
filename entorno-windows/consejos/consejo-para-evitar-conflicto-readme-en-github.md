# 📚 Guía: consejo-para-evitar-conflicto-readme-en-github

Esta guía te ayudará a evitar un error muy común con el archivo `README.md` a la hora de crear un nuevo repositorio en **GitHub**.

---

## 🛠️ Consejos y buenas prácticas

### 🤔 ¿Cuándo (no) marcar "Add a README file"?

Cuando creas un nuevo repositorio en **GitHub**, puedes optar por iniciar con un archivo `README.md`.

> ❗ **Pero atención:** si ya tienes un archivo `README.md` en tu proyecto local y también marcas esta opción en **GitHub**, al hacer el primer `git push`, es probable que veas un error similar a este ejemplo:

```bash
! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/tuusuario/mi-proyecto.git'
```

Este error ocurre porque los contenidos del `README.md` local y el que creó **GitHub** no coinciden, y **Git** detecta un conflicto entre ambos. Esto obliga a realizar un **merge**, lo cual puede ser confuso si estás empezando.

---

### ✅ Recomendación:

Si ya tienes un `README.md` en tu proyecto local, **no marques la opción** en **GitHub**.

Si no tienes ningún `README.md` aún, puedes marcarla sin problema.

Así evitarás conflictos innecesarios al subir tu proyecto por primera vez.

---

*Fin del documento*
