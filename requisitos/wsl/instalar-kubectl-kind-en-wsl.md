# 📚 Guía: Instalar kubectl + Kind en WSL / Ubuntu

> 📖 Esta guía te permitirá instalar y configurar **Kind (Kubernetes in Docker)** en **WSL2 (Ubuntu)**, junto con las herramientas necesarias como **kubectl** y **Docker**, para levantar clústeres de Kubernetes de forma local y liviana.

---

## 🧩 1. ¿Qué son y para qué sirven?

| Herramienta | Propósito | Instalación requerida |
|--------------|------------|------------------------|
| **kubectl** | Cliente oficial de Kubernetes. Permite interactuar con el clúster (aplicar *manifests*, ver *pods*, consultar *logs*, etc.). | ✅ Sí, manual |
| **Kind** | Herramienta que permite ejecutar clústeres de Kubernetes dentro de contenedores Docker. Ideal para entornos de desarrollo y pruebas. | ✅ Sí, manual |
| **Docker** | Motor de contenedores necesario para que Kind cree los nodos del clúster. | ✅ Sí, manual (o desde Docker Desktop) |

---

## ⚙️ 2. Instalación paso a paso

A continuación, se describen los pasos para preparar tu entorno en **WSL (Ubuntu)**.

### 🔹 Requisitos previos

1. **Tener instalado WSL2 con una distribución Ubuntu.**  

   - 👉 Puedes verificarlo en `PowerShell`, `CMD` o `Git Bash`:
   ```bash
   wsl -l -v
   ```
   - > ✍️ **Importante:** Asegúrate de que tu distribución tenga **versión 2**.

   - 📄 [Configurar Linux-WSL2 en Windows](https://github.com/tejada1970/guias-desarrollo/blob/master/configuraciones/windows/configurar-linux-wsl2-en-windows.md)



2. **Tener Docker disponible:**

   - O bien instalando **Docker Desktop** para Windows (que expone el socket a WSL).
   - O instalando **Docker Engine** directamente dentro de Ubuntu.

   **Verifica que Docker funcione correctamente:**
   ```bash
   docker version
   ```

   - 📄 [Instalar Docker Desktop con WSL2 en Windows](https://github.com/tejada1970/guias-desarrollo/blob/master/requisitos/windows/instalar-docker-desktop-wsl2-en-windows.md)

---

### 🧱 Instalar kubectl

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

> ✍️ **Notas:**
> - `/usr/local/bin` es una ruta incluida en el `PATH` del sistema, por eso puedes ejecutar `kubectl` desde cualquier directorio.
> - Si prefieres instalarlo en otra ruta, asegúrate de agregarla al `PATH` en tu `~/.bashrc` o `~/.zshrc`.

---

### 🧩 Instalar Kind

```bash
# Descargar el binario de Kind (última versión estable)
curl -Lo ./kind https://kind.sigs.k8s.io/dl/$(curl -Ls https://kind.sigs.k8s.io/dl/latest.txt)/kind-linux-amd64

# Dar permisos de ejecución
chmod +x ./kind

# Moverlo a una ruta global
sudo mv ./kind /usr/local/bin/kind

# Verificar instalación
kind version
```

---

### 🚀 Crear un clúster local con Kind (para prueba)

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

## 🧰 Recursos útiles

- 📘 [Documentación oficial de Kind](https://kind.sigs.k8s.io/)
- 📗 [Documentación oficial de kubectl](https://kubernetes.io/docs/reference/kubectl/)
- 🐳 [Instalar Docker en WSL2](https://docs.docker.com/desktop/wsl/)

---

## ✅ Resultado esperado

Una vez completados los pasos:

- Tienes **Docker**, **Kind** y **kubectl** instalados.
- Puedes levantar un clúster local con `kind create cluster`.
- Puedes gestionarlo con `kubectl`.

---

**Fin del documento**
