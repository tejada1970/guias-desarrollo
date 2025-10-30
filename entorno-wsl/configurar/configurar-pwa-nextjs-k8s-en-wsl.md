# 📚 Guía: configurar-pwa-nextjs-k8s-en-wsl

Esta guía explica cómo configurar y desplegar una aplicación **PWA
basada en Next.js** dentro de **Kubernetes (Kind)**, usando Docker como entorno de construcción y ejecución.

---

## 🎯 Propósito

Establecer un entorno de desarrollo reproducible para **Next.js** (PWA) dentro de **Kind**, usando imágenes Docker y Kubernetes para mantener un flujo moderno y limpio, sin dependencias globales de Node.js en el host.

---

## 🧠 Antes de comenzar

Asegúrate de tener instalado:

- ✅ **Windows 11 con WSL2 (Ubuntu)**
- ✅ **Docker Desktop con integración WSL2 habilitada (motor de contenedores)**
- ✅ **Git**
- ✅ **Visual Studio Code + extensión (`Remote - WSL`)**
- ✅ **kubectl y Kind** (para crear y gestionar el clúster local de Kubernetes)

> 📖 Consulta las guías:
>
> - 📖 [configurar-linux-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/configurar/configurar-linux-wsl2-en-windows.md)
> - 📖 [instalar-docker-desktop-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-docker-desktop-wsl2-en-windows.md)
> - 📖 [instalar-git-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-git-en-windows.md)
> - 📖 [instalar-vscode-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-vscode-en-windows.md)
> - 📖 [instalar-kubectl-kind-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/instalar/instalar-kubectl-kind-en-wsl.md)

---

## 🛠️ Consejos y buenas prácticas

> - 📖 [consejo-para-usar-nodejs-en-docker-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/consejos/consejo-para-usar-nodejs-en-docker-wsl.md)

---

## 🐙 GitHub CLI `gh` (opcional-recomendado)

Guía para instalar y usar la herramienta oficial de GitHub desde la terminal. Por ejemplo, para crear repositorios desde la línea de comandos:
- 📖 [instalar-github-cli-gh-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/instalar/instalar-github-cli-gh-en-wsl.md)

---

## 📂 Estructura del proyecto (ejemplo)

```text
pwa-next/
|
├── .gitignore
├── .gitattributes
├── README.md
├── LICENSE
|
├── k8s/
│   ├── namespace.yaml
│   ├── deployment.yaml
│   ├── service.yaml
|
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── next.config.js
│   └── (código Next.js)
└──
```

---

## 🐋 Dockerfile para PWA (Next.js)

Este Dockerfile está pensado **para desarrollo local**, usando el
servidor de desarrollo de Next.js (`npm run dev`).

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

---

## 📝 Añadir `.dockerignore` (muy recomendado para PWA):

```dockerignore
node_modules
.next
.git
*.log
```

---

## ⚡ Crear la imagen Docker

Desde la raíz del proyecto (`pwa-next/`):

``` bash
docker build -t pwa:latest .
```

Explicación:

-   `-t pwa:latest` → Asigna nombre y etiqueta a la imagen.
-   `.` → Indica que el Dockerfile está en el directorio actual.

---

## 🚀 Ejecutar en local con Docker

Para probar la aplicación sin Kubernetes:

``` bash
docker run -it --rm -p 3000:3000 pwa:latest
```

Luego abre en tu navegador:\
👉 `http://localhost:3000`

---

## 🚀 Desplegar en Kubernetes (Kind)

### 🏷️ Namespace de Kubernetes

```yaml
# k8s/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: pwa
```

### 🧩 Deployment de la PWA

```yaml
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pwa
  namespace: pwa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pwa
  template:
    metadata:
      labels:
        app: pwa
    spec:
      containers:
        - name: pwa
          image: pwa:latest
          ports:
            - containerPort: 3000
```

### 🧩 Service para la PWA

```yaml
# k8s/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: pwa
  namespace: pwa
spec:
  selector:
    app: pwa
  ports:
    - port: 3000
      targetPort: 3000
  type: ClusterIP
```

### ⚡ Crear la imagen Docker

Desde la raíz del proyecto `pwa-next/`:

```bash
docker build -t pwa-next ./frontend
```

### 🚀 Desplegar en Kind

``` bash
# Crea el clúster local
kind create cluster --name pwa
# Aplica los manifests
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
# Accede a la PWA
kubectl port-forward service/pwa 3000:3000 -n pwa
```

**Abre en el navegador:**
👉 `http://localhost:3000`

---

## ✅ Resultado esperado
- Contenedor Next.js corriendo en Kubernetes (Kind)
- Acceso a la PWA desde `localhost:3000`
- Entorno reproducible y aislado
- Sin necesidad de Node.js instalado globalmente

---

## 💡 Buenas prácticas

| Consejo                       | Descripción                                                      |
|-------------------------------|------------------------------------------------------------------|
| 🧩 Usa imágenes fijas        | Ejemplo: `node:20-alpine` en lugar de `latest`.                  |
| 🧹 Añade `.dockerignore`     | Excluye `node_modules`, `.next`, `.git`, etc.                    |
| 🧱 Un servicio por contenedor| Evita mezclar frontend y backend en la misma imagen.             |
| ⚙️ Usa ConfigMaps o Secrets  | Para variables de entorno (si las necesitas).                    |

---

## ✨ Conclusión
Este entorno te permite trabajar con una **PWA moderna basada en
Next.js** dentro de **Kubernetes (Kind)**, totalmente aislada,
reproducible y sin dependencias globales.

> ✍️ **Nota:**
>
> Esta configuración usa `npm run dev` para desarrollo dentro de `Kubernetes`.
>
> Cuando prepares el entorno de producción, deberás crear una segunda imagen con `npm run build` + `next start`.

---

*Fin del documento*
