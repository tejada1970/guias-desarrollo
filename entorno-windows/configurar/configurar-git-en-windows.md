# 📚 Guía: configurar-git-en-windows

Esta guía, detalla los pasos para configurar **Git** por primera vez en **Windows**.

---

## ⚙️ Pasos para la configuración

> 💻 Abre la terminal **Git Bash** (búscalo en el menú de inicio) y ejecuta las siguientes configuraciones:

### 🧑‍ Configuración global de nombre de usuario y correo electrónico

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tucorreo@example.com"
```

### 🖊️ Configurar el editor por defecto (Visual Studio Code)

```bash
git config --global core.editor "code --wait"
```

### 🌈 Activar colores en la salida del terminal

```bash
git config --global color.ui true
```

### 🧱 Configuración de fin de línea (`core.autocrlf`)

El manejo de saltos de línea puede variar entre sistemas operativos:

* En **Windows**, se usan `\r\n` (retorno de carro y salto de línea).
* En **Linux/macOS**, solo se usa `\n`.

Para evitar problemas de compatibilidad al clonar, subir o colaborar en proyectos entre sistemas diferentes, ajusta la conversión automática de saltos de línea:

#### En **Windows**:

```bash
git config --global core.autocrlf true
```

#### En **Linux/macOS**:

```bash
git config --global core.autocrlf input
```

---

## 💡 Resultado

Con esto, **Git** quedará correctamente instalado y configurado para trabajar en cualquier entorno de desarrollo multiplataforma.

---

## 🛠️ Consejos y buenas prácticas

> ✅ Aunque la opción `core.autocrlf` ayuda en tu entorno local, la mejor práctica es incluir un archivo `.gitattributes` en cada proyecto. Te recomiendo consultar esta guía:

- 📖 [consejo-uso-de-gitattributes-en-proyectos](https://github.com/tejada1970/guias-desarrollo/blob/master/entorno-windows/consejos/consejo-uso-de-gitattributes-en-proyectos.md)

---

*Fin del documento*
