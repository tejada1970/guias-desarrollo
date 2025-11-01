# 📚 Guía: instalar-docker-cli-en-wsl

Esta guía explica cómo instalar y configurar el **cliente de Docker (`docker-cli`)** dentro de **WSL2 (Ubuntu)** para conectarse correctamente al motor de contenedores de **Docker Desktop** en Windows 11.

---

## ❓ 1. ¿Qué es y para qué sirve?

| Componente                    | Propósito                                                                                              | Instalación requerida    |
|-------------------------------|--------------------------------------------------------------------------------------------------------|--------------------------|
| **Docker Desktop**            | Motor de contenedores que corre en Windows y gestiona los *daemons* y recursos de Docker.              | ✅ Sí (en Windows)      |
| **Docker CLI (`docker-cli`)** | Cliente de línea de comandos que se instala en WSL para comunicarse con Docker Desktop.                | ✅ Sí (en WSL / Ubuntu) |

> ⚠️ **Importante:** 
>
> Docker Desktop incluye el motor (daemon) de Docker, pero **no instala automáticamente el cliente (`docker-cli`)** dentro de tu distribución WSL.  
> Por eso es necesario instalarlo manualmente para poder usar `docker` desde WSL (Ubuntu).

---

## ⚙️ 2. Requisitos previos

Antes de comenzar, asegúrate de tener instalado:

- ✅ **Windows 11 con WSL2 (Ubuntu)**  
- ✅ **Docker Desktop** con integración WSL2 habilitada  
- ✅ Docker Desktop abierto y corriendo  

> 📖 Consulta las guías:
>
> - 📖 [configurar-linux-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/configurar/configurar-linux-wsl2-en-windows.md)  
> - 📖 [instalar-docker-desktop-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-docker-desktop-wsl2-en-windows.md)

---

## 🧰 3. Instalar `docker-cli`

Ejecuta los siguientes comandos **dentro de tu terminal WSL (Ubuntu):**

```bash
# Actualizar los paquetes
sudo apt update

# Instalar únicamente el cliente de Docker
sudo apt install -y docker-cli
```

> ⚠️ **No instales `docker-ce` ni `docker.io`**, ya que eso intentaría crear un daemon dentro de WSL y entraría en conflicto con el de Docker Desktop.

---

## ✅ 4. Verificar instalación

### Comprobar ubicación del binario:

```bash
which docker
```

🔍 **Salida esperada:**

```bash
/usr/bin/docker
```

### Verificar versión del cliente:

```bash
docker --version
```

🔍 **Salida de ejemplo:**

```nginx
Docker version 28.5.1, build e180ab8
```

✅ Esto confirma que el cliente está instalado correctamente y puede comunicarse con **Docker Desktop**.

---

## 🧪 5. Probar conexión con Docker Desktop

Asegúrate de que **Docker Desktop esté abierto y corriendo en Windows**, y luego ejecuta:

```bash
docker ps
```

🔍 **Salida esperada (tabla vacía o con contenedores activos):**

```nginx
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

Si ves esto sin errores, la conexión con el daemon está funcionando correctamente 🎉

---

## 🚨 6. Errores comunes

| Error                                                                   | Causa probable                                                       | Solución                                                                               |
|-------------------------------------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| `docker: command not found`                                             | No se instaló el cliente (`docker-cli`)                              | Ejecuta `sudo apt install docker-cli`                                                  |
| `Cannot connect to the Docker daemon at unix:///var/run/docker.sock`    | Docker Desktop no está abierto o la integración WSL está desactivada | Docker Desktop → **Settings → Resources → WSL Integration** → activa tu distro Ubuntu. |
| `permission denied while trying to connect to the Docker daemon socket` | Ejecutando sin permisos adecuados                                    | Normalmente no requiere `sudo`, pero asegúrate de que Docker Desktop esté activo.      |          

---

## ✅ 7. Recomendaciones

- Siempre **abre Docker Desktop antes** de usar `docker` dentro de WSL.  
- No inicies servicios de Docker manualmente dentro de Ubuntu (`sudo service docker start` no es necesario).  
- Usa solo el cliente (`docker-cli`) para conectarte al daemon de Docker Desktop.  
- Verifica el socket disponible con:
  ```bash
  ls /var/run/docker.sock
  ```

---

## ✅ 9. Resultado esperado

Una vez completados los pasos:

- `/usr/bin/docker` apunta al cliente nativo de Ubuntu.  
- `docker --version` muestra la versión del cliente.  
- `docker ps` se comunica correctamente con Docker Desktop.  
- Tu entorno WSL está listo para usar Docker, Kubernetes y Kind sin conflictos.

---

## 🔗 8. Recursos adicionales

- 🔗 [Documentación oficial de Docker para WSL2](https://docs.docker.com/desktop/wsl/)

---

*Fin del documento*
