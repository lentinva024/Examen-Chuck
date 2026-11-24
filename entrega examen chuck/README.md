# Entrega Examen - Valentín Lago Valdez

**Alumno:** Valentín Lago Valdez

---

### Pasos realizados y capturas:

**1. Escaneo de la red**
* **Imagen:** `Advanced ip scanner maquina 192.168.111.55.png`
* Primero usé **Advanced IP Scanner** para buscar qué máquinas estaban activas en la red y así encontré la IP de la máquina vulnerable que es la **192.168.111.55**.

**2. Revisión del tráfico en Wireshark**
* **Imagen:** `tcp wireshark con conversacion.png`
* Abrí el archivo `.pcapng` en **Wireshark** y me fui a la parte de conversaciones TCP para ver qué conexiones había y qué IPs estaban comunicándose.

**3. Análisis de las sesiones FTP**
* **Imagen:** `scanner tcp wireshark con conversacion2.png`
* Le di a seguir el flujo TCP (**Follow TCP Stream**) de la sesión FTP y pude ver los comandos que se habían ejecutado, como los inicios de sesión y las carpetas por las que se movían.

**4. Obtención de las contraseñas y usuarios**
* **Imagen:** `EncontrarArchivocontraseñas.png`
* Al revisar los paquetes de datos (`ftp-data`), encontré que se habían subido los archivos `usuarios.txt` y `password.txt`. De ahí saqué las listas para poder usarlas después.

**5. Ataque de fuerza bruta con Hydra**
* **Imagen:** `Crackeo hidra comando.png`
* Como el puerto SSH estaba abierto y sabía que el usuario era **aladar**, preparé el comando en **Hydra** usando el diccionario `password.txt`:
```bash
hydra -I -l aladar -P password.txt ssh://192.168.111.55 -t 4 -f -vV
```

**6. Acceso SSH y creación de la flag**
* **Imagen:** `Crackeo hidra resolucion, conexion ssh y creacion del touch.png`
* Hydra sacó la contraseña correcta, me conecté por **SSH** con `ssh aladar@192.168.111.55`, metí la clave y una vez dentro creé la flag con el comando:
```bash
touch Valentin
```

