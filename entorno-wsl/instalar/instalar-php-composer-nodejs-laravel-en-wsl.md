# 📚 Guía: instalar-php-composer-nodejs-laravel-en-wsl

> Esta guía describe dos formas de preparar tu entorno Laravel dentro de **WSL (Ubuntu)**:  
>
> - 🐧 **Instalación nativa en WSL**, ideal para desarrollo directo. 
> - 🐋 **Configuración mediante Docker**, (recomendada) para entornos profesionales y colaborativos.
 
---

## 🎯 Propósito

Establecer un entorno de desarrollo **Laravel** totalmente funcional dentro de **WSL2 (Ubuntu)**, compatible con proyectos basados en **Docker**, **Kind** y **Kubernetes**, asegurando rendimiento, consistencia y escalabilidad.

---

## 🧠 Antes de comenzar

Asegúrate de tener instalado:

- ✅ **Windows 11 con WSL2 (Ubuntu)**  
- ✅ **Docker Desktop con integración WSL2 habilitada (motor de contenedores)**
- ✅ **Git**  
- ✅ **Visual Studio Code + extensión (`Remote - WSL`)**

> 📖 Consulta las guías: 
> 
> - 📖 [configurar-linux-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/configurar/configurar-linux-wsl2-en-windows.md)
> - 📖 [instalar-docker-desktop-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-docker-desktop-wsl2-en-windows.md)
> - 📖 [instalar-git-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-git-en-windows.md)
> - 📖 [instalar-vscode-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-vscode-en-windows.md)

---

## 🐧 Instalación nativa en WSL, ideal para desarrollo directo

### 🧰 1. Instalar PHP 8.2+ en WSL (Ubuntu)

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
sudo apt install -y php8.2 php8.2-cli php8.2-common php8.2-mbstring php8.2-xml php8.2-curl php8.2-zip php8.2-bcmath unzip git curl
```

🔍 **Verificar versión:**
```bash
php -v
```

✅ **Salida esperada:**

```
PHP 8.2.x (cli) (built: ...)
```

### 🧰 2. Instalar Composer

```bash
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
rm composer-setup.php
```

🔍 **Verificar instalación:**
```bash
composer --version
```

✅ **Salida esperada:**
```
Composer version 2.x.x ...
```

Agrega el binario global al `PATH` (solo una vez):

```bash
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

> ✍️ **Nota:** Este paso es necesario si planeas instalar paquetes globales con Composer (**por ejemplo laravel**).

### 🧰 3. Instalar Node.js y npm

```bash
# Instalar Node.js 20 y npm
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Actualizar npm a la última versión
sudo npm install -g npm@latest
```

🔍 **Verificar versiones:**

```bash
node -v
npm -v
```

✅ **Salida esperada:**

```scss
v20.x.x
x.x.x (npm version)
```

> ✍️ **Nota:** Esto permite compilar assets con Vite, Tailwind u otros paquetes frontend de Laravel.

### 🧰 4. Instalar Laravel Installer globalmente

```bash
composer global require laravel/installer
```

🔍 **Verificar instalación:**
```bash
laravel --version
```

✅ **Salida esperada:**
```
Laravel Installer 5.x
```

### 🚀 5. Crear un nuevo proyecto Laravel

```bash
cd ~/projects
laravel new myapp
cd myapp
php artisan serve
```

🌐 **Abrir en el navegador:**
```
http://localhost:8000
```

### 🧪 6. Comprobación rápida

| Herramienta           | Comando              | Resultado esperado                                   |
|-----------------------|----------------------|------------------------------------------------------|
| 🐘 PHP               | `php -v`             | PHP 8.2.x                                            |
| 🎼 Composer          | `composer --version` | Composer 2.x.x                                       |
| 🚀 Laravel Installer | `laravel --version`  | Laravel Installer 5.x                                |
| 🌐 Servidor local    | `php artisan serve`  | Development server running at `127.0.0.1:8000`       |
|🔹 Node.js            | `node -v`            | v20.x.x                                              |
|🔹 npm                | `npm -v`             | Última versión                                       |

### ✅ **Resultado esperado:**
- PHP 8.2+ funcionando correctamente  
- Composer global disponible  
- Laravel operativo  
- Proyectos creados en WSL (~/docker-projects/...)

---

## 🐋 Configuración mediante Docker, (recomendada) para entornos profesionales y colaborativos

Esta configuración contiene **dos ejemplos prácticos**:

1. 🧩 **Un solo microservicio Laravel con Docker**
2. 🧱 **Arquitectura completa de múltiples microservicios (Laravel + Gateway + DBs)**

### 🧩 Ejemplo 1 — Un Microservicio Laravel con Docker

#### 📂 Estructura del proyecto

Ejemplo con un microservicio llamado user-service:

```text
my-project/
└── user-service/
    ├── Dockerfile
    ├── docker-compose.yml
    ├── .env
    └── (código Laravel se generará aquí)
```

#### 🐋 Dockerfile

```dockerfile
# user-service/Dockerfile
FROM php:8.2-fpm

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    git unzip curl libpng-dev libjpeg-dev libfreetype6-dev zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo_mysql mbstring exif pcntl bcmath opcache

# Instalar Composer globalmente
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin --filename=composer

# Instalar Node.js y actualizar npm globalmente
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs && npm install -g npm@latest

WORKDIR /var/www

# Copiar el código (vacío al inicio)
COPY . .

# Instalar dependencias si existe composer.json
RUN if [ -f composer.json ]; then composer install; fi

EXPOSE 8000
CMD ["php-fpm"]
```

#### ⚙️ docker-compose.yml

```yaml
version: "3.9"

networks:
  app-network:

services:
  app:
    build: .
    container_name: user-service
    working_dir: /var/www
    volumes:
      - .:/var/www
    ports:
      - "8000:8000"
    environment:
      - APP_ENV="local"
      - APP_DEBUG="true"
      - APP_KEY=""
      - DB_HOST="db"
      - DB_PORT="3306"
      - DB_DATABASE="user_service"
      - DB_USERNAME="root"
      - DB_PASSWORD="secret"
    depends_on:
      - db
    command: bash -c "php artisan serve --host=0.0.0.0 --port=8000"
    networks:
      - app-network

  db:
    image: mysql:8
    container_name: user-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: user_service
    ports:
      - "3307:3306"
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - app-network

volumes:
  db_data:
```

#### 📁 Crear el proyecto Laravel dentro del contenedor

Si estás en WSL o Windows, dentro de my-project/user-service/, ejecuta:

```bash
docker compose run --rm app composer create-project laravel/laravel .
```

**Esto hará lo siguiente:**
- Usa el contenedor app (que ya tiene PHP + Composer).
- Crea un nuevo proyecto Laravel dentro de la carpeta actual.
- No instala nada en tu máquina.

> ⚠️ Este comando solo se ejecuta una vez para crear el proyecto Laravel; luego usas docker compose up normalmente.

#### 🚀 Levantar el servicio

Una vez creado el proyecto, levanta todo con:

```bash
docker compose up --build
```

**Tu microservicio estará disponible en:**
👉 `http://localhost:8000`

Y tendrá una base de datos MySQL accesible desde db (o localhost:3307 si accedes desde tu host).

---

#### 🧠 Conexión Laravel a MySQL

En el `.env` de Laravel asegúrate de tener:

```env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=user_service
DB_USERNAME=root
DB_PASSWORD=secret
```

Así Laravel se conecta directamente al contenedor de base de datos.

---

#### 🚀 4. Crear otro microservicio

Solo duplica la carpeta `user-service`:

```bash
cp -r user-service order-service
```

Y cambia los puertos y variables:

En `order-service/docker-compose.yml` → `ports: "8001:8000`"

En `.env` → `DB_DATABASE=order_service`

Luego levantas todos los servicios juntos desde el nivel superior, con una composición raíz si lo deseas.

---

### 🧱 Ejemplo 2 — Arquitectura Completa de Múltiples Microservicios

#### 📂 Estructura del proyecto

```text
my-microservices/
├── docker-compose.yml          # Orquestador principal
├── user-service/
│   ├── Dockerfile
│   ├── .env
│   └── (código Laravel)
├── order-service/
│   ├── Dockerfile
│   ├── .env
│   └── (código Laravel)
└── gateway/
    └── nginx.conf
```

#### 🐋 Dockerfile (para cada microservicio Laravel)

```dockerfile
FROM php:8.2-fpm

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    git unzip curl libpng-dev libjpeg-dev libfreetype6-dev zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo_mysql mbstring exif pcntl bcmath opcache

# Instalar Composer globalmente
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin --filename=composer

# Instalar Node.js y actualizar npm globalmente
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs && npm install -g npm@latest

WORKDIR /var/www

# Copiar el código (vacío al inicio)
COPY . .

# Instalar dependencias si existe composer.json
RUN if [ -f composer.json ]; then composer install; fi

EXPOSE 9000
CMD ["php-fpm"]
```

#### ⚙️ docker-compose.yml (raíz)

