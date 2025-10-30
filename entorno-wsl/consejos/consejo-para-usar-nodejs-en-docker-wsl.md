# 📚 Guía: consejo-para-usar-nodejs-en-docker-wsl

Esta guía ofrece una **recomendación práctica** para optimizar el uso de **Node.js**, **NPM** y frameworks frontend modernos (como **Next.js**, **React**, **Vite** o **SvelteKit**) dentro de entornos **Docker + WSL2**, evitando instalaciones globales innecesarias y mejorando el rendimiento.

---

## 🛠️ Consejos y buenas prácticas

### 👉 Evita instalar Node.js globalmente

> 🚫 **No instales** `Node.js` ni `NPM` de forma global en **Windows** o **WSL**.  
> En su lugar, define la versión y las dependencias directamente dentro del **Dockerfile** de tu aplicación **frontend o PWA**.

Esto garantiza que todos los desarrolladores, entornos de CI/CD y servidores compartan la **misma versión exacta** de Node y dependencias, evitando conflictos y diferencias entre equipos.

---

### ✅ Beneficios de usar Node.js dentro de Docker

| Ventaja             | Descripción                                                   |
|---------------------|---------------------------------------------------------------|
| 🔁 Reproducibilidad | Mismo entorno para todos los desarrolladores y entornos.     |
| 🚀 Entornos limpios | Evita conflictos entre versiones globales de Node/NPM.       |
| 🧹 Sistema ligero   | Mantiene tu WSL sin dependencias innecesarias.               |
| ⚙️ CI/CD listo      | Las mismas imágenes pueden usarse en pipelines o producción. |

---

### 📝 Ejemplo de Dockerfile (para desarrollo)

``` dockerfile
# Etapa base: desarrollo local
FROM node:20-alpine

# Establecer directorio de trabajo
WORKDIR /usr/src/app

# Copiar dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar el resto del código
COPY . .

# Exponer el puerto del servidor de desarrollo
EXPOSE 3000

# Comando por defecto
CMD ["npm", "run", "dev"]
```

> 💡 Ideal para proyectos con **Next.js**, **Vite**, **React** o **PWA** en desarrollo local.

---

### 🐧 Consejo adicional: separar Windows ↔️ WSL

| Entorno              | Rol principal                    | Ejemplos                                          |
|----------------------|----------------------------------|---------------------------------------------------|
| 🪟 **Windows**      | Interfaz y herramientas globales | Docker Desktop, VS Code, Git, Navegador           |
| 🐧 **WSL (Ubuntu)** | Ejecución real del código        | PHP, Node.js, Composer, Docker CLI, kubectl, Kind |

> ✍️ **Recomendación:** Edita tu proyecto en **VS Code Remote - WSL** (`code .`) para evitar problemas de permisos y mejorar el rendimiento.

---

### ✅ Resultado esperado

- Node.js y NPM gestionados dentro del contenedor  
- Entorno de desarrollo reproducible y limpio  
- WSL sin conflictos de versiones  
- Integración total con Docker Desktop y VS Code Remote  

---

*Fin del documento*
