# 📚 Guía: configurar-laravel-k8s-en-wsl

Esta guía muestra cómo desplegar **microservicios Laravel** con **PHP + Composer + Node** en **Kubernetes (Kind)**, sin Docker Compose.

Incluye:

- User Service
- Order Service
- API Gateway (Nginx)
- Bases de datos MySQL aisladas

---

## 🎯 Propósito

Desplegar un entorno de microservicios Laravel con PHP + Composer + Node en un clúster Kubernetes (Kind), con bases de datos MySQL aisladas y un API Gateway unificado, asegurando reproducibilidad, escalabilidad y aislamiento de cada servicio sin depender de Docker Compose.

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

## 📂 Estructura del proyecto

```
my-microservices/
├── k8s/
│   ├── namespace.yaml
│   ├── databases.yaml
│   ├── user-service/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── configmap.yaml
│   ├── order-service/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── configmap.yaml
│   └── gateway/
│       ├── deployment.yaml
│       ├── service.yaml
│       └── configmap.yaml
├── user-service/
│   ├── Dockerfile
│   └── (código Laravel)
├── order-service/
│   ├── Dockerfile
│   └── (código Laravel)
└──
```

---

## 🧰 Dockerfile con PHP, Composer y Node

Cada microservicio debe tener su **Dockerfile** listo. Ejemplo:

```dockerfile
FROM php:8.2-fpm

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    git unzip curl libpng-dev libjpeg-dev libfreetype6-dev zip gnupg \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo_mysql mbstring exif pcntl bcmath opcache

# Instalar Composer globalmente
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin --filename=composer

# Instalar Node.js y actualizar npm globalmente
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs && npm install -g npm@latest

# Copiar el código (vacío al inicio)
WORKDIR /var/www

COPY . .

# Instalar dependencias si existe composer.json
RUN if [ -f composer.json ]; then composer install; fi

# Puerto por defecto de PHP-FPM
EXPOSE 8000

CMD ["php-fpm"]
```

---

## ⚡ Crear la imagen Docker

Ejecuta estos comandos **desde la raíz del proyecto** (`my-microservices/`):

```bash
docker build -t user-service:latest ./user-service
docker build -t order-service:latest ./order-service
```

👉 Esto construye las imágenes Docker de cada microservicio usando sus respectivos Dockerfile.

✅ Explicación:

- `-t user-service:latest` → asigna un nombre y etiqueta a la imagen.
- `./user-service` → ruta del Dockerfile de **User Service**.
- `-t order-service:latest` → asigna un nombre y etiqueta a la imagen.
- `./order-service` → ruta del Dockerfile de **Order Service**.

---

## 🏗️ Crear proyecto Laravel (solo una vez)

Ejecuta estos comandos **desde la raíz del proyecto** (`my-microservices/`):

```bash
docker run --rm -v ./user-service:/var/www user-service:latest composer create-project laravel/laravel .
docker run --rm -v ./order-service:/var/www order-service:latest composer create-project laravel/laravel .
```

👉 Esto crea un proyecto Laravel dentro de cada servicio usando la imagen que ya construiste, **sin instalar PHP, Composer ni Node en tu máquina local**.

Explicación:

- `--rm` → elimina el contenedor al terminar.
- `-v ./user-service:/var/www` → monta la carpeta del microservicio en /var/www dentro del contenedor.
- `user-service:latest` → imagen Docker que contiene PHP + Composer + Node.
- `composer create-project laravel/laravel .` → genera el código de Laravel en la carpeta montada.

---

## 🏷️ Namespace

Crea un espacio lógico para tus servicios:

```yaml
# k8s/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: laravel-micro
```

---

## 🐬 Bases de datos (MySQL)

Puedes usar un Deployment sencillo para cada base de datos:

```yaml
# k8s/databases.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-db
  namespace: laravel-micro
spec:
  selector:
    matchLabels:
      app: user-db
  template:
    metadata:
      labels:
        app: user-db
    spec:
      containers:
        - name: mysql
          image: mysql:8
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: secret
            - name: MYSQL_DATABASE
              value: user_service
          ports:
            - containerPort: 3306
---
apiVersion: v1
kind: Service
metadata:
  name: user-db
  namespace: laravel-micro
spec:
  selector:
    app: user-db
  ports:
    - port: 3306
      targetPort: 3306
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-db
  namespace: laravel-micro
spec:
  selector:
    matchLabels:
      app: order-db
  template:
    metadata:
      labels:
        app: order-db
    spec:
      containers:
        - name: mysql
          image: mysql:8
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: secret
            - name: MYSQL_DATABASE
              value: order_service
          ports:
            - containerPort: 3306
---
apiVersion: v1
kind: Service
metadata:
  name: order-db
  namespace: laravel-micro
spec:
  selector:
    app: order-db
  ports:
    - port: 3306
      targetPort: 3306
```

