# 📚 Guía: Configurar Docker Desktop con WSL2 en Windows

Esta guía te ayudará a configurar **Docker Desktop** en Windows 11 usando **WSL2**.  

---

## 1. Configurar Docker Desktop con WSL2 (opcional)

👉 Este paso es solo si planeas usar Docker directamente desde Ubuntu en WSL.  
Si prefieres Git Bash, PowerShell o CMD, no es necesario activar esta integración.

1. Abre Docker Desktop desde el menú Inicio.  
2. En la primera ejecución, acepta los permisos de administrador.  
3. Ve a ⚙️ **Settings → Resources → WSL Integration**.  
4. Marca tu distro de Ubuntu.  

**Ejemplo:**  
- Desmarca: `Enable integration with my default WSL distro`  
- Activa: `Enable integration with additional distros: [x] Ubuntu`  

---

## 2. Probar Docker

1. Abre **Ubuntu en WSL** o tu terminal de preferencia (Git Bash, PowerShell, CMD).  
2. Ejecuta:  

```bash
docker --version
```

3. Deberías ver algo como:  

```
Docker version 27.0.2, build 123abc
```

4. Prueba ejecutando un contenedor:  

```bash
docker run hello-world
```

- Esto descargará una imagen pequeña y mostrará un mensaje de éxito.  

5. Opcional: listar contenedores e imágenes

```bash
docker ps -a
docker images
```

---

## 3. Verificar integración entre Docker y WSL2

En Ubuntu ejecuta:  

```bash
docker info | grep WSL
```

Deberías ver:  

```
WSL Integration: enabled
```

---

## ✅ Resumen

Con esto ya tienes:    
- Configurado para usar WSL2 y Ubuntu.  
- Docker probado con `hello-world`.  

👉 Ahora estás listo para crear contenedores de Laravel, MySQL, Redis, etc.

---

*Fin del documento*