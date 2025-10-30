# 📚 Guía: instalar-kubectl-kind-en-wsl

> 📖 Esta guía te permitirá instalar y configurar **Kind (Kubernetes in Docker)** en **WSL2 (Ubuntu)**, junto con las herramientas necesarias como **kubectl** y **Docker**, para levantar clústeres de Kubernetes de forma local y liviana.

---

## 🧩 1. ¿Qué son y para qué sirven?

| Herramienta | Propósito                                                                                                                            | Instalación requerida                   |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------|
| **kubectl** | Cliente oficial de Kubernetes. Permite interactuar con el clúster (aplicar *manifests*, ver *pods*, consultar *logs*, etc.).         | ✅ Sí, manual                          |
| **Kind**    | Herramienta que permite ejecutar clústeres de Kubernetes dentro de contenedores Docker. Ideal para entornos de desarrollo y pruebas. | ✅ Sí, manual                          |
| **Docker**  | Motor de contenedores necesario para que Kind cree los nodos del clúster.                                                            | ✅ Sí, manual (o desde Docker Desktop) |

---

## 🧰 2. Instalación paso a paso

A continuación, se describen los pasos para preparar tu entorno en **WSL (Ubuntu)**.

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

### 🧰 Instalar kubectl

Ejecuta los siguientes comandos en tu terminal de **WSL (Ubuntu)**:

```bash
# Descargar el binario oficial de la última versión estable
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Dar permisos de ejecución
chmod +x kubectl

# Moverlo a una ruta global (para hacerlo accesible desde cualquier lugar)
sudo mv kubectl /usr/local/bin/

# Verificar instalación y versión
kubectl version --client
```

**🔍 Salida esperada:**

```bash
Client Version: v1.34.1
Kustomize Version: v5.7.1
```

**📘 Interpretación:**

| **Campo**                     | **Qué significa**                                                                                                                                 | **Estado**  |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| **Client Version: v1.34.1**   | Versión del binario `kubectl`. `v1.34.1` es una versión reciente y estable de Kubernetes (junio 2024 aprox.), totalmente compatible con **Kind**. | ✅ Correcto |
| **Kustomize Version: v5.7.1** | `kubectl` incluye internamente la herramienta **Kustomize**, usada para aplicar configuraciones declarativas avanzadas (overlays, patches, etc.). | ✅ Correcto |

✍️ **Notas:**
>
- `/usr/local/bin` es una ruta incluida en el `PATH` del sistema, por eso puedes ejecutar `kubectl` desde cualquier directorio.
- Si prefieres instalarlo en otra ruta, asegúrate de agregarla al `PATH` en tu `~/.bashrc` o `~/.zshrc`.

---

### 🧰 Instalar Kind

#### ✅ Paso 1: Eliminar archivos corruptos

Si intentaste descargar el binario anteriormente y el archivo resultante está dañado o incompleto, es recomendable eliminarlo antes de proceder:

```bash
rm -f ./kind
```

#### ✅ Paso 2: Descargar el binario de Kind

Visita la página de [releases de Kind](https://github.com/kubernetes-sigs/kind/releases?utm_source=chatgpt.com) en **GitHub** y busca la última versión estable. Por ejemplo, si la última versión es `v0.30.0`, puedes descargar el binario correspondiente a tu sistema operativo. Para Linux (AMD64) o (WSL / Ubuntu en Windows), el comando sería:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.30.0/kind-linux-amd64
```

   - 👉 **Importante:** Asegúrate de reemplazar `v0.30.0` con la versión más reciente disponible.

#### ✅ Paso 3: Dar permisos de ejecución

Una vez descargado el archivo, debes otorgarle permisos de ejecución:

```bash
chmod +x ./kind
```

#### ✅ Paso 4: Mover el binario a un directorio en tu PATH

Para poder ejecutar kind desde cualquier lugar, mueve el archivo a un directorio incluido en tu variable de entorno PATH:

```bash
sudo mv ./kind /usr/local/bin/kind
```

#### ✅ Paso 5: Verificar la instalación

Finalmente, verifica que la instalación fue exitosa ejecutando:

```bash
kind version
```

Deberías ver la versión de Kind que descargaste:

**🔍 Salida de ejemplo**

```bash
 kind v0.30.0 go1.24.6 linux/amd64
```

---

### 🚀 Crear un clúster local con Kind

> 👉 **Importante:** Asegúrate de que Docker este encendido y corriendo.

Una vez instaladas las herramientas, puedes crear un clúster de Kubernetes local:

```bash
# Crear un nuevo clúster llamado "demo-cluster"
kind create cluster --name demo-cluster
```

Esto descargará las imágenes necesarias y levantará un clúster en contenedores Docker.

Para listar los clústeres creados:

```bash
kind get clusters
```

Y para conectarte con `kubectl` al clúster activo:

```bash
kubectl cluster-info
```

---

### 🧹 Eliminar un clúster

Si ya no necesitas el clúster:

```bash
kind delete cluster --name demo-cluster
```

---

## 🧩 3. Verificación final

Puedes probar que todo funcione ejecutando:

```bash
kubectl get nodes
```

Deberías ver un nodo (`kind-control-plane`) en estado **Ready**.

---

## 🔗 Recursos útiles

- 🔗 [Documentación oficial de Kind](https://kind.sigs.k8s.io/)
- 🔗 [Documentación oficial de kubectl](https://kubernetes.io/docs/reference/kubectl/)
- 🔗 [Instalar Docker en WSL2](https://docs.docker.com/desktop/wsl/)

> 👇**También puedes consultar la siguiente guía en este repositorio:**
>
> 📖 [instalar-docker-desktop-wsl2-en-windows](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/instalar/instalar-docker-desktop-wsl2-en-windows.md)

---

## ✅ Resultado esperado

Una vez completados los pasos:

- Tienes **Docker**, **Kind** y **kubectl** instalados.
- Puedes levantar un clúster local con `kind create cluster`.
- Puedes gestionarlo con `kubectl`.

---

*Fin del documento*
