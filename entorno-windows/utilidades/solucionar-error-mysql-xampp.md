# 📚 Guía: solucionar-error-mysql-xampp

Esta guía te ayudará a solucionar el error de arranque de MySQL en XAMPP cuando el servicio no inicia correctamente debido a corrupción en los archivos de InnoDB.

---

## 🔎 Qué significa el error

Al intentar iniciar MySQL desde el panel de XAMPP, puede aparecer un mensaje como:

```
12:51:14  [mysql]   Error: MySQL shutdown unexpectedly.
12:51:14  [mysql]   This may be due to a blocked port, missing dependencies, 
12:51:14  [mysql]   improper privileges, a crash, or a shutdown by another method.
12:51:14  [mysql]   Press the Logs button to view error logs and check
12:51:14  [mysql]   the Windows Event Viewer for more clues
12:51:14  [mysql]   If you need more help, copy and post this
12:51:14  [mysql]   entire log window on the forums
```

---

## ✅ Resumen de la solución

1. Cierra el panel de XAMPP y accede a: `xampp/mysql/`  
2. Renombra la carpeta `data/` a `data_old/`  
3. Haz una copia de la carpeta `backup/` → renómbrala a `data/`  
4. Copia todas las carpetas de `data_old/` a la nueva `data/` **excepto** `mysql`, `performance_schema` y `phpmyadmin`  
5. Copia el archivo `data_old/ibdata1` a la carpeta `data/`  
6. Cierra el panel de XAMPP y finaliza los procesos en segundo plano (`xampp-control.exe`)  
7. Abre el panel de XAMPP como administrador e inicia Apache y MySQL

---

## ✅ Paso a paso detallado

1. **Cerrar el panel de XAMPP y acceder a:** `xampp/mysql/`  

2. **Renombrar la carpeta:** `data/` → `data_old/`  
   - Esto guarda los datos actuales como respaldo.

3. **Hacer una copia de la carpeta `backup/` → renombrarla a `data/`**  
   - XAMPP trae un MySQL limpio y funcional.

4. **Copiar todas las carpetas de `data_old/` a la nueva `data/` excepto:** `mysql`, `performance_schema` y `phpmyadmin`  
   - Trae solo las bases de datos de usuario.

5. **Copiar el archivo `ibdata1` de `data_old/` a la nueva `data/`**  
   - Contiene datos de InnoDB y metadatos de tablas.

6. **Cerrar XAMPP y procesos de MySQL**  
   - En la barra inferior haz click derecho y pincha en "Administrador de tareas" para acceder a los procesos". Busca y haz click derecho en los procesos que esten corriendo `xampp-control.exe` y pincha en "finalizar tarea" para detener el proceso en cada uno de ellos.

7. **Abrir el panel de XAMPP como administrador e iniciar Apache y MySQL**  
   - Ahora MySQL debería arrancar correctamente.

---

## ✅ Por qué esto funciona

El error:

```
Missing MLOG_CHECKPOINT … Plugin initialization aborted
```

se debe a corrupción en los archivos de InnoDB.  
Al reemplazar la carpeta `data/` por un backup limpio y luego traer solo tus bases de datos + `ibdata1`, recuperas tus datos en un entorno de InnoDB limpio evitando la corrupción de los archivos del sistema.

---

*Fin del documento*
