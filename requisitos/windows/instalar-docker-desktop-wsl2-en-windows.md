# 📚 Guía: Instalación de Docker Desktop con WSL2 en Windows

Esta guía te ayudará a instalar **Docker Desktop** en Windows 11 usando **WSL2**.  

🔹 **¿Qué es Docker y por qué lo necesitamos?**  
Docker permite crear y ejecutar aplicaciones dentro de contenedores.  
Un contenedor es como una mini-computadora con todo lo que necesita tu aplicación (PHP, MySQL, Node, etc.).  

Gracias a Docker:  
- No necesitas instalar MySQL, PHP, Redis, etc. directamente en Windows.  
- Todo vive dentro de contenedores aislados, fáciles de borrar o reiniciar.  
- En Windows 11, Docker Desktop usa WSL2 como motor, por eso es el segundo requisito después de instalar Ubuntu con WSL2.

---

## 🧰 Pasos para la instalación

### 1. Descargar Docker Desktop

1. Ve a la página oficial 👉 [Docker Desktop para Windows](https://www.docker.com/products/docker-desktop/)  
2. Descarga el instalador para Windows 11 (x86_64 o ARM64 según tu PC).  

👉 ¿Cómo saber si tu equipo es x86_64 o ARM64?  
Abre PowerShell y ejecuta:  

```powershell
$env:PROCESSOR_ARCHITECTURE
```

👉 Lo más común es AMD64 (la mayoría de PCs Windows 11).  

---

### 2. Instalar Docker Desktop

1. Ejecuta el archivo descargado.  
2. Durante la instalación:  
   - Asegúrate de que está marcada la opción **Use WSL 2 instead of Hyper-V**.  
   - Haz clic en **Next** y termina la instalación.  
   - Reinicia tu PC si lo pide.

---

## ⚙️ Configurar Docker Desktop con WSL2 (opcional)

👉 Este paso es solo si planeas usar Docker directamente desde Ubuntu en WSL.  
Si prefieres Git Bash, PowerShell o CMD, no es necesario activar esta integración.

- 📄 [Configurar Docker Desktop con WSL2 en Windows](https://github.com/tejada1970/guias-desarrollo/blob/master/configuraciones/configurar-docker-desktop-wsl2-en-windows.md)

---

## 🛠 Utilidades

Si quieres solucionar errores comunes en la terminal de Ubuntu, revisa:

- 📄 [Solucionar error de terminal Ubuntu (fallo catastrófico) causado por Docker Desktop y WSL2](https://github.com/tejada1970/guias-desarrollo/blob/master/utilidades/solucionar-error-terminal-ubuntu-docker-wsl2.md)

---

*Fin del documento*
