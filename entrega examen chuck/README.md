# Entrega Examen - Valentín Lago Valdez

**Alumno:** Valentín Lago Valdez


### Pasos realizados y capturas:

**1. Escaneo de la red**
Primero usé **Advanced IP Scanner** para buscar qué máquinas estaban activas en la red y así encontré la IP de la máquina vulnerable que es la **192.168.111.55**.

![Escaneo de red](Advanced%20ip%20scanner%20maquina%20192.168.111.55.png)

---

**2. Revisión del tráfico en Wireshark**
Abrí el archivo `.pcapng` en **Wireshark** y me fui a la parte de conversaciones TCP para ver qué conexiones había y qué IPs estaban comunicándose.

![Conversaciones TCP](tcp%20wireshark%20con%20conversacion.png)

---

**3. Análisis de las sesiones FTP**
Le di a seguir el flujo TCP (**Follow TCP Stream**) de la sesión FTP y pude ver los comandos que se habían ejecutado, como los inicios de sesión y las carpetas por las que se movían.

![Flujo FTP](scanner%20tcp%20wireshark%20con%20conversacion2.png)


**4. Obtención de las contraseñas y usuarios**
Al revisar los paquetes de datos (`ftp-data`), encontré que se habían subido los archivos `usuarios.txt` y `password.txt`. De ahí saqué las listas para poder usarlas después.

![Extracción de contraseñas](EncontrarArchivocontrase%C3%B1as.png)

---

**5. Ataque de fuerza bruta con Hydra**
Como el puerto SSH estaba abierto y sabía que el usuario era **aladar**, preparé el comando en **Hydra** usando el diccionario `password.txt`:
```bash
hydra -I -l aladar -P password.txt ssh://192.168.111.55 -t 4 -f -vV
```

![Comando Hydra](Crackeo%20hidra%20comando.png)

---

**6. Acceso SSH y creación de la flag**
Hydra sacó la contraseña correcta, me conecté por **SSH** con `ssh aladar@192.168.111.55`, metí la clave y una vez dentro creé la flag con el comando:
```bash
touch Valentin
```

![SSH y Flag](Crackeo%20hidra%20resolucion,%20conexion%20ssh%20y%20creacion%20del%20touch.png)

