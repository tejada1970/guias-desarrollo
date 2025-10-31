# 📚 Guía: solucionar-error-gh-delete-repo-wsl

Esta guía te ayudará a solucionar el error `403` **al intentar eliminar un repositorio con GitHub CLI (`gh`) en WSL**.

---

## 🚨 Errores comunes

### ❓ ¿Qué significa este error?

Si al intentar eliminar un repositorio obtienes un error como:

```pgsql
HTTP 403: Must have admin rights to Repository.
This API operation needs the "delete_repo" scope.
```

Esto significa:
- Que tu token de autenticación de GitHub CLI **no tiene permiso para eliminar repositorios**.
- Aunque seas propietario del repositorio, el token que `gh` está usando no tiene el `scope delete_repo`, por lo que GitHub bloquea la acción.

---

### ⚙️ Pasos para solucionarlo

1. **Refresca tu autenticación y añade el scope `delete_repo`:**

```bash
gh auth refresh -h github.com -s delete_repo
```

  - Esto abrirá tu navegador para **reautorizar la CLI** con permisos de eliminación de repositorios.

2. **Verifica los scopes de tu token:**

```bash
gh auth status --show-token
```

  - Asegúrate de que aparezca `delete_repo` en la lista de scopes.

3. **Vuelve a intentar eliminar el repositorio:**

```bash
gh repo delete tu_usuario/nombre-del-repo
```
- Te pedirá confirmar:

```bash
? Type tu_usuario/nombre-del-repo to confirm deletion:
```

- Escribe:

```bash
tu_usuario/nombre-del-repo
```

- 🔍 **Salida esperada:**

```kotlin
✓ Deleted repository tu_usuario/nombre-del-repo
```

> ✍️ **Nota:** Debes ser el **propietario del repositorio** o tener **permisos de administrador**. Si estás usando **WSL** o **Linux**, asegúrate de que el navegador pueda abrir la ventana de autorización correctamente y que estás autenticado con la cuenta correcta.

---

#### ✅ Esto asegura que el repositorio se elimine correctamente sin errores de permisos.

---

*Fin del documento*
