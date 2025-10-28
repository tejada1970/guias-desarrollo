# 📚 Guía: consejo-para-trabajar-con-vscode-wsl

Esta guía ofrece buenas prácticas para optimizar tu flujo de trabajo con **Visual Studio Code** y **Windows Subsystem for Linux (WSL2)**.

---

## 🛠️ Consejos y buenas prácticas

> ✅ **Siempre trabaja dentro del sistema de archivos Linux** (`/home/usuario/...`), en lugar de rutas montadas de Windows como `/mnt/c/...`.  
> Esto mejora el rendimiento y evita problemas de permisos.

> ✅ **Usa las mismas extensiones dentro del entorno remoto.**  
> Cuando abras un proyecto en WSL, VS Code te preguntará si deseas instalar las extensiones también dentro del entorno Linux. Acepta para que funcionen correctamente.

> ✅ **Docker y WSL2 funcionan juntos.**  
> Si usas contenedores, instala también las extensiones:  
>
>  - `Docker (Microsoft)`
>  - `Docker DX (Docker)`
>
> Ambas detectarán automáticamente los contenedores ejecutándose en WSL.

> ✅ **Un servidor por distribución.**  
> Si usas más de una distro de Linux (por ejemplo Ubuntu y Debian), VS Code instalará su propio servidor en cada una.

> ⚡ Siguiendo estas buenas prácticas, tu entorno VS Code + WSL será más estable y eficiente.

---

*Fin del documento*