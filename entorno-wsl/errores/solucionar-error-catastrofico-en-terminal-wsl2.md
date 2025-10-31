# 📚 Guía: solucionar-error-catastrofico-en-terminal-wsl2

Esta guía te ayudará a solucionar el error (fallo catastrófico) causado por Docker Desktop y WSL2:

```
Error catastrófico – Wsl/Service/E_UNEXPECTED
```

---

## 🚨 Errores comunes

### ❓ ¿Qué significa este error?

Básicamente, WSL (el servicio de Linux en Windows) se quedó colgado.

Suele pasar después de tocar la integración en Docker Desktop, porque Docker fuerza cambios en cómo se conecta con la distro (Ubuntu u otra).

Si después de haber realizado este paso:

- Configurar Docker Desktop con WSL2:
  - Abre Docker Desktop desde el menú Inicio.
  - En la primera ejecución, te pedirá permisos de administrador → acéptalos.
  - Ve a ⚙️ **Settings → Resources → WSL Integration**.
  - Marca tu distro de Ubuntu para que Docker pueda usarla.

**Ejemplo:**  
`Enable integration with my default WSL distro [x] Ubuntu`

Y te sale este error en tu terminal de Ubuntu:

```
Error catastrófico Código de error: Wsl/Service/E_UNEXPECTED
Press any key to continue...
```

---

### ⚙️ Pasos para solucionarlo

#### Opción 1: Reiniciar la integración de Docker Desktop

1. Abre **Docker Desktop → ⚙️ Settings → Resources → WSL Integration**.  
2. Haz clic en **Restart the WSL integration**.  

👉 Esto suele arreglarlo al forzar un reinicio limpio.

#### Opción 2: Reiniciar manualmente WSL (👉 más seguro)

1. Abre **PowerShell como administrador** y ejecuta:

```powershell
wsl --shutdown
```

- Esto apaga todas tus distros Linux y reinicia el servicio de WSL.  
- Luego abre Ubuntu desde el menú Inicio.  

2. Verificar que tu Ubuntu sigue ahí:

```powershell
wsl -l -v
```

- Deberías ver tu Ubuntu listado con `VERSION 2`.

3. Probar Docker otra vez en Ubuntu:

```bash
docker run hello-world
```

- Si vuelve a salir el mensaje de éxito, ya está todo bien.

---

### ⚠️ Importante

No se pierde nada de tu configuración de Ubuntu:  
Tus archivos, configuraciones y lo que ya instalaste (git, composer, etc.) siguen ahí.  
El problema fue solo un fallo en la conexión entre Docker Desktop y WSL2.

---

### 🛠️ Si no se arregla

Si después de reiniciar WSL y Docker Desktop el error sigue:

1. En **Docker Desktop → Settings → Resources → WSL Integration**:  
   - Desmarca Ubuntu → **Apply & Restart**.  
   - Luego vuelve a marcar Ubuntu → **Apply & Restart**.  

👉 Esto fuerza a Docker a reconfigurar la integración con tu Ubuntu y debería recuperar la normalidad sin perder nada.

---

*Fin del documento*