---

## 🧩 User Service (Deployment + Service + ConfigMap)

```yaml
# k8s/user-service/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: user-service-env
  namespace: laravel-micro
data:
  APP_NAME: "UserService"
  APP_ENV: "local"
  APP_DEBUG: "true"
  DB_CONNECTION: "mysql"
  DB_HOST: "user-db"
  DB_PORT: "3306"
  DB_DATABASE: "user_service"
  DB_USERNAME: "root"
  DB_PASSWORD: "secret"
```

```yaml
# k8s/user-service/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
  namespace: laravel-micro
spec:
  replicas: 1
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
        - name: user-service
          image: user-service:latest
          ports:
            - containerPort: 8000
          envFrom:
            - configMapRef:
                name: user-service-env
          command:
            ["bash", "-c", "php artisan serve --host=0.0.0.0 --port=8000"]
```

```yaml
# k8s/user-service/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: user-service
  namespace: laravel-micro
spec:
  selector:
    app: user-service
  ports:
    - port: 8000
      targetPort: 8000
  type: ClusterIP
```

---

## 🧩 Order Service (Deployment + Service + ConfigMap)

```yaml
# k8s/order-service/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: order-service-env
  namespace: laravel-micro
data:
  APP_NAME: "OrderService"
  APP_ENV: "local"
  APP_DEBUG: "true"
  DB_CONNECTION: "mysql"
  DB_HOST: "order-db"
  DB_PORT: "3306"
  DB_DATABASE: "order_service"
  DB_USERNAME: "root"
  DB_PASSWORD: "secret"
```

```yaml
# k8s/order-service/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-service
  namespace: laravel-micro
spec:
  replicas: 1
  selector:
    matchLabels:
      app: order-service
  template:
    metadata:
      labels:
        app: order-service
    spec:
      containers:
        - name: order-service
          image: order-service:latest
          ports:
            - containerPort: 8000
          envFrom:
            - configMapRef:
                name: order-service-env
          command:
            ["bash", "-c", "php artisan serve --host=0.0.0.0 --port=8000"]
```

```yaml
# k8s/order-service/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: order-service
  namespace: laravel-micro
spec:
  selector:
    app: order-service
  ports:
    - port: 8000
      targetPort: 8000
  type: ClusterIP
```

> ✍️ **Nota:** Para producción se recomienda usar nginx + php-fpm en lugar de `php artisan serve`.

---

## 🚪 API Gateway (Nginx) - (Deployment + Service + ConfigMap)

```yaml
# k8s/gateway/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
  namespace: laravel-micro
data:
  default.conf: |
    server {
        listen 80;

        location /users/ {
            proxy_pass http://user-service:8000/;
        }

        location /orders/ {
            proxy_pass http://order-service:8000/;
        }

        location / {
            return 200 'API Gateway running 🚀';
            add_header Content-Type text/plain;
        }
    }
```

```yaml
# k8s/gateway/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-gateway
  namespace: laravel-micro
spec:
  replicas: 1
  selector:
    matchLabels:
      app: api-gateway
  template:
    metadata:
      labels:
        app: api-gateway
    spec:
      containers:
        - name: nginx
          image: nginx:alpine
          ports:
            - containerPort: 80
          volumeMounts:
            - name: nginx-conf
              mountPath: /etc/nginx/conf.d
      volumes:
        - name: nginx-conf
          configMap:
            name: nginx-config
```

```yaml
# k8s/gateway/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: api-gateway
  namespace: laravel-micro
spec:
  selector:
    app: api-gateway
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
  type: NodePort
```

---

## 🚀 Desplegar en Kind

```bash
# Crea el clúster local
kind create cluster --name laravel-micro
# Aplica los manifests
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/databases.yaml
kubectl apply -f k8s/user-service/
kubectl apply -f k8s/order-service/
kubectl apply -f k8s/gateway/
# Accede al Gateway
kubectl port-forward service/api-gateway 8080:80 -n laravel-micro
```

---

## ✨ Conclusión

### Accesos finales

- `http://localhost:8080/users/` → User Service
- `http://localhost:8080/orders/` → Order Service

### Ventajas

- Microservicios independientes con su propio Laravel + Node + Composer.
- Bases de datos aisladas.
- Gateway unificado.
- Totalmente reproducible y portable con Kind.
- Sin Docker Compose.

---

*Fin del documento*
