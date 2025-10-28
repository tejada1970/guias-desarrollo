# 📚 Guía: configurar-linux-wsl2-en-windows

Esta guía detalla los pasos para habilitar **WSL2** y configurar **Ubuntu** dentro de Windows 11.  
WSL2 (Windows Subsystem for Linux 2) te permite usar un sistema Linux dentro de Windows, sin necesidad de una máquina virtual pesada.  
Es ideal para desarrollo porque **Laravel, Docker y muchas herramientas funcionan mejor en Linux que en Windows puro**.

---

## ⚙️ Pasos para la configuración

### 1. Habilitar las características necesarias en Windows

#### 1.1 Habilitar funciones opcionales

En **Windows 11 Home**, **Hyper-V** no aparece en las características opcionales, aunque la virtualización esté habilitada.  
En **Windows 11 Pro / Enterprise / Education**, sí deberías ver Hyper-V en la ventana de *Activar o desactivar características de Windows*.

1. Haz clic en **Inicio** y busca:  
   👉 `Activar o desactivar las características de Windows`  
   👉 O escribe en la búsqueda: **características de windows**

2. En la ventana que se abre, marca estas opciones:  
   ✅ **Plataforma de máquina virtual** (Virtual Machine Platform)  
   ✅ **Subsistema de Windows para Linux** (Windows Subsystem for Linux)

3. Haz clic en **Aceptar** y deja que Windows instale los componentes.  

4. Reinicia tu PC.

---

#### 1.2 Verificar si la virtualización está habilitada

1. Abre el **Administrador de tareas** con `Ctrl + Shift + Esc`.  
2. Haz clic en la pestaña **Rendimiento**.  
3. En el menú de la izquierda selecciona **CPU**.  
4. A la derecha, debajo del gráfico, busca la línea:  

👉 **Virtualización: Habilitada / Deshabilitada** ✅  

---

### 2. Instalar WSL2 desde PowerShell

1. Abre **PowerShell como Administrador** (clic derecho en Inicio → *Terminal (Administrador)*).  
2. Ejecuta:  

```powershell
wsl --install
```

Esto hará tres cosas:  
- Instalará WSL2.  
- Configurará Ubuntu como tu distribución por defecto.  
- Descargar e instalará Ubuntu automáticamente.  

👉 Cuando termine, reinicia tu PC si lo pide.

---

### 3. Primer arranque de Ubuntu (Linux dentro de Windows)

1. Después de reiniciar, abre el menú **Inicio** y busca **Ubuntu**.  
2. La primera vez que lo abras:  
   - Te pedirá crear un usuario de Linux y una contraseña.  
   - Este usuario es independiente de tu usuario de Windows.  

👉 A partir de ahora, cada vez que quieras entrar en tu entorno Linux, abre **Ubuntu** desde el menú Inicio o ejecuta `wsl` en PowerShell.

---

### 4. Verificar que estás usando WSL2

En **PowerShell** (no en Ubuntu), ejecuta:  

```powershell
wsl -l -v
```

Deberías ver algo como:  

```
  NAME      STATE     VERSION
* Ubuntu    Running   2
```

👉 Si aparece **VERSION 1**, cámbialo a WSL2 con:  

```powershell
wsl --set-version Ubuntu 2
```

---

### 5. Actualizar paquetes en Ubuntu

Dentro de la terminal de **Ubuntu**, actualiza todo con:  

```bash
sudo apt update && sudo apt upgrade -y
```

👉 Esto dejará tu entorno Linux al día.

---

### 6. (Opcional) Establecer Ubuntu como predeterminado

Si planeas usar siempre Ubuntu en WSL, configúralo como distro por defecto:  

```powershell
wsl --set-default Ubuntu
```

---

## ✅ Resumen

Con estos pasos ya tienes:  

- WSL2 habilitado en Windows 11.  
- Ubuntu instalado y listo.  
- Entorno Linux preparado para instalar **Docker, Composer, Node**, etc.  

---

*Fin del documento*