```yaml
version: "3.9"

networks:
  app-network:

volumes:
  user_data:
  order_data:

services:
  user-service:
    build: ./user-service
    container_name: user-service
    working_dir: /var/www
    volumes:
      - ./user-service:/var/www
    environment:
      - DB_HOST="user-db"
      - DB_DATABASE="user_service"
      - DB_USERNAME="root"
      - DB_PASSWORD="secret"
    depends_on:
      - user-db
    command: bash -c "php artisan serve --host=0.0.0.0 --port=8000"
    ports:
      - "8000:8000"
    networks:
      - app-network

  order-service:
    build: ./order-service
    container_name: order-service
    working_dir: /var/www
    volumes:
      - ./order-service:/var/www
    environment:
      - DB_HOST="order-db"
      - DB_DATABASE="order_service"
      - DB_USERNAME="root"
      - DB_PASSWORD="secret"
    depends_on:
      - order-db
    command: bash -c "php artisan serve --host=0.0.0.0 --port=8000"
    ports:
      - "8001:8000"
    networks:
      - app-network

  user-db:
    image: mysql:8
    container_name: user-db
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: user_service
    volumes:
      - user_data:/var/lib/mysql
    networks:
      - app-network

  order-db:
    image: mysql:8
    container_name: order-db
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: order_service
    volumes:
      - order_data:/var/lib/mysql
    networks:
      - app-network

  gateway:
    image: nginx:alpine
    container_name: api-gateway
    ports:
      - "8080:80"
    volumes:
      - ./gateway/nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - user-service
      - order-service
    networks:
      - app-network
```

#### 🌐 gateway/nginx.conf

```nginx
server {
    listen 80;

    location /users/ {
        proxy_pass http://user-service:8000/;
    }

    location /orders/ {
        proxy_pass http://order-service:8000/;
    }

    location / {
        return 200 'API Gateway is running 🚀';
        add_header Content-Type text/plain;
    }
}
```

#### 📁 Crear los proyectos Laravel dentro del contenedor

Si estás en WSL o Windows, dentro de my-microservices/user-service/, ejecuta:

```bash
docker compose run --rm user-service composer create-project laravel/laravel .
docker compose run --rm order-service composer create-project laravel/laravel .
```

#### 🚀 Levantar todo el ecosistema

```bash
docker compose up --build
```

Accesos:
- Gateway → http://localhost:8080
- User Service → http://localhost:8000
- Order Service → http://localhost:8001

---

#### 🧠 Conexión Laravel a MySQL

En el `.env` de Laravel asegúrate de tener:

📘 `user-service/.env`

```env
APP_NAME=UserService
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=user-db
DB_PORT=3306
DB_DATABASE=user_service
DB_USERNAME=root
DB_PASSWORD=secret
```

📘 `order-service/.env`

```env
APP_NAME=OrderService
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8001

DB_CONNECTION=mysql
DB_HOST=order-db
DB_PORT=3306
DB_DATABASE=order_service
DB_USERNAME=root
DB_PASSWORD=secret
```

Así Laravel se conecta directamente al contenedor de base de datos.

---

### 🔍 Comparativa: WSL vs Docker

| Aspecto              | Instalación en WSL              | Dependencias en Docker |
|----------------------|---------------------------------|------------------------|
| 🔁 Reproducibilidad | ⚠️ Variable según entorno local | ✅ Garantizada        |
| 💻 Rendimiento      | ✅ Nativo (rápido)              | ⚙️ Ligera sobrecarga  |
| 🧩 Aislamiento      | ⚠️ Parcial                      | ✅ Completo           |
| ⚙️ Compatibilidad   | ⚠️ Depende del sistema          | ✅ Homogénea          |
| 🌍 Ideal para       | Desarrollo individual            | Equipos / Producción  |

---

## ✨ Conclusión

- Para proyectos **individuales o experimentales**, instalar PHP, Composer y Laravel dentro de **WSL** es suficiente.  
- Para proyectos **colaborativos, CI/CD o Kubernetes**, define las dependencias en **Dockerfiles** para mantener entornos reproducibles.  
- **WSL + Docker Desktop + VS Code Remote** es la combinación más más óptima de las dos, para rendimiento y productividad.

---

## ✅ Recomendación Profesional

La mejor forma de hacerlo profesionalmente y la más óptima de todas es usando Kubernetes (Kind).

Para ver detalles, consulta la siguiente guía:
- 📖 [configurar-laravel-k8s-en-wsl](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-wsl/configurar/configurar-laravel-k8s-en-wsl.md)

*Fin del documento*
