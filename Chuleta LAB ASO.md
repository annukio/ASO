---
created: 2024-12-07T15:09
updated: 2024-12-15T13:46
---
# Comandos utilizados en las prácticas de laboratorio

- `sudo su`: *Entra en modo superusuario*
- `lspci`: *Lis todos los dispositivos PCI conectados al sistema.*
	- `-v / -vv`: *Muestra información detallada de cada dispositivo (vv más detallada)*
	- `-k`: *Indica que controladores de kernel están manejando cada dispositivo.*
	- `-nn` *Muestra IDs + Nombres de cada dispositivo*
	- `-s <bus:slot.func>`: *Filtra y muestra información solo para el dispositivo especificado por el bus, slot y función* -> `lspci -s 00:1f.2`.
	
- `lsusb`: *Lista todos los dispositivos conectados al bus USB*
	- `-v / -vv`: *Muestra información detallada de cada dispositivo (vv más detallada)*
	- `-t`: *Presenta los dispositivos en una estructura de árbol, mostrando la jerarquía de puertos*.
	- `-s <bus:slot.func>`: *Filtra y muestra información solo para el dispositivo especificado por el bus, slot y función* -> `lsusb -s 00:1f.2`
	- `-D <device>`: *Muestra información detallada para el dispositivo USB especificado*.
- `dmesg`: *Muestra lo mensajes del búfer de anillos del kernel*.
- `mount`: *Se utiliza para montar sistemas de archivos.* -> `mount [opciones] dispositivo punto_de_montaje`
	- `-t <tipo>`: *Especifica el tipo de sistema de archivos (ext4)*
	- `-o <opciones>`: 
		- `-ro`: *Montar como read only*
		- `-rw`: *Montar con permisos de escritura y lectura*
		- `uid`: *Establece el usuario propietario*
	- -U: Monta por UUID del dispositivo
	- `-B`: *Hace un "bind mount" que significa montar un directorio en otro lugar manteniendo el mismo contenido*
- `gdisk`: *Herramienta de particionamiento en Linux que se utiliza para trabajar con tablas de partición en formato GPT* -> `sudo gisk <dispositivo>`*Al ejecutarse se entra en un modo interactivo: (Se pueden crear hasta 128 particiones sin ninguna restricción)
	- `?`: Muestra una lista de todos los comandos posibles
	- `p`: Muestra la tabla de particiones actual
	- `n`: Crea una nueva partición
	- `d`: Crea una nueva partición
	- `t`: Cambia el tipo de partición
	- `w`: Escribe los cambios en el disco y sale del programa
	- `q`: Sale del programa **sin guardar**
	- `x`: Entra en el modo experto donde se puede 
		- Cambiar tamaño encabezado GPT
		- Reparar tablas de partición corruptas
- `partprobe:` *Recarga la tabla de particiones.*
- `mkfs`:  *Crea un sistema de archivos (define cómo se organizan y almacenan los datos en una partición*.  
	- `mkfs -t <fstype> <dispositivo>`
		- `-t`: 
		- `fstype`: ext4 (predeterminado para linux) , btrfs, vfat (para el USB `/dev/usb1` según el enunciado),etc.
- `mkswap`: *Prepara la partición para que el sistema operativo la reconozca como espacio de intercambio*.
- `chroot`: *cambia el directorio raiz aparente para un proceso y sus hijos creando un entorno aislado donde ese proceso solo tiene acceso a su nuevo directorio raíz.*
- `passwd`: *Cambia la contraseña del usuario*
- `tune2fs`: *Permite ajustar y modificar los parámetros de sistemas de archivos ext2, ext3 y ext4* -> `tune2fs [opciones] <dispositivo>`
	- `-L`: *Cambia o establece una etiqueta para identificar el sistema de archivos: `tune2fs -L "Miparticion" /dev/sda1`
	- `-i`: *Establece el tiempo máximo entre dos verificaciones automáticas por fsck, Formatos: d(días), w(semanas), m (meses)*.
- `grep`: *Busca texto dentro de archivos o salidas de otros comandos*.
	- `-r`: *Busca recursivamente en subdirectorios*.
	- `-i`: *Ignora mayúsculas y minúsculas.*
	- `-n`: *Muestra el número de línea donde aparece el patrón.*
	- `-v`: *Muestra las líneas que no coinciden*
	- `--color`: *Resalta las coincidencias encontradas.*
- `auto <ethernet IF>:` *Indica que la interfaz se configure automáticamente al iniciar el sistema* -> `auto eth0*
- `iface <ethernet IF> inet static:` *Define la configuración de la interfaz como estática (IP fija)* -> `iface eth0 inet static`
- `address <dirección IP>` : *Especifica la dirección IP asignada a la interfaz* -> `address 10.10.41.50`
- `network 10.10.41.0:` *Define la dirección de red asociada a la interfaz* -> `network 10.10.41.0`
- `netmask <mask>` *Establece la máscara de subred para la interfaz* -> `netmask 255.255.255.0`
- `gateway <direccion IP>:` *Define la puerta de enlace predeterminada para la interfaz* -> `gateway 10.10.41.1`.
- `apt update`:*Descarga la info más reciente de los paquetes disponibles desde los repositorios.*
- `apt install <paquete>`: *instala uno o más archivos del repositorio*
- `sftp username@hostname`: *Te conectas a un servidor sftp*
	- `mget file_pattern`: *Dentro de sftp permite descargarte más de un archivo a la vez.*
- `ls`: *Lista los directorios hijos de un directorio padre.*
	- `-la` Lista también los archivos ocultos.
- `tar`: *Herramienta para agrupar múltiples archivos en un único archivo (no comprimido por defecto). Combinado con opciones como `-z` o `-j`, soporta compresión gzip o bzip2 respectivamente.*
- `ln`: *Comando para crear enlaces entre archivos. Los enlaces simbólicos (`-s`) apuntan a la ubicación del archivo original, mientras que los hard links son duplicados referenciales en el sistema de archivos.*
- `df -h I grep /carpeta`: *Comprueba que la partición está montada en /carpeta.*
- `echo`: *Imprime por la salida un mensaje.*
- `touch`: *Modifica el acceso del archivo y modifica sus tiempos de última vez editado. Si no existe el archivo, lo crea.*
- `mv` : *Mueve un archivo de un directorio a otro/Lo renombra `mv /root /root.old`*
- `passwd`: *Cambia la contraseña de un usuario.*
- `swapoff:` *Desactiva una partición de intercambio.*
- shutdown 0: *Apaga el sistema inmediatamente.*
- `tune2fs:` *Ajusta parámetros del FS ext2/ext3/ext4.*
	- -i <intervalo: Cambia el intervalo de chequeo del filesystem (ej: `tune2fs -i 28 /dev/sda2`).
- `grep:` *Busca texto dentro de archivos.* (Ej: `grep -r "Debian GNU/Linux 11" /etc`)
- `ip link, ip addr, ip route`: *Comandos para configurar y mostrar información de interfaz de red, direcciones IP y rutas.* 
		(ej: `ip addr add`, `ip route add default via ...`, `ip link set dev eth0 up`).	
- `ifup / ifdown:` *Activa o desactiva interfaces de red definidas en `/etc/network/interfaces`.*
- `sftp usuario@servidor:` *Conexión a servidor SFTP.*
- `ls:` *Lista archivos/directorios en el servidor remoto*.  
- `get <archivo>`: *Descarga un archivo.*
- `mget <patrón>`: *Descarga múltiples archivos que coincidan con un patrón.*
- `dpkg:` *Gestor de paquetes base de Debian.*  
	- --install paquete.deb: Instala un paquete .deb.  
	- -r: Desinstala dejando configuración.  
	- -P (purge): Desinstala borrando configuración.
- `apt update:` *Actualiza la información de paquetes disponibles.*
- `apt install <paquete>`: *Instala paquetes desde el repositorio.* 
- `apt upgrade:` *Actualiza los paquetes instalados a sus últimas versiones.*
- `apt info <paquete>:` *Muestra info de un paquete.*
- `apt search <patrón>:` *Busca paquetes.*  
- `apt clean:` *Limpia la caché de paquetes descargados.*
- `dpkg-reconfigure:` *Reconfigura un paquete ya instalado.*
- `make`: *Compila el código fuente según las directrices del Makefile.* 
- `make install:` *Instala los binarios compilados en las ubicaciones finales del sistema.*
- `make clean`: *Elimina archivos temporales de compilación.*
- `make uninstall`: *Desinstala lo instalado previamente (si el Makefile lo soporta).*
# Guia Vi

## Modos VI

### Command mode:

> Modo utilizado para ejecutar comandos como guardar archivos, ejecutar comandos, mover el cursor, cortar (**yank**), pegar lineas o palabras, buscar/reemplazar. Todo lo escrito se interpreta como un comando.

### Insert Mode:

> Modo que permite insertar texto en el archivo, para entrar **pulsar i** desde el modo de **comando**.


>💡**PULSAR "ESC" DOS VECES PARA IR AL MODO COMANDO**


## Comandos VI

- **SALIR DE VI**:  `:q` *Sale de VI siempre y cuando no haya cambios realizados, en caso de haber hecho algun cambio te dará una advertencia*

- **SALIR DE VI SIN GUARDAR:** `:q!`: *Sale de VI sin guardar aunque hayas hecho algun cambio*

- **SALIR Y GUARDAR:** `ZZ`: // `:wq`: *Sale y guarda el archivo*

- **GUARDAR:** `:w`: *Guarda el archivo*

- **COPIAR:** `yy`: *Copia la linea actual*

- **PEGAR:** 
	- `p`: *Pega la linea copiada a partir de la posición del cursor*.
	- `P`: *Pega la linea copiada antes del cursor*.


- **BORRAR**: 
	- `x`: *Borra el caracter donde apunta el cursor (supr).*
	- `X`: *Borra el caracter anterior al cursor (backspace).*
	- `dw`: *Borra desde el cursor hasta el final de la palabra.*
	- `d^`: *Borra desde el principio de la linea hasta la posición del cursor.*
	- `d$`: *Borra desde la posición del cursor hasta el final de la linea.*
	- `dd`: *Borra toda la línea en la que se encuentra el cursor.*
- **BÚSQUEDA DE PALABRAS Y CARÁCTERES**
	- `/`: *Busca hacia abajo del archivo*
	- `?`: *Busca hacia arriba en el archivo*


# Guía Systemd and systemctl


### El proceso init y la evolución hacia systemd

El proceso **init** es el primer proceso que se inicia en sistemas Unix (PID=1) y permanece activo hasta el apagado del sistema. Su rol es arrancar los demonios y servicios de usuario, montar sistemas de archivos, gestionar hardware, etc. Históricamente, existían dos grandes enfoques para el init:

- **BSD-style**: basado en scripts en `/etc/rc/`
- **System V (SysVinit)**: basado en "runlevels"

Ambos tenían como inconveniente el arranque secuencial y, por ende, mayor lentitud.

Nuevas alternativas surgieron para reemplazar estos sistemas, siendo **systemd** la más adoptada en diversas distribuciones Linux (pese a ciertas críticas). Esta herramienta proporciona un arranque paralelo y una gestión centralizada de servicios y unidades, mejorando rendimiento y flexibilidad.

### systemctl y su interacción con systemd

`systemctl` es el comando principal para interactuar con `systemd`. Permite listar, iniciar, detener, reiniciar y configurar servicios, además de gestionar sockets, puntos de montaje y más. La autocompletación (TAB) ayuda a descubrir sus opciones.

### Conceptos clave de systemd

- **Units (Unidades)**: Son recursos manejados por systemd: servicios (ej. `ssh.service`), sockets, puntos de montaje (`.mount`), temporizadores (`.timer`), etc. Existen 11 tipos de unidades.
- **Unit files**: Cada unidad se describe mediante un archivo de configuración de texto plano, cuyo nombre refleja el tipo de la unidad (ej. `nginx.service`, `boot.mount`). Se organizan en secciones (`[Unit]`, `[Install]`, `[Service]`, ...), con directivas clave-valor.
- **Estado de las unidades**: Al arrancar, las unidades se cargan en memoria y muchas quedan activas, esperando eventos (ej. conexión de un dispositivo, apertura de un socket) que disparen acciones del demonio correspondiente.
- **Dependencias**: Las unidades pueden requerir otras unidades, especificándose con directivas como `Wants`, `Requires`, `After`, `Before` en la sección `[Unit]` del archivo de la unidad.

### Operaciones básicas con systemctl

- **Listar unidades**:
  - `systemctl list-units`: lista unidades cargadas y activas.
  - `systemctl list-units --all`: incluye también las inactivas.
  - `systemctl list-units --type <tipo>`: filtra por tipo (ej. `service`).
  - `systemctl list-units --failed`: muestra unidades en estado fallido.

- **Obtener información de una unidad**:
  - `systemctl status <unidad>`: estado y últimos mensajes del log.
  - `systemctl cat <unidad>`: muestra el archivo de unidad.
  - `systemctl list-dependencies <unidad>`: árbol de dependencias.
  - `systemctl show <unidad>`: propiedades detalladas.

- **Controlar el estado de las unidades**:
  - `systemctl stop <unidad>`: desactiva inmediatamente la unidad.
  - `systemctl start <unidad>`: activa inmediatamente la unidad.
  - `systemctl restart <unidad>`: reinicia la unidad.
  - `systemctl enable <unidad>`: la unidad se activará en el próximo arranque.
  - `systemctl disable <unidad>`: la unidad no se activará en el siguiente arranque.

- **Editar configuración**:
  - `systemctl edit <unidad>`: abre el archivo de la unidad en un editor (determinado por `SYSTEMD_EDITOR`, `EDITOR` o `VISUAL`, o por defecto nano/vim/vi).

### Ecosistema systemd

- **Journald y journalctl**:  
  - `systemd-journald.service` es el daemon del journal.
  - `journalctl` permite consultar el log. Ejemplos:
    - `journalctl --since "1 hr ago"`: últimos mensajes de la última hora.
    - `journalctl -n N`: últimas N entradas.
    - `journalctl --disk-usage`: uso en disco del journal.
    - `journalctl -u <unidad>`: filtra por una unidad específica.

- **Otros servicios**:
  - `systemd-logind.service`: gestiona sesiones de login.
  - `systemd-networkd.service`: gestiona la configuración de red.
  - `systemd-halt.service`, `systemd-poweroff.service`, `systemd-reboot.service`, etc.: gestionan apagado y reinicio del sistema.

### Operaciones avanzadas

- **systemd --user**: Permite a usuarios crear su propia instancia systemd para gestionar servicios personales.
- **Unidades enmascaradas (masked)**: Una unidad enmascarada no puede ser iniciada ni habilitada hasta ser desenmascarada.
- **Conexión remota**: `systemctl --host=nombre_host` permite interactuar con systemd de otra máquina.
- **Estados detallados**: `systemctl --state=help` enumera todos los estados y sub-estados posibles.

  
# Command Reference

![[Pasted image 20241207183121.png]]

---
# Práctica 1 Installation of the OS

### Descripción de la práctica
1. Identificamos los componentes hardware del sistema:
	- `lspci`: Lista todos los dispositivos que están conectados al bus PCI.
	- `lsusb`: Lista todos los dispositivos conectados al bus USB.
	![[Pasted image 20241207190557.png]]
2. Terminamos de rellenar la tabla de arriba usando el comando `dmesg`, recordando que **los dispositivos normalmente están almacendos en el directorio /dev .
3. Si tienes un sistema con dos discos NVMe y un disco SATA:	
	3.1 **Primer NVMe:**
		• Controlador: /dev/nvme0
		• Namespace: /dev/nvme0n1
		• Primera partición: /dev/nvme0n1p1
	3.2. **Segundo NVMe:**
		• Controlador: /dev/nvme1
		• Namespace: /dev/nvme1n1
		• Primera partición: /dev/nvme1n1p1
	3.3 **SATA:**
		• Primer disco SATA: /dev/sda

4. El primer paso para instalar el sistema es particionar el disco en el dispositivo USB. (/dev/sda)y para ello desmontamo previmente todos los dispositivos usb
	- `umount /dev/usb`
5. Nos movemos al /dev y ejecutamos:
	- `sudo gdisk /dev/sda`.
6. Creamos las siguientes particiones usando los comandos de gdisk correspondientes.
	![[Pasted image 20241207201201.png]]

7. Una vez hemos creado las particiones necesarias, empezamos inicializando el área swap (doble de la RAM) (tampoco es obligatorio)
	- `mkswap device`
8. Seguidamente creamos el sistema de archivos (define cómo se orgnaizan y almacenan los datos en una partición, sin éste no podría ni guardar ni leer datos en una partición).
		
```bash
# Formatear las particiones
mkfs.vfat /dev/usb1             # Formatear /boot/efi como vfat
mkfs.ext4 /dev/usb2             # Formatear / como ext4
mkfs.ext4 /dev/usb3             # Formatear /usr/local como ext4
mkfs.ext4 /dev/usb4             # Formatear /home como ext4
mkswap /dev/usb5                # Configurar el swap
swapon /dev/usb5                # Activar el swap
mkfs.ext4 /dev/usb6             # Formatear la partición reservada como ext4

# Crear directorio principal para montaje
mkdir /linux

# Montar las particiones
mount /dev/usb2 /linux                  # Montar /
mkdir -p /linux/boot/efi
mount /dev/usb1 /linux/boot/efi         # Montar /boot/efi
mkdir -p /linux/usr/local
mount /dev/usb3 /linux/usr/local        # Montar /usr/local
mkdir -p /linux/home
mount /dev/usb4 /linux/home             # Montar /home
```

> Es importante crear los directorios después de montar el /linux pero antes de montar el resto.


9. Instalaremos el sistema base que se encuentra en un servidor SFTP de la siguiente forma:
	```bash
cd /linux
sftp aso@asoserver.pc.ac.upc.edu
#Ponemos la password AsORoCkSHaRd!
get aso-install.tar.gz
exit
tar xzf aso-install.tar.gz
rm aso-install.tar.gz
	```

10. Terminamos de montar los sistemas auxiliares
```bash
for i in /dev /dev/pts /proc /sys /run; do
	mount -B $i /linux/$i
done
```

> Este script toma algunos directorios clave del sistema (que son necesarios para que el sistema operativo funcione correctamente, como /dev y /proc) y los “clona” en otro directorio (en este caso /linux). Esto se hace para que, cuando estés dentro del entorno de /linux, sigas teniendo acceso a estos sistemas esenciales.

11. Ahora pasamos a configurar la tabla sistemas de archivos (/etc/fstab)
```bash
vim /linux/etc/fstab
device(/dev/usb5 en caso del ejemplo) none swap defaults 0 0 #Añadir la partición swap
device / ext4 defaults 0 1 # Añadir la partición de root
device /boot/efi cf
```

> Primer número: **DUMP** (0/1) si debe realizar una copia de seguridad con dump. Casi siempre 0.
> Segundo número: (fsck): 1 se verifica al inicio (Normalmente root /), 2 Verificación en otras particiones (después de la raiz).

`/proc y /sys` no tienen dispositivos adjuntos porque son sistemas de archivos virtuales diseñados para dar información sobre el sistema y el kernel en lugar de interactuar directamente con hardware físico tal y como lo harían los archivos de dispositivos en /dev.
12. Cambiamos el directorio root del sistema y usamos temporalmente el software instalado en el sistema en vez del disponible en el sistema:
		`chroot /linux`

> El comando chroot cambia el directorio raiz aparente para un proceso y sus hijos creando un entorno aislado donde ese proceso solo tiene acceso a su nuevo directorio raíz.

13. Configuramos el teclado:
```
dpkg-reconfigure locales
dpkg-reconfigure console-data
dpkg-reconfigure keyboard-configuration
```

14. Para evitar tener que modificar la tabla de particiones cada vez que encendemos un ordenador, usaremos un *bootloader*, un set de programas residentes en el disco duro que permiten al usuario cargar otros sistemas operativos, instalaremos GRUB:
 
	 `grub-install --target=x86_64-efi /dev/usb`

> Asumiendo que la ya hemos realizado estos comandos previamente:

```bash
mount /dev/usb2 /linux
mount /dev/usb1 /linux/boot/efi
```

Para no tener que editar el archivo `/boot/grub/grub.cfg` ejecutamos `update-grub`que crea automáticamente este archivo.

15. Ahora cambiaremos las contraseñas que como ya sabemos se enecuentran en el archivo `/etc/passwd` con el comando: `passwd`
16. Desmontamos todo lo que hemos montado antes, en caso de no saber que particiones están montadas actualmente se puede utilizar el comando:
		`mount | grep linux`

	>**IMPORTANTE**: Desmontar en orden inverso al que se ha montado:

```
umount /linux/boot/efi
umount /linux/usr/local
umount /linux/home

umount /linux

# Y si quieres desactivar swap:
swapoff /dev/usb5 #Suponiendo que esta en usb5
sudo shutdown 0
```

17. Ahora nos encargaremos de la **Post-Configuración**. Para ello empezamos dandole a la tecla F12 para ir al menú de BOOT de la BIOS, seleccionamos *Toshiba harddrive from the UEFI boot partition* y no la Legacy, ya que no hemos configurado con mecanismo MBR y si todo ha funcionado correctamente deberíamos tener dos cuentas de usuario, root y aso. Para cambiar a superusuario como aún no tenemos `sudo` instalado podemos hacerlos ejecutando `su`.
18. Cambiamos la frecuencia de checks del filesystem en el usb2 a 28 días.
	`tune2fs -i 28 /dev/sda2`

> Con tune2fs también podemos cambiar el porcentaje de bloques reservados (modificar el espacio reservado para el superusuario (-m). 

19. Hay varios mensajes que aparecen durante el proceso de login del sistema, queremos cambiar alguno de ellos. Todos están localizados en /etc. Queremos cambiar el mensaje que dice algo parecido a "Debian GNU/Linux 11". Para encontrarlo usamos el comando:
	`grep -r "Debian GNU/Linux 11" /etc

> Y encontramos que el archivo es /etc/issue.

20. Modificamos el MOTD (Message of the day) modificando el `/etc/motd`

21. Pasamos a configurar la red, se puede hacer via **manual** o **automática**:
	**Manual:**
		Hacemos Flush de la conexión actual asegurarnos que que está activo.
```bash
ip link show #
ip link set dev <ethernet IF> down
ip link set dev <ethernet IF> up
```

The commands for configuring the IP_address and his default route is:
```bash
sudo ip addr add <IP_address> / <netmask> dev <interface>\
ip link set dev eno1 up
ip route add default via 10.10.41.1
```

Y justo después creamos el archivo /etc/resolv.conf con la información DNS.

> De esta forma tendríamos que configurarlo cada vez que encendemos el ordenador. Para evitar esto lo configuraremos para que se configure automáticamente al momento de iniciar.

**Automática:**
```bash
vim /etc/network/interfaces
auto <ethernet IF>
iface <ethernet IF> inet static
address 10.10.41.??? # (ip que te da el profesor)
network 10.10.41.0
netmask 255.255.255.0
gateway 10.10.41.1

ifup <ethernet IF>
ifdown <ehternet IF> # Para comprobar si se han configurado correctamente
```

**Con DHCP:**
```bash
vim /etc/network/interfaces
auto <ethernet IF>
iface <ethernet IF> inet dhcp
```

---
# Práctica 2 Application Management

#### Resumen rápido preguntas del principio:
- Para conectarse a un sever sftp usamos: `sftp username@hostname`
- Dentro de **sftp**:
	- ls: Lista directorios
	- get: Obtiene un archivo de un directorio.
	- mget file_pattern: Obtiene muchos archivos de un directorio.
- Para comprimir: `tar -cvfz archivocomprimido.tar.gz archivo 1 archivo 2 archivo 3`
	- -c: Crea un archivo tar.
	- -v: Modo verbose (muestra los archivos añadidos al tar).
	- -z: Comprime con gzip.
	- -f: Especifica el nombre del archivo tar.
- Y para descomprimir: `tar -xvzf`, donde la x indica que extrae los archivos.
- Para crear hard y softlinks funciona de la siguiente manera:
	- **hardlink**: `ln existing_file hardlink_name` -> `ln file.txt hardlink.txt`
	- **softlink**: ln -s target_file link_name.

- El PATH envioroment variable significa 

#### Introducción
## Resumen

La instalación de software en un sistema operativo consiste en copiar los archivos de la aplicación en las ubicaciones adecuadas y, si hace falta, ajustar parámetros de configuración. En sistemas modernos, gestionar las dependencias es fundamental, ya que antes de instalar un nuevo software hay que asegurarse de tener instaladas las librerías o paquetes de los que depende.

### Sistemas de gestión de software

En distribuciones como Debian (la base de ASO Linux), el software se organiza en paquetes `.deb`. Estos paquetes incluyen binarios, librerías, archivos de configuración, manuales y documentación, así como información sobre sus dependencias. De esta forma, es fácil instalar, actualizar y desinstalar programas sin tener que resolver manualmente las dependencias.

### Entorno gráfico en UNIX: X-Window

El sistema X-Window (X11, X) es un protocolo que ofrece las bases para mostrar interfaces gráficas en sistemas tipo UNIX. Funciona mediante un modelo cliente/servidor: el **X server** se encarga de la salida gráfica y de recibir la entrada del usuario, mientras que las aplicaciones (clientes) solicitan la creación de ventanas y reaccionan a eventos. X por sí solo no define el aspecto de las ventanas, menús o botones; esto queda en manos de:

- **Window Managers (Gestores de ventanas)**: Controlan la posición, aspecto y gestión de las ventanas. Ejemplos: `kwin`, `gnome-shell`, uno muy ligero: `pekwm`
- **Display Managers (Gestores de sesión)**: Muestran una pantalla de login gráfica y controlan el inicio de la sesión. Ejemplos: `XDM`, `GDM`, `SDDM`, `lightDM`.
- **Desktop Environments (Entornos de escritorio)**: Ofrecen una interfaz unificada con íconos, menús, barras de tareas y aplicaciones integradas (p.ej. GNOME, KDE). Estos entornos se apoyan en un gestor de ventanas y un display manager, y emplean una biblioteca gráfica (GTK+, QT, etc.).

*Si usas pekwm + lightDM no necesitas desktop enviroment, se hace todo desde la terminal

La tabla siguiente muestra algunos ejemplos:

| Entorno de Escritorio | Window Manager   | Display Manager | Biblioteca Gráfica |
|-----------------------|------------------|-----------------|--------------------|
| GNOME                 | gnome-shell      | GDM             | GTK+               |
| KDE                   | Kwin             | SDDM            | QT                 |
| XfCE                  | Xfwm4            | LightDM          | GTK+               |
| LXDE                  | Openbox          | LXDM            | QT                 |

### Instalación de paquetes binarios (Debian)

Para instalar paquetes `.deb` manualmente, se utiliza el comando `dpkg`. Este comando permite:

- Instalar paquetes: `dpkg --install paquete.deb`  
- Desinstalar (sin borrar archivos de configuración)  
- Purgar (desinstalar borrando además los archivos de configuración)  
- Listar paquetes instalados  
- Ver archivos de un paquete

#### Diferencia entre desinstalar y purgar un paquete

- **Desinstalar (remove)**: Elimina los archivos binarios del paquete, pero deja intactos los archivos de configuración.
- **Purgar (purge)**: Elimina tanto los archivos binarios como los archivos de configuración, dejando el sistema como si el paquete nunca se hubiese instalado.

#### Instalación con dependencias

Si un paquete tiene dependencias, es necesario instalarlas antes o simultáneamente. Por ejemplo, si al intentar instalar `lynx` falla por no tener `lynx-common`, primero habrá que instalar `lynx-common`.

**¿Qué comando usaste para instalar lynx sin el -common?**  
Se intentó con:  

```bash
dpkg --install lynx.deb
```

Esto falló debido a la falta de lynx-common. Tras instalar:

```bash
dpkg --install lynx-common.deb
```

Se pudo completar la instalación de lynx.

La instalación y gestión de paquetes en Debian puede realizarse con distintas herramientas, pasando desde el nivel básico (dpkg) hasta el avanzado (APT), que resuelve automáticamente las dependencias y facilita la instalación de entornos gráficos completos, compiladores y software externo.

#### APT y repositorios

Primero debes configurar el repositorio en /etc/apt/sources.list, por ejemplo:

```bash
deb http:_//ftp.es.debian.org/debian/ stable main non-free contrib_
```

Luego, actualiza el índice de paquetes:
```bash
apt update
```

Para actualizar todos los paquetes instalados a su última versión:
```bash
apt upgrade
```

Para obtener información de un paquete:
```bash
apt info nombre-paquete
```  

#### Instalación del entorno gráfico X-Window

Instalar el servidor X:

```Shell
apt install x-window-system
```
  
#### Entornos de escritorio

Debian proporciona metapaquetes (task-< entorno >-desktop) que instalan entornos completos:
Listar todos los paquetes:

  ```bash
  apt list
  ```

Filtrar metapaquetes task-...-desktop:

```bash
apt list | grep '^task-.*-desktop'
```

O usar la búsqueda:
```bash
apt search desktop
```

Elegir e instalar un entorno, por ejemplo GNOME:
```bash
apt install task-gnome-desktop
```
  
Si algo falla, reconfigura el paquete afectado:

```bash
dpkg-reconfigure nombre-paquete
```  

#### Preparar el sistema para compilar

Instalar compilador, librerías y Firefox:  

```bash
apt install gcc libc6-dev firefox
```

Limpiar la caché de paquetes:

```bash
apt clean
```
  
apt clean elimina todos los paquetes descargados de la caché, mientras que apt autoclean solo elimina los obsoletos.
#### Instalar binarios fuera de repositorios

Descomprimir JDK en una carpeta de tu elección:

```bash
tar -xvzf jdk-11.0.14_linux-x64_bin.tar.gz
```


Mover la carpeta resultante:

```shell
mv jdk-11.0.14 /opt/java1.11
```  

Verificar la versión:  

```shell
/opt/java1.11/bin/java -version
```  

Hacer lo mismo para otra versión (ej. Java 1.17) en /opt/java1.17.

El comando java -version del sistema no mostrará estas nuevas versiones porque no están en el PATH por defecto. Para solucionarlo, crea enlaces simbólicos:  

```shell
ln -s /opt/java1.11/bin/java /usr/local/bin/java
```

Así java -version usará la versión 1.11. Para acceder a distintas versiones sin cambiar el PATH por defecto, crea enlaces simbólicos con nombres distintos:  

```shell
ln -s /opt/java1.17/bin/java /usr/local/bin/java1.17
ln -s /opt/java1.11/bin/java /usr/local/bin/java1.11
```
  
De esta forma puedes ejecutar java1.17 -version o java1.11 -version según necesites.#### instalación desde código fuente*

En algunos casos es necesario instalar software directamente desde el código fuente, ya sea porque no hay un paquete disponible o para adaptar mejor la aplicación a nuestro sistema. El proceso típico incluye descargar el código fuente, configurarlo, compilarlo, instalarlo, y finalmente limpiar los archivos temporales.  

**Pasos generales:**
1. Descargar el archivo fuente (por ejemplo asosh-0.1.tar.gz) desde el servidor especificado.
2. Descomprimir el código fuente en el directorio designado, normalmente /usr/src.

```bash
tar -xvzf asosh-0.1.tar.gz -C /usr/src
```

_¿Qué comando usaste para descomprimir?_

```bash
sftp aso@asoserver.pc.ac.upc.edu + AsORoCkSHaRd!
cd sources + get asosh-0.1.tar.gz +exit
tar xvfz asosh-0.1.tar.gz
```

Por ejemplo, el anterior si estabas en el directorio donde se descargó el tar.
3. Examinar el contenido del directorio del código fuente. Allí suele haber un script configure que permite ajustar la instalación (por defecto, asosh se instala en /usr/local).

Para que se instale en /usr/local/asosh:  

```bash
./configure --prefix=/usr/local/asosh  
```

_¿Qué parámetros se usaron?_

```bash
La opción --prefix=/usr/local/asosh.
```

4. Si la configuración da error por falta de librerías de desarrollo (headers), por ejemplo un mensaje indicando que no encuentra cierto header (.h):

_¿Cuál es el error reportado?_
Alguna librería requerida no está presente (por ejemplo falta una librería de desarrollo).

_¿Razón del error?_
Las cabeceras de desarrollo no están instaladas.

_¿Cómo lo solucionaste?_
Instalar el paquete de desarrollo correspondiente:
```bash
apt install libreadline-dev
```

5. Una vez solucionadas las dependencias, ejecutar de nuevo:  
```
./configure --prefix=/usr/local/asosh
```
  
Si termina sin errores, procedemos a compilar:

```bash
make
```
  
Este paso no requiere permisos de root.

6. Instalar el software ya compilado (coloca los binarios y demás archivos en su ubicación final):

```
sudo make install
```


7. Una vez instalado, es buena idea eliminar los archivos temporales generados durante la compilación:

_¿Qué comando se usa para borrar archivos temporales?_

```
make clean
```
  
Además, se pueden revertir los pasos de instalación:

_¿Qué argumento se puede usar para deshacer la instalación?_
  
```
make uninstall
```

Este proceso es estándar para la mayoría de software distribuido en código fuente: configurar (./configure), compilar (make), instalar (make install), limpiar (make clean) y, si es necesario, desinstalar (make uninstall).

# Práctica 3: Scripts


Todos los intérpretes de comandos incorporan un lenguaje de programación con sentencias de control de flujo, asignación de variables, funciones, etc. Los usuarios pueden escribir programas (****shellscripts****) utilizando este lenguaje para automatizar la ejecución de secuencias de comandos. Los shellscripts serán interpretados por el shell.

### Creación de un Shellscript

1. **Crear el archivo:**
   - Invoca un editor de textos y escribe el código correspondiente.
2. **Primera línea del script:**
   - `#!/bin/bash`  
     Indica el shell que interpretará el programa.
3. **Guardar el archivo:**
   - Guarda el script con un nombre adecuado, por ejemplo, `mi_script.sh`.
4. **Dar permisos de ejecución:

```bash
chmod 700 mi_script.sh
  ```

5. **Ejecutar el script:**
```bash
./mi_script.sh
```

### Comentarios en Shellscripts
  
- Utiliza el carácter `#` para insertar comentarios dentro del shellscript.  
### Consulta del Manual

- Para buscar información en el manual sobre las sentencias propias de ****bash**** relacionadas con la programación de shellscripts, ejecuta:

  ```bash
  man bash
```

### Comandos Comunes en Shellscripts
#### sleep
• **Descripción:**
	Detiene la ejecución del shellscript durante el número de segundos indicado como parámetro.
• **Ejemplo:**
	sleep 5
	Retorna el control pasados 5 segundos.
#### echo
• **Descripción:**
Muestra un mensaje en la salida estándar. Permite imprimir el valor de las variables.
• **Ejemplos:**
	echo Hola
	Muestra el mensaje “Hola”.
	echo Valor de home: $HOME
	Muestra el contenido de la variable HOME.
	echo -n Sin salto de línea
	No muestra salto de línea (parámetro -n).
	echo -e "\ta\t"
	El parámetro -e activa la interpretación de caracteres especiales como \t (tabulador).
**test**

• **Descripción:**
Evalúa condiciones respecto a archivos (existencia, permisos, tipo), cadenas de caracteres (igualdad, etc.) o numéricas (igualdad, desigualdad, mayor que, etc.). No escribe nada en la salida estándar, pero devuelve un código de estado ($?):
	0 si la condición es verdadera.
	Diferente de 0 si la condición es falsa.
• **Ejemplos:**
`test -d /bin; echo $?`
Escribe 0 porque /bin es un directorio.
`test -w /bin; echo `
Escribe 1 porque no se puede escribir en /bin.
`test hola = adeu; echo $?`
Escribe 1 porque las cadenas son diferentes.
`test 4 -gt 5; echo $?`
Escribe 1 porque 4 no es mayor que 5.
`test 3 -ne 6; echo $?`
Escribe 0 porque 3 no es igual a 6.
`test 3 -gt 2 -a 5 -lt 7; echo $?`
Escribe 0 porque se cumplen ambas condiciones (-a indica and).

#### expr
• **Descripción:**
Evalúa una expresión aritmética y muestra el resultado en la salida estándar.
• **Ejemplos:**
`expr 3 + 4`
Muestra 7. Es necesario que existan espacios en blanco entre los operandos y el operador.
`expr 3 \* 4`
Muestra 12. Es necesario proteger el operador * con el carácter de escape \ para evitar que el shell lo interprete como un comodín.

#### read
• **Descripción:**
Permite leer una línea de la entrada estándar y guardarla en una variable. También puede guardar las palabras que componen la línea en variables diferentes.
 
- **Ejemplos:**
`read lin; echo L: $lin`
Carga la línea leída en la variable lin.
`read word1 word2; echo L1: $word1; echo L2: $word2`
Carga la primera palabra leída en word1 y la segunda (y las restantes) en word2.
#### exit
• **Descripción:**
Finaliza la ejecución del shellscript.
#### true / false
• **Descripción:**
Comandos que se usan para generar condiciones de control en bucles infinitos.
#### Comillas (Metacaracteres) en Shellscripts

El shell dispone de tres tipos de comillas:
• **Comillas simples (**' '**)**
• Interpretan literalmente la cadena que están entre las comillas (sin expandir metacaracteres ni interpretar espacios en blanco como separadores).
• Ejemplo:
`echo '$PATH *'`
Muestra la cadena literal $PATH *.

• **Comillas dobles (**" "**)**

• Permiten interpretar el metacaracter $ para reemplazar el valor de las variables.

• Ejemplo:

`echo "$PATH *"`

Muestra el valor de la variable PATH seguido de la lista de archivos del directorio actual.

• **Comillas inversas (\ ` `` `)**

• Ejecutan la comanda que está entre las comillas y usan el resultado como parámetro de otra comanda.
• Permiten interpretar el metacaracter $.
• Ejemplo:
```bash
ls -l `which sort`
```

Utiliza el resultado de ejecutar which sort como parámetro para ls -l.

• **Escapar metacaracteres (**\**)**
• Inhibe la expansión de metacaracteres.
• Ejemplo:

```bash
echo \*
  ```

Muestra el carácter * en lugar de expandirlo a la lista de archivos.

#### Variables

Repasa lo explicado en sesiones anteriores sobre variables.

**Control de Flujo**
**if**
• **Sintaxis:**

```bash
if condición1
then
    sentencias1
[ elif condición2
then
    sentencias2 ]
...
[ else
    sentencias3 ]
fi
```

• **Descripción:**
Evalúa una condición. Si es verdadera, ejecuta sentencias1; si es falsa y condición2 es verdadera, ejecuta sentencias2; y así sucesivamente. Si todas las condiciones son falsas, ejecuta sentencias3.

• **Formas típicas de generar condiciones:**
	• Comando test.
	• Comando grep (retorna verdadero si encuentra la palabra).
	• Otras comandas que retornan verdadero si han ejecutado correctamente y falso en caso de error.
	
**while / until**
• **Sintaxis:**
```bash
while condición
do
    sentencias
done
  ```

```bash
until condición
do
    sentencias
done
```

• **Descripción:**

• `while:` Evalúa la condición. Si es verdadera, ejecuta las sentencias dentro del bucle y vuelve a evaluar.
• `until:` Itera mientras la condición se evalúe como falsa.

**for**
• **Sintaxis:**
  
```bash
for variable in lista_valores
do
    sentencias
done
```

• **Descripción:**

Itera sobre cada elemento de lista_valores y ejecuta las sentencias internas. En cada iteración, variable toma el valor del elemento correspondiente.

• **Formas de generar** lista_valores:

• * para iterar sobre los nombres de archivo del directorio actual.
• Comando entre comillas invertidas para iterar sobre cada palabra resultante de la ejecución de una comanda.
• $* para iterar sobre los parámetros del shellscript.

#### case
• **Sintaxis:**
```bash
case palabra in
    patrón1) sentencias1 ;;
    patrón2) sentencias2 ;;
    ...
    patrónN) sentenciasN ;;
esac
```

• **Descripción:**

Busca el primer patrón que corresponda a palabra y ejecuta las sentencias asociadas.
• **Uso de patrones:**
• a*: Palabras que comienzan con a.
• a*|b*: Palabras que comienzan con a o b.
• *: Todas las palabras (usualmente como último patrón para manejar casos no coincidentes).

**Comentarios sobre las Sentencias de Control de Flujo**
- Dentro de bucles (**for**, **while**, **until**):
-  **break**: Sale del bucle.
- **continue**: Salta a la siguiente iteración del bucle.

• **Redirección:**
• Es posible redirigir la entrada estándar y/o la salida estándar de una sentencia de tipo for, while o until. Esta redirección afecta a todas las comandas ejecutadas dentro del bucle.
• **Errores Comunes:**

• Olvidar palabras clave como done o no cerrar una cometa puede provocar el error de ejecución Unexpected EOF.

**Paso de Argumentos a los Shellscripts**
Cuando invocamos un shellscript, podemos pasarle argumentos. Para acceder a ellos:
- $#**:**
*Permite obtener el número de parámetros del shellscript.*
• $***:
*Contiene la lista de todos los parámetros del shellscript*

**Acceso Individual:**
• El primer parámetro: $1
• El segundo parámetro: $2
• …
• El noveno parámetro: $9

• **Más de 9 Parámetros:**
• Para acceder a parámetros superiores a $9, utiliza la comanda shift.

```bash
shift
```

• **Descripción:**
Descarta el valor de $1, mueve el valor de $2 a $1, el de $3 a $2, …, y coloca el valor del primer parámetro no accesible en $9. Actualiza el valor de $# y $*.

**Nota:** El efecto de shift no puede ser deshecho.
• $0:
Siempre contiene el nombre del **shellscript**.

#### Comprobación de Argumentos

Cuando un shellscript espera argumentos, es recomendable comprobar que el valor de $# es el esperado.
  
**Ejemplo:**
  
```bash
if [ $# -lt 2 ]; then

    echo "Uso: $0 arg1 arg2"

    exit 1

fi
```

Este script verifica que al menos se hayan pasado dos argumentos; de lo contrario, muestra un mensaje de *Usage* y finaliza.

## Inicio práctica 3

### Script para detectar a usuarios inválidos

> Tenemos que hacer un script que determine qué usuarios en /etc/passwd son inválidos, es decir si el usuario está en el archivo passwd pero no tiene ningún archivo. Aunque también existen algunos usuarios que no tienen archivos pero sirven para ejecutar los *daemons* (programas que se ejecutan en segundo plano) y debemos añadir una opción que declare que éstos usuarios sí son válidos.

Tenemos que rellenar los huecos del siguiente script:

```bash
# !/ bin / bash
p=0
function print_help
{
	echo "Usage:␣$1␣[options]␣"
	echo "Possible␣options:"
	echo "-p␣validate␣users␣with␣running␣process"
}
if [ $ # - gt 1 ]; then
	print_help $0
	exit
fi

while [ $ # - gt 0 ]; do
	case $1 in
		"-p")
			p=1
			shift;;
		*) 
			echo "Error:␣not␣valid␣option:␣$1"
			exit 1;;
	esac
done


for user in _______________; do
	home=$ (cat /etc/passwd | grep "^$user:" | cut -d: -f6)
	if [ -d $home ]; then
		num_fich=$ (find "$home" -type f -user $user | wc -l)
	else
		num_fich=0
	fi
	
	if [ $num_fich -eq 0 ]; then
		if [ $p -eq 1 ]; then
			user_proc=___________________
			if [ $ user_proc -eq 0 ]; then
				echo "The user $user has no processes"
			fi
		else
			echo "The user $user has no files in $home"
		fi
	fi
done
```

- Por lo que parece tenemos que rellenar dos huecos, el primero lo rellenamos con:
```bash
$(cut -d: f1 /etc/passwd)
```

- **cut**: como éste comando imprime las partes seleccionadas de cada linea de un ARCHIVO por la salida estándar, nos interesa para imprimir el primer campo (field, f1) del archivo /etc/passwd de cada usuario. La opción -d hace que se vean solo los nombres de usuario, sin esa opción se vería todo el archivo /etc/passwd. Al ser un comando, debe ir con $ antes y entre paréntesis.

- Para rellenar el segundo campo, debemos saber cómo sabemos si un usuario tiene procesos en ejecucción y eso lo sabemos gracias al comando `ps -U username`, y para saber si NO tiene ningún proceso en ejecucción lo podemos saber gracias a que no devuelva ninguna línea, con lo que podríamos hacer un `wc -l` del comando anterior que cuente las líneas.

```bash
user_proc=$(ps -U|wc -l)
user_proc=$((user_proc-1))
```
El -1 es para eliminar la línea automática que siempre se cuenta, la de los encabezados. También podría hacerse poniendo `--headers` antes de user_proc.

> El comando `shift` elimina el primer argumento posicional ($1) de la lista de argumentos haciendo que el siguiente argumento pase a ser  $1. Esto se usa para iterar correctamente sobre las opciones una vez que se ha procesado una.

> En el comando `grep "^$user:"`sobre /etc/passwd, el símbolo ^ indica el inicio de la linea, con lo que ^$user: busca una línea que comience exactamente con el nombre del usuario seguido de dos puntos. Esto evita que se obtengan coincidencias parciales, asegurando que solo se localice la línea correspondiente a ese usuario específico. El carácter : es importante porque en el archivo /etc/passwd el formato es usuario:contraseña:UID:GID:info:home:shell, así el : tras el nombre de usuario garantiza que sea el campo correcto, no solo una subcadena del nombre.

#### Detección de usuarios inactivos

Ahora extenderemos el script anterior para detectar usuarios inactivos, es decir un usuario que no tiene ningún proceso en ejecución, que hace mucho no inicia sesión y que no ha cambiado ninguno de sus archivos desde hace mucho tiempo. El periodo de tiempo se pasará por parámetro:

![[Pasted image 20241212150428.png]]
#### Otro ejemplo de script

Escribe un script que muestre un llistado con los 10 procesos que mas tiempo consumen en CPU. El listado tiene que mostrar 10 líneas, una por proceso, donde cada linea debe mostrar el pid, el usuario propietario, el tiempo acumulado y el nombre del ejecutable. Las lineas deben estar ordenadas de más a menos tiempo consumido.

```bash
#!/bin/bash
ps -eo pid,user,cputime,comm --sort=-cputime | head -n 11
```

Resumen de como funciona:
- `ps` muestra los procesos actuales
- `-e` muestra todos los procesos
- `-o` hace que salga con un formato específico (pid,user,cputime,comm (comanda)).
- `--sort` es una opcion de output, puedes añadir `+` o `-` para ordenar creciente o decrecientemente.
- `head`corta el output a `n` lineas (10 + el header), el propio `ps` no tiene una opción directa para controlar el numero de lineas de output

Modifica el script de forma que podamos parametrizar el numero de procesos a mostrar. Por defecto el script se comportará como el del apartado anterior, pero si recibe un parámetro este sera el número de procesos que hay que alistar.

```bash
DEFAULT_NUM=10
NUM_PROCS=${1:-$DEFAULT_NUM}

ps -eo pid,user,cputime,comm --sort=-cputime | head -n $((NUM_PROCS + 1))
```

# Práctica 4 gestión de usuarios
### Objetivos
- Crear nuevas cuentas de usuario y cambiar sus propiedades.
- Deshabilitar y eliminar cuentas de usuario de forma segura.
### Antes de empezar
*Preguntas previas:*
1. **¿En qué archivos se definen las bases de datos de usuarios, contraseñas y grupos?**
   - Usuarios y contraseñas: `/etc/passwd` (usuarios y algunos datos básicos), `/etc/shadow` (contraseñas cifradas y políticas de expiración).
   - Grupos: `/etc/group`.

2. **¿Cómo se pueden asignar UID para nuevos usuarios?**
   - El UID se asigna típicamente de forma automática al crear usuarios con `useradd` u `adduser`. Si se hace manualmente, se puede editar `/etc/passwd` y asignar un UID único no utilizado. Normalmente las distribuciones mantienen un rango de UID para usuarios del sistema (0-999) y otro para usuarios normales (1000 en adelante).

3. **¿Qué comandos pueden usarse para cambiar propietarios y permisos de un archivo y de todos los archivos en un directorio?**
   - Cambiar propietario: `chown`.
   - Cambiar grupo: `chgrp`.
   - Cambiar permisos: `chmod`.
   Para aplicar en un directorio y todos sus subdirectorios y archivos, se usa la opción `-R` (recursivo), por ejemplo: `chown -R usuario:grupo /ruta/del/directorio`.

> En un sistema Linux, cada usuario tiene una cuenta que incluye toda su información, archivos y procesos. Los usuarios se identifican internamente con un UID (un número entero). Además, existe una base de datos que asocia el UID a un nombre de usuario (username), y que también contiene información adicional (como el directorio home, el shell de inicio, etc.).
  
La creación de un nuevo usuario implica:
- Asignar un UID.
- Modificar la base de datos de usuarios.
- Crear un grupo o asociar el usuario a uno existente.
- Copiar archivos de configuración inicial desde `/etc/skel` al directorio home del usuario.
- Opcionalmente asignar el usuario a varios grupos.

El uso de grupos permite dividir a los usuarios en categorías con diferentes permisos y privilegios.
### Perfil y entorno de usuario

Tras un login interactivo, el shell ejecuta ciertos archivos de configuración. En el caso de BASH:

- Se ejecuta `/etc/bash_profile` (o `/etc/profile`) para configurar el entorno global.
- Luego se ejecuta `~/.bash_profile` para la configuración del usuario.

En `/etc/skel` se almacenan archivos base que se copian al crear nuevos usuarios. Esto permite asegurar un entorno mínimo (variables PATH, prompt, etc.).

***Ejemplo:***
- Asegurar que el PATH de todos los usuarios contenga `/usr/local/bin`:

```bash
  export PATH=$PATH:/usr/local/bin  
```

Este comando toma el valor actual de PATH, y le agrega al final :/usr/local/bin. De esta forma, cuando el usuario ejecute comandos, también se buscarán en ese directorio.

**Análisis del comando** `export PATH=$PATH:/usr/local/bin:`
• export PATH=: indica que vamos a definir la variable de entorno PATH.
• `$PATH:/usr/local/bin`: Toma el valor actual de PATH ($PATH) y agrega :/usr/local/bin.
• Con export hacemos la variable visible para procesos hijos.

**Cambiar el prompt para el usuario** aso:
Queremos que se vea así:  
`aso:CWD - date $`
Donde CWD es el directorio actual y date es la fecha en formato día/mes hora:minuto.
Podemos modificar la variable de entorno PS1 en ~/.bash_profile por:
```PS1='aso:\w - \d \t $'```
• \w muestra el directorio actual.
• \d muestra la fecha en formato DOW Mon DD.
• \t muestra la hora actual HH:MM:SS.
Si se requiere un formato específico día/mes hora:minuto, se podría utilizar el comando date embebido, por ejemplo:
PS1='aso:\w - $(date +"%d/%m %H:%M") $ '

**¿Qué cambios se aplicaron a la variable PATH?**
• Se le agregó el directorio /usr/local/bin.
**¿En qué variable se define el prompt?**
• En la variable de entorno PS1.
**¿Qué cambios se aplicaron a la variable del prompt?**
• Se estableció un valor personalizado que muestra el nombre del usuario, el directorio actual y la fecha/hora en el formato deseado.

### Creación de usuarios manualmente
Se pide crear cuentas de usuario para cada miembro del grupo de laboratorio, asignándolos al grupo admin.
**Parámetros a definir:**
• UID
• Nombre de usuario
• Directorio HOME
• Shell
• Grupos (principal y secundarios)
Por ejemplo:
**Parámetros** **Usuario 1** **Usuario 2**

UID 1001 1002
Username quique marc
HOME /home/quique /home/marc
Shell /bin/bash /bin/bash
Groups admin (primario) admin (primario)

Para editar la base de datos de usuarios, se usa:
vipw
Esto abre /etc/passwd en un entorno seguro.

**¿Diferencia entre usar vipw y editar directamente con vi?**

• vipw bloquea el fichero /etc/passwd y /etc/shadow para evitar corrupciones si otro administrador está editándolo simultáneamente. Garantiza integridad y seguridad. Si se usara vi directamente, podríamos dañar la consistencia del archivo si alguien más lo edita a la vez.

Usar vigr para editar /etc/group y crear o modificar grupos. Con vipw -s podemos editar /etc/shadow de forma segura.

**¿Qué grupos se han creado?**

• Por ejemplo students.

**¿Qué usuarios forman parte de esos grupos?**
• quique y marc en students.
• Otros usuarios según necesidad.
**Desactivar una cuenta de usuario para que no pueda hacer login:**

• Se puede colocar un * o ! al inicio del campo de contraseña en /etc/shadow.
• Por ejemplo, cambiar el campo de contraseña del usuario en /etc/shadow a 
`!:usermod -L username`
o manualmente con vipw -s colocando !.
**Desactivar cuentas nuevas hasta terminar el proceso:**
```bash
usermod -L juan
usermod -L maria
```

Crear el directorio HOME:
```bash
mkdir /home/quique
cp -r /etc/skel/.* /home/quique
chown -R quique:quique /home/quique
chmod 700 /home/quique
  ```
  
**¿Qué comandos se han usado para cambiar el propietario?**
`chown -R juan:juan /home/juan`

**¿Qué comandos para cambiar los permisos?**
`chmod 700 /home/juan`

**Asignar contraseña:**
```bash
passwd quique
passwd marc
```  

Esto actualiza /etc/shadow.

**¿Qué riesgos de seguridad existen al poner la contraseña en el archivo de usuarios?**

• Si la contraseña estuviera en /etc/passwd (en texto plano o cifrado simple) podría ser leída por cualquier usuario ya que /etc/passwd es legible por todos. Por eso se usa /etc/shadow, que sólo es legible por root.

**¿Qué comando se usa para editar /etc/shadow de forma segura?**
```bash
vipw -s
```

**¿Qué significan los parámetros en /etc/shadow?**

`/etc/shadow` contiene:
	• Nombre de usuario
	• Contraseña cifrada
	• Días desde el epoch del último cambio de contraseña
	• Mínimo y máximo de días de validez, aviso de expiración, etc.
**¿Qué comando puede modificar parámetros de la contraseña?**
• `chage` permite modificar las fechas de expiración de la contraseña, etc.
Usar `chfn` y `chsh` para establecer información del usuario:

• `chfn` juan permite cambiar el nombre completo, teléfono, etc.
• `chsh` juan permite cambiar el shell del usuario.

### Creación automática de usuarios

Utilizar useradd (o adduser) para crear cuentas:

• Profesores: emorancho, rserral

• Estudiante: student

• Cuentas asoXX para grupos de práctica, por ejemplo: aso01, aso02, etc.

Elegir nombres adecuados. Por ejemplo, emorancho y rserral para profesores, student para el estudiante genérico, y aso01 para un grupo.

```bash
#!/bin/bash

# Función para crear un usuario
create_user() {
    local username=$1
    local group=$2
    local shell=$3
    local home=$4

    # Crear grupo si no existe
    if ! grep -q "^${group}:" /etc/group; then
        echo "Creando grupo $group..."
        groupadd $group
    fi

    # Crear usuario con los parámetros especificados
    echo "Creando usuario $username..."
    useradd -m -d "$home" -s "$shell" -g "$group" "$username"

    # Asignar contraseña predeterminada (puede ser cambiada después)
    echo "$username:password" | chpasswd

    # Mostrar detalles
    echo "Usuario $username creado con éxito."
    echo "Home: $home | Grupo: $group | Shell: $shell"
    echo ""
}

# Crear profesores
echo "Creando cuentas de profesores..."
create_user "emorancho" "professors" "/bin/bash" "/home/emorancho"
create_user "rserral" "professors" "/bin/bash" "/home/rserral"

# Crear estudiante genérico
echo "Creando cuenta de estudiante..."
create_user "student" "students" "/bin/bash" "/home/student"

# Crear usuarios para grupos de laboratorio
echo "Creando cuentas de otros usuarios (grupos de laboratorio)..."
for i in $(seq -w 1 4); do
    username="aso$i"
    create_user "$username" "labgroup" "/bin/bash" "/home/$username"
done

echo "Todas las cuentas han sido creadas."
```


**Permisos para diferentes grupos:**
• Profesores: acceso a nivel de grupo a todos los archivos de todos los usuarios.
• Estudiantes: acceso a nivel de grupo a todos los archivos de todos los usuarios, excepto el de los profesores.
• Administradores: acceso a nivel de grupo sólo a los archivos de su propio grupo.
• Otros usuarios (asoXX): sin acceso a nivel de grupo a ningún archivo.

Estas condiciones dictan el uso de grupos y máscaras de creación (umask) apropiadas.

**¿Cómo configurar los permisos del directorio para que los archivos heredados tengan permisos adecuados?**

• Ajustar la umask en /etc/profile o en el ~/.bash_profile para los grupos deseados.
• Por ejemplo, para que los archivos creados por teachers tengan permisos group-read y group-write, se puede usar umask 002.
• Además, el bit **setgid** en directorios asegura que los nuevos archivos creados hereden el grupo del directorio, por ejemplo:

```$> chmod g+s /home/teachersgroup```

**Eliminar y desactivar de usuarios**

Para eliminar un usuario se deben:
• Borrar su correo, trabajos de impresión, trabajos cron y at.
• Eliminar su entrada en /etc/passwd, /etc/shadow y /etc/group.
• Borrar sus archivos, previo back up.

**¿Cómo hacer backup de todos los archivos de un usuario?**
• Usar find y tar:
```bash
find /home/username -user username -print | tar cvf backup_username.tar -T -
```

**Problema con nombres con espacios:**
• `xargs` por defecto separa por espacios. Usar xargs -0 y find -print0 para manejar nombres con espacios (sin comprimir)
```bash
find / -user username -print0 | xargs -0 -I _ cp _ /backups
```

**¿Qué comando para buscar y eliminar todos los archivos de un usuario?**
- con -exec:
`find / -user username -exec rm {} \;`
- con xargs y excluyendo carpeta de backups:
`find / -not \(-name"backups"\) -user username -print | xargs -I _ rm -rf _`


Deshabilitar la cuenta antes de eliminar archivos:
• Cambiar el shell del usuario a un script que informe la desactivación:
`chsh -s /usr/local/bin/failed-login.sh username`

`/usr/local/bin/failed-login.sh:`
```bash  
#!/usr/bin/bash

echo "Esta cuenta ha sido cerrada por razones de seguridad."

echo "Contacte al administrador."

read
```

• Asegurar permisos de ejecución: chmod +x /usr/local/bin/failed-login.sh
• Añadir /usr/local/bin/failed-login.sh a /etc/shells.

**¿Cómo comprobar que la cuenta está desactivada?**

• Intentar iniciar sesión con ese usuario y verificar que aparece el mensaje del script en vez de iniciar shell.

**Script para hacer backup, borrar archivos y desactivar cuenta:**
```bash
#!/bin/bash
# Script: remove_user.sh
# Uso: remove_user.sh username

if [ $# -ne 1 ]; then

  echo "Uso: $0 username"

  exit 1

fi

user=$1  

# 1. Backup de archivos

backup="backup_${user}.tar"

find / -user $user -print0 | xargs -0 tar cvf $backup

_# 2. Borrar archivos del usuario_

find / -user $user -exec rm {} \;

_# 3. Desactivar cuenta cambiando el shell_

chsh -s /usr/local/bin/failed-login.sh $user

echo "Cuenta $user desactivada y archivos respaldados en $backup."
```


### Sudo y Control de la Ejecución de Aplicaciones


Al igual que shutdown, hay otros comandos de administración que solo pueden ser ejecutados por el usuario root. Es una mala práctica de seguridad usar la cuenta root para ejecutar estos comandos. Para resolver este problema, se puede utilizar el comando sudo, que permite a un usuario ejecutar un comando con permisos de root. La configuración de qué aplicaciones puede ejecutar un usuario en particular se define en el archivo /etc/sudoers. Este archivo debe ser editado de manera segura usando el comando visudo.

**Pasos para Configurar sudo**
**1. Editar el Archivo /etc/sudoers Usando visudo**
Siempre utiliza `visudo` para editar el archivo /etc/sudoers ya que realiza comprobaciones de sintaxis antes de guardar los cambios, evitando errores que podrían bloquear el acceso administrativo.
```sudo visudo```.

**2. Permitir al Grupo admin Ejecutar Todos los Comandos como Superusuarios**
Añade la siguiente línea al final del archivo /etc/sudoers:
```bash
%admin ALL=(ALL:ALL) ALL
```  

• %admin: Se refiere al grupo admin.

• ALL=(ALL:ALL): Permite ejecutar comandos como cualquier usuario y grupo.

• ALL: Permite ejecutar cualquier comando.

**3. Permitir al Grupo teachers Ejecutar Scripts Específicos y Binaries**

Añade la siguiente línea para permitir que los usuarios del grupo teachers ejecuten el script de eliminación de usuarios y todos los binarios en /usr/local/teachers/bin:

```bash 
%teachers ALL=(ALL:ALL) /usr/local/bin/remove_user.sh, /usr/local/teachers/bin/*
```
• %teachers: Se refiere al grupo teachers.
• /usr/local/bin/remove_user.sh: Ruta al script específico que permite eliminar usuarios.
• /usr/local/teachers/bin/*: Permite ejecutar cualquier binario dentro de este directorio.

• **Como miembro del grupo** admin:

```bash
sudo whoami
```

Debería devolver root.

• **Como miembro del grupo** teachers:
Ejecuta el script permitido:
```bash
sudo /usr/local/bin/remove_user.sh username
```
Debería ejecutarse sin solicitar permisos adicionales.

**6. Deshabilitar la Cuenta Root**  
**Pasos para Deshabilitar la Cuenta Root**

1. **Asegurarse de Tener Acceso Administrativo con** sudo
Antes de deshabilitar root, verifica que puedes ejecutar comandos administrativos con un usuario del grupo admin.

```bash
sudo whoami
```

Debería devolver root.

2. **Bloquear la Cuenta Root**

Bloquea la contraseña de root para evitar inicios de sesión directos.

```bash
sudo passwd -l root
```
  
• -l: Bloquea la contraseña del usuario, evitando inicios de sesión directos.

3. **Verificar que la Cuenta Root Está Bloqueada**
Intenta cambiar a root:

```bash 
su - root
```

Deberías recibir un mensaje de error indicando que la cuenta está deshabilitada.

4. **Configurar** sudo **para Usar Solo Usuarios del Grupo** admin
Asegúrate de que solo los miembros del grupo admin puedan usar sudo para tareas administrativas.

**Preguntas y Respuestas**

1. **¿Qué cambios se requieren en el archivo** /etc/sudoers **para habilitar la configuración descrita anteriormente?**

• **Para el Grupo** admin:
```bash 
%admin ALL=(ALL:ALL) ALL
```

Permite a todos los miembros del grupo admin ejecutar cualquier comando como cualquier usuario y grupo.

• **Para el Grupo** teachers:

```bash
%teachers ALL=(ALL:ALL) /usr/local/bin/remove_user.sh, /usr/local/teachers/bin/*
```
  
Permite a los miembros del grupo teachers ejecutar el script específico remove_user.sh y cualquier binario dentro de /usr/local/teachers/bin.

2. **¿Cuáles son los pasos requeridos para deshabilitar la cuenta root?**
• **Verificar Acceso Administrativo:**
• Asegúrate de que puedes ejecutar comandos administrativos con sudo desde una cuenta perteneciente al grupo admin.

• **Bloquear la Cuenta Root:**
• Ejecuta `sudo passwd -l root` para bloquear la contraseña de root.
• **Verificar el Bloqueo:**
• Intenta cambiar a root con `su - root` y verifica que no es posible iniciar sesión.
• **Configurar** sudo **Adecuadamente:**
• Asegúrate de que solo los usuarios autorizados (grupo admin) puedan usar sudo para tareas administrativas antes de bloquear a root.

---

# Practica 5 Backups

**Resumen rápido preguntas del principio:**

### **Empaquetar y desempaquetar archivos con** tar:

• **Empaquetar:**

```bash
tar -cvf archivo.tar archivo1 archivo2 directorio/
```
• -c: Crea un nuevo archivo tar.
• -v: Muestra el progreso en la terminal.
• -f: Especifica el nombre del archivo tar resultante.

• **Desempaquetar:**

```bash
tar -xvf archivo.tar
```

• -x: Extrae los archivos del tar.
• -v: Muestra el progreso en la terminal.
• -f: Especifica el archivo tar a extraer.


• **Hard link**

• Un hard link es una referencia adicional al mismo inodo en el sistema de archivos.

• **Crear un hard link**

```bash
ln archivo_a archivo_b
```
  
> **Diferencia entre** cp **y** ln:


- **Copiar archivos (cp):**
• Crea una copia independiente con un inodo diferente.
• Modificar uno no afecta al otro.
• Si se elimina uno, el otro permanece.

- **Crear un hard link (ln):**
• Ambos archivos comparten el mismo inodo.
• Modificar uno afecta al otro.
• El archivo no se elimina hasta que todos los enlaces son eliminados.

### **Introducción**

**Consideraciones para la Política de Back up**

> Antes de realizar back ups , el administrador debe decidir una política considerando aspectos como:

• **Tipo de Medio Físico:** Seleccionar el medio adecuado para los back ups  considerando tamaño, costo, velocidad, disponibilidad, usabilidad y fiabilidad.

• **Archivos a los que hacer un back up:** Decidir qué archivos necesitan back up y dónde se encuentran. Los archivos más importantes son los de configuración y los de usuario (usualmente en /root y /home, respectivamente). Algunos archivos no requieren back up, como los temporales (/tmp) y los binarios del sistema (/bin, /sbin/).

• **Frecuencia y Programación:** Depende de la variabilidad de los datos. Por ejemplo, una base de datos puede requerir back ups  múltiples diarios, mientras que un servidor web puede necesitar solo una copia diaria y otros sistemas de archivos una copia semanal.

• **Otros Aspectos:** Dónde almacenar las copias, cuánto tiempo mantenerlas y la rapidez necesaria para recuperar cada tipo de archivo.

**Estrategia de back up**

Con la información anterior, es posible decidir una estrategia de back up que incluye la frecuencia y el tipo de copias. Una estrategia común es realizar copias completas e incrementales:

• **Copias Completas (Nivel 0):** Semanales.
• **Copias Incrementales (Nivel 1 o superior):** Diarias.

Si la tasa de cambio de archivos es muy alta, se puede modificar el modelo para incluir:
• **Nivel 0:** Copia mensual.
• **Nivel 1:** Copias incrementales semanales.
• **Nivel 2:** Copias incrementales diarias.


**Herramientas para Implementar la Estrategia**

En este laboratorio utilizaremos `tar` y `rsync`. Se usará el mismo disco para realizar los back ups , aunque en un entorno real esto no es recomendable debido al alto riesgo de que una pérdida de datos afecte también a los back ups .

  
  

### **Pasos para Configurar la Partición de Back Up**

1. **Crear el directorio** /backup:
Este directorio servirá como punto de montaje para la nueva partición donde se almacenarán los back ups .

```bash
mkdir /backup
```



2. **Crear una nueva partición en el espacio libre disponible:**

Utiliza herramientas como gdisk para crear una nueva partición en el espacio libre del disco.
  
```bash
gdisk /dev/sdX
```

• Dentro de `gdisk`, sigue los pasos interactivos:
• Presiona n para crear una nueva partición.
• Selecciona el tipo de partición, número y tamaño según tus necesidades.
• Presiona w para escribir los cambios en el disco.

3. **Formatear la partición con el sistema de archivos** `btrfs`:
Formatea la nueva partición para prepararla para su uso.
```bash
mkfs.btrfs /dev/sdXn
```

• Reemplaza /dev/sdXn con el identificador de la partición creada (por ejemplo, /dev/sdb1).


4. **Montar la partición en el directorio** /backup:

Monta la partición formateada en el directorio /backup.

```bash
mount /dev/sdXn /backup
```

5. **Cambiar los permisos del directorio** /backup **para restringir el acceso a root:**

Ajusta los permisos para que solo el usuario root pueda acceder al directorio, protegiendo así los back ups .
  
chmod 700 /backup
chown root:root /backup


**Protección Adicional para el Directorio /backup**

Para aumentar la seguridad del directorio /backup, es recomendable montar la partición en modo de solo lectura la mayor parte del tiempo, permitiendo el modo de lectura-escritura únicamente cuando se realicen back ups . Esto previene modificaciones no autorizadas y protege la integridad de los datos respaldados.

• **Montar en modo de solo lectura:**

```bash
mount -o remount,ro /dev/sdXn /backup
  ```
  
• **Montar en modo de lectura-escritura:**

```bash
mount -o remount,rw /dev/sdXn /backup
```



**Respuesta a la Pregunta Planteada**

**¿Qué debes hacer para montar automáticamente esta nueva partición en modo de solo lectura al inicio del sistema?**  

Para montar automáticamente la nueva partición en modo de solo lectura durante el arranque del sistema, es necesario editar el archivo /etc/fstab. Este archivo contiene las especificaciones de montaje de los sistemas de archivos que se deben montar al iniciar el sistema.

**Pasos para Configurar el Montaje Automático en Modo de Solo Lectura:**

1. **Identificar el UUID de la partición:**

Es recomendable usar el UUID en lugar del nombre del dispositivo para evitar problemas si cambian las designaciones de los dispositivos.

```bash
blkid /dev/sdXn
```

• Esto devolverá una línea similar a:

```bash
/dev/sdXn: UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" TYPE="btrfs"
```
  

2. **Editar el archivo** `/etc/fstab`:

Abre el archivo /etc/fstab con un editor de texto, por ejemplo, vim.

```bash
vim /etc/fstab
```
  
3. **Añadir una línea para la nueva partición con opciones de montaje en** ro:
```bash
UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" /backup btrfs defaults,ro 0 2 
```

• UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx: Identificador único de la partición.
• /backup: Punto de montaje.
• btrfs: Sistema de archivos.
• defaults,ro: Opciones de montaje (defaults incluye opciones estándar y ro especifica modo de solo lectura). 
• 0 2: Opciones de dump y fsck 

> Monta todas las particiones especificadas en /etc/fstab sin reiniciar.

```bash
mount -a
```

• Confirma que la partición /backup esté montada en modo de solo lectura:

```bash
mount | grep /backup
```

• Deberías ver una línea que indica que /backup está montado con las opciones ro.


### **Backups completos**

> Para realizar un back up completo del directorio /root, utilizamos el comando tar, que permite empaquetar y opcionalmente comprimir archivos y directorios. Es fundamental que los nombres de los archivos de back up sean descriptivos e incluyan información sobre el contenido, la fecha y hora del back up, así como si el back up es completo o incremental. Esto facilita la gestión y restauración de los back ups .

  
**Incluir la Fecha Automáticamente en el Nombre del Archivo de Back up**

Para incluir automáticamente la fecha y hora en el nombre del archivo de back up, podemos utilizar el comando date dentro de una sustitución de comandos $(). Por ejemplo:

```bash
backup-etc-level0-$(date +%Y%m%d-%H%M).tar
```

  
Este comando generará un nombre de archivo con el formato `backup-etc-level0-202401131230.tar` si se ejecuta el 13 de enero de 2024 a las 12:30.


**Comando para Hacer una Copia Completa del Directorio /root**

Para crear una copia completa del directorio /root, utilizamos el siguiente comando tar:

```bash
tar -cvf /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar -C /root .
```

• tar: Comando para empaquetar archivos.
• -c: Crea un nuevo archivo tar.
• -v: Muestra el progreso en la terminal (modo verbose).
• -f: Especifica el nombre del archivo tar resultante.
• /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar: Ruta y nombre del archivo de back up, incluyendo la fecha y hora.
• -C 
• /root: Directorio que se va a hacer un back up.

**Compresión del Archivo de Back up**

Para comprimir el archivo de back up, se añade la opción -z al comando tar, que utiliza gzip para la compresión. El comando modificado sería: 

```bash
tar -cvfz /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar.gz /root
```

• -z: Comprime el archivo usando gzip.


**Consideraciones de Seguridad al Comprimir Archivos de Back up**

Aunque comprimir los archivos de back up reduce el espacio que ocupan y puede facilitar su transferencia, **no es recomendable en términos de seguridad** por las siguientes razones:

• **Exposición de Datos Sensibles:** La compresión no encripta los datos, lo que significa que cualquier persona con acceso al archivo comprimido puede extraer y leer su contenido.

• **Integridad de los Datos:** La compresión puede introducir vulnerabilidades si no se maneja correctamente, aunque esto es menos común.

• Tener que descomprimir i comprimir cada vez que se necesitan los datos **introduce mucho overhead** y puede hacer que el proceso tarde aún más.

**Excluir Archivos Específicos del Back up**

A veces, es necesario excluir ciertos archivos del back up completo. Para ello, se puede crear un archivo de exclusiones que liste los archivos o directorios a omitir. Por ejemplo, creamos un archivo llamado excludes.txt con el siguiente contenido:

```txt
/tmp
/bin
/sbin
```

**Comando para Crear el Archivo de Exclusiones:** 

```bash
echo -e "/tmp\n/bin\n/sbin" > /backup/excludes.txt
```


**Comando para Excluir Archivos en el Back up**

Para excluir los archivos listados en excludes.txt, se añade la opción --exclude-from al comando tar:

```bash
tar -cvf /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar --exclude-from=/backup/excludes.txt /root
```

• --exclude-from=/backup/excludes.txt: Especifica el archivo que contiene la lista de archivos/directorios a excluir.

**Verificación de la Integridad del back up con sha512sum**

Es importante verificar que los archivos de back up no hayan sido modificados después de su creación. Para ello, utilizamos sha512sum para generar una firma digital que asegura la integridad del archivo.

**Comando para Generar la Firma SHA512:**

```bash
sha512sum /backup/backup-root-level0-(date +%Y%m%d%H%M).tar > /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar.asc
  ```
  
**Desglose del Comando:**

• sha512sum /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar: Calcula el hash SHA512 del archivo de back up.

• >: Redirecciona la salida al archivo especificado.
• /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar.asc: Archivo donde se almacena la firma SHA512.

*Si quieres un archivo .asc con todos los sha512sum de los backups, haz append en vez de redireccionar la salida*

```bash
sha512sum /path/to/backup/file >> /path/to/signature.asc
```


**Respuestas a las Preguntas de 5.5.1**

1. **¿Cómo puedes incluir automáticamente la fecha en el nombre del archivo de back up?**

Utilizando el comando date dentro de una sustitución de comandos $(). Por ejemplo:
```bash
backup-etc-level0-$(date +%Y%m%d-%H%M).tar
```


2. **¿Qué comando has usado para hacer la copia completa del directorio** /root?

```bash
tar -cvf /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar /root
```


3. **Si queremos comprimir el archivo de back up, ¿qué opción debes añadir al comando** tar?
Añadir la opción -z para comprimir con gzip:

```bash
tar -cvfz /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar.gz /root
```  

4. **¿Por qué no es generalmente bueno en términos de seguridad comprimir el archivo de back up?**

• **Exposición de Datos Sensibles:** La compresión no encripta los datos, permitiendo que cualquier persona con acceso al archivo comprimido pueda extraer y leer su contenido.

• **Integridad de los Datos:** Aunque menos común, la compresión puede introducir vulnerabilidades si no se maneja correctamente.

• **Dependencia de Herramientas:** Requiere herramientas de descompresión compatibles durante la restauración.

5. **¿Qué comando has añadido al comando** tar **para excluir archivos?**

Añadir la opción --exclude-from especificando el archivo de exclusiones:

```bash
tar -cvf /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar --exclude-from=/backup/excludes.txt /root
```
  
6. **¿Cómo has usado el comando** sha512sum **para producir la firma SHA512?**

Generando el hash y redireccionándolo a un archivo con extensión .asc:

```bash
sha512sum /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar > /backup/backup-root-level0-$(date +%Y%m%d%H%M).tar.asc
```


### **Back ups Incrementales**

Un back up incremental captura únicamente los archivos que han cambiado desde el último back up (ya sea completo o incremental). Esto optimiza el espacio y el tiempo necesarios para realizar los back ups , especialmente en sistemas con grandes volúmenes de datos que cambian frecuentemente.

**Modificaciones Previas al back up Incremental**

Antes de realizar un back up incremental, es necesario modificar algunos archivos en el directorio /root:

• **Crear nuevos archivos y subdirectorios:**

```bash
mkdir /root/nuevo_directorio
touch /root/nuevo_directorio/nuevo_archivo.txt
```


• **Modificar el contenido de algunos archivos:**

```bash
echo "Contenido actualizado" >> /root/existente.txt
```

• **Usar el comando** touch **para cambiar la fecha de modificación de algunos archivos:**

``` bash
touch /root/existente.txt
```

  
**Realizar un back up Incremental con tar**

Para realizar un back up incremental, se utiliza la opción --newer de tar, que incluye únicamente los archivos modificados desde una fecha específica o desde la última modificación de un archivo de referencia.


**Ejemplo de Comando para back up Incremental:**

```bash
tar -cvf /backup/backup-root-level1-$(date +%Y%m%d%H%M).tar --newer="2024-01-13 12:30" /root
```

O poniendo directamente que los archivos se hayan modificado en el último x tiempo:

```bash
name=$(date '+%Y%m%d-%H%M') 
tar -zcvf /backup/"$name.tar.gz" --newer-mtime="24 hours ago" -C /etc .
```

*"X \[time_mesurement] ago", como "time_mesurement" puedes poner: second(s), minute(s), hour(s), day(s), month(s), year(s)... *

O utilizando un archivo de referencia:

```bash
tar -cvf /backup/backup-root-level1-$(date +%Y%m%d%H%M).tar --newer=/backup/backup-root-level0-202401131230.tar /root
```

**Generar Firma SHA512 para el back up Incremental**

```bash
sha512sum /backup/backup-root-level1-$(date +%Y%m%d%H%M).tar > /backup/backup-root-level1-$(date +%Y%m%d%H%M).tar.asc
```
  
**Respuestas a las Preguntas de 5.5.2**

1. **¿Qué comando has usado para hacer la copia incremental?**

```bash
tar -cvf /backup/backup-root-level1-$(date +%Y%m%d%H%M).tar --newer=/backup/backup-root-level0-202401131230.tar /root
  ```
  
2. **¿Qué problema potencial tiene el uso del archivo de back up completo para obtener la fecha del back up al hacer la copia incremental?**

El principal problema es que el proceso de back up completo puede llevar mucho tiempo, lo que puede generar discrepancias en la fecha si el back up incremental se realiza mientras el back up completo aún está en progreso. Además, si el back up completo falla o se interrumpe, la referencia para el back up incremental puede no ser precisa.

3. **¿Cómo puedes resolver este problema?**

Para solucionar este problema, se puede utilizar un archivo de referencia que se actualice solo cuando el back up completo se haya completado exitosamente. De esta manera, los back ups  incrementales siempre se basarán en una referencia estable y consistente.

**Realizar un Segundo back up Incremental**
Después de realizar más modificaciones en el directorio /root:
• **Crear nuevos archivos y subdirectorios:**

```bash
mkdir /root/otro_directorio
touch /root/otro_directorio/otro_archivo.txt
```
  
• **Modificar el contenido de algunos archivos:**

```bash
echo "Otro contenido actualizado" >> /root/existente.txt
```

• **Usar el comando** touch **para cambiar la fecha de modificación de algunos archivos:**

```bash
touch /root/existente.txt
```
  
• **Eliminar algunos de los archivos generados para el primer back up incremental:**

```bash
rm /root/nuevo_directorio/nuevo_archivo.txt
```

**Comando para el Segundo back up Incremental:** 
```bash
tar -cvf /backup/backup-root-level2-$(date +%Y%m%d%H%M).tar --newer=/backup/backup-root-level1-202401131245.tar /root
  ```
  

**Generar Firma SHA512 para el Segundo back up Incremental:**

```bash
sha512sum /backup/backup-root-level2-$(date +%Y%m%d%H%M).tar > /backup/backup-root-level2-$(date +%Y%m%d%H%M).tar.asc
```

  
4. **¿Cómo puedes verificar que el contenido del back up es el mismo que el directorio original?**
Comparando el contenido del back up con el directorio original utilizando herramientas como diff, o verificando la integridad con las firmas SHA512 previamente generadas.

5. **¿Cómo puedes verificar, usando el comando** sha512sum, la integridad del back up?

Calculando el hash SHA512 del archivo de back up y comparándolo con el hash almacenado en el archivo .asc. Por ejemplo:

```bash
sha512sum -c /backup/backup-root-level1-202401131245.tar.asc
```  
Si los hashes coinciden, la integridad del back up está asegurada.

  
**5.5.3 Restaurando un back up** 

La restauración de un back up implica descomprimir y extraer los archivos respaldados en su ubicación original. Es crucial restaurar los back ups  en el orden correcto para asegurar que las copias incrementales se apliquen adecuadamente sobre el back up completo.


**Simular Pérdida de Datos y Restauración**

1. **Renombrar el Directorio** /root **para Simular Pérdida de Datos:**
  
```bash
mv /root /root.old
```

2. **Restaurar el Directorio desde los back ups :**

Para restaurar completamente el directorio /root, se deben restaurar primero el back up completo y luego los back ups  incrementales en el orden en que fueron creados.

**Orden de Restauración:**
• Restaurar el back up completo (Nivel 0).
• Restaurar el primer back up incremental (Nivel 1).
• Restaurar el segundo back up incremental (Nivel 2).

3. **Comandos Utilizados para Restaurar los back ups :**
• **Restaurar el back up Completo:**

```bash
tar -xvf /backup/backup-root-level0-202401131230.tar -C /
```


• **Restaurar el Primer back up Incremental:**

```bash
tar -xvf /backup/backup-root-level1-202401131245.tar -C /  
```

• **Restaurar el Segundo back up Incremental:**  
```bash
tar -xvf /backup/backup-root-level2-202401131300.tar -C /

  ```
  
  4. **¿Qué ocurrió con los archivos que se habían eliminado antes del segundo back up incremental?**

Al restaurar los back ups  completos e incrementales, los archivos eliminados antes del segundo back up incremental no se restauran automáticamente, ya que los back ups  incrementales solo agregan o modifican archivos, pero no eliminan aquellos que ya fueron eliminados en el sistema original.

5. **¿Cómo puedes detectar que algunos archivos han sido eliminados? ¿Cuándo esos archivos serán restaurados desde los back ups ?**
• **Detección de Eliminaciones:**
Utilizando herramientas de comparación como diff para comparar el estado actual del directorio /root con el estado de los back ups  restaurados.
• **Restauración de Archivos Eliminados:**
Para restaurar archivos que fueron eliminados, se deben extraer específicamente desde el back up completo o desde el back up incremental donde fueron incluidos antes de ser eliminados.

**Restauración de un Fragmento del back up**

Para restaurar únicamente una subcarpeta específica del directorio /root, se puede utilizar la opción --extract con una ruta específica.
**Ejemplo de Comando para Restaurar una Subcarpeta:**

```bash
#para alistar el contenido sin descomprimir/desempaquetar:
tar -tf nombre.tar.gz
# una vez encontrado el nombre del subdirectorio, extrae solo ese haciendo:
tar -xvf nombre.tar.gz -C /root ./nombre_subdirectorio/
```

• -tf: Alistar archivos
• -xvf: Opciones para extraer, verbose, y especificar archivo.
• /backup/backup-root-level0-202401131230.tar: Archivo de back up desde el cual extraer.
• /root/subdirectorio: Subdirectorio específico que se desea restaurar.
• -C /: Directorio raíz donde se restaurará la subcarpeta.

### **5.6 Backups con rsync**

Hasta ahora, hemos almacenado los back ups  en la misma máquina que contiene los datos. Sin embargo, lo más común es tener varias máquinas para respaldar y almacenar las copias en una máquina central utilizando la red. 

Para ello, podemos usar el comando **rsync** -> permite copiar un directorio (o conjunto de archivos) a otro directorio a través de una conexión de red. 
**rsync** utiliza un algoritmo de suma de verificación eficiente para transmitir solo las diferencias entre los dos directorios, al mismo tiempo que comprime los archivos para una transmisión más rápida.

Esta herramienta permite copiar archivos desde o hacia un directorio ubicado en una máquina remota, o directorios de la misma máquina. Lo que no permite es copiar directorios entre dos máquinas remotas. Además, rsync permite copiar enlaces, dispositivos y preservar permisos, propietarios y grupos. También soporta listas de exclusión y conexiones remotas usando Secure Shell (SSH) entre otras posibilidades (para más información, consulte man rsync).

##### **5.6.1 Haciendo back ups  a Través de una Red**

Como se mencionó anteriormente, rsync puede respaldar una máquina remota. Esto se puede hacer con rsh, o poniendo rsync en modo servidor, pero puede ser peligroso porque una máquina local en la red podría estar capturando los datos de la conexión. Para resolver estos problemas, rsync permite conexiones seguras usando ssh.

**Pasos Requeridos para Instalar y Activar el Servidor SSH**

1. **Instalar el Servidor SSH:**

En distribuciones basadas en Debian:

```bash
sudo apt-get update
sudo apt-get install openssh-server
```
  

2. **Iniciar y Habilitar el Servicio SSH:**

```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

3. **Verificar que el Servidor SSH Está Corriendo:**

```bash
sudo systemctl status ssh
```

**Habilitar el Acceso del Usuario Root a Través de SSH**

Por razones de seguridad, el acceso del usuario root a través de SSH está deshabilitado por defecto. Para habilitarlo, sigue estos pasos:

1. **Editar el Archivo de Configuración de SSH:**

```bash
sudo nano /etc/ssh/sshd_config
```
  
2. **Buscar la Línea que Contiene** PermitRootLogin:
3. **Descomentar la Línea y Cambiar su Valor a** yes:

```bash
#PermitRootLogin prohibit-password
PermitRootLogin yes
```


4. **Reiniciar el Servicio SSH para Aplicar los Cambios:**
  
```bash
sudo systemctl restart ssh 
```
  
**Nota:** Habilitar el acceso del usuario root a través de SSH puede representar un riesgo de seguridad. Se recomienda utilizar claves SSH en lugar de contraseñas y restringir el acceso por IP si es posible.
  

Para realizar back ups  completos utilizando rsync, seguiremos estos pasos:
##### **5.6.2 Haciendo backups completos**

1. **Crear un Directorio para los back ups  en la Partición** `/backup`:

```bash
mkdir -p /backup/rsync-backup/
```


2. **Ejecutar el Comando** `rsync`:

**Comando Proporcionado:**

```bash
rsync -avz /root -e ssh root@localhost:/backup/rsync-backup/  
```

• -a (**Archive**): Modo de archivo. Equivale a -rlptgoD. Preserva enlaces simbólicos, permisos, propietarios, grupos, tiempos y dispositivos.
• -v (**Verbose**): Modo verbose. Muestra información detallada sobre el proceso de sincronización.
• -z (**Compress**): Comprime los datos durante la transferencia para acelerar la transmisión a través de la red.

**Crear un Archivo en /root y Realizar el Mismo Comando rsync**

1. **Crear un Archivo Nuevo:**  
```bash
touch /root/nuevo_archivo.txt
```

2. **Ejecutar el Comando** rsync **de Nuevo:**

```bash
rsync -avz /root -e ssh root@localhost:/backup/rsync-backup/
```


3. **Eliminar el Archivo y Ejecutar** rsync **Nuevamente:**

```bash
rm /root/nuevo_archivo.txt
rsync -avz /root -e ssh root@localhost:/backup/rsync-backup/
  ```
  

**¿Qué Ocurrió con el Archivo Eliminado?**

El archivo eliminado (nuevo_archivo.txt) ya no existe en el directorio /root, pero **no se elimina automáticamente del directorio de back up** /backup/rsync-backup/. Esto se debe a que, por defecto, rsync solo actualiza o agrega archivos, pero no elimina aquellos que han sido eliminados en el directorio fuente.

**¿Qué Opción de rsync Permite una Sincronización Exacta de los Dos Directorios?**
La opción --delete permite que rsync elimine en el directorio de destino aquellos archivos que ya no existen en el directorio fuente, logrando una sincronización exacta.

**Comando con la Opción** --delete:

```bash
rsync -avz --delete /root -e ssh root@localhost:/backup/rsync-backup/
```

**¿Cómo Puedes Hacer una Copia de Todos los Archivos en el Directorio /root Excepto Aquellos que Tienen una Extensión .txt?**

Utilizando la opción --exclude para excluir archivos con la extensión .txt.

**Comando:**  

```bash
rsync -avz --exclude='*.txt' /root -e ssh root@localhost:/backup/rsync-backup/
```

**¿Cuál es la Diferencia entre rsync /source /destination y rsync /source /destination/?**

Con /destination/, si /destination ya existe, rsync creará un subdirectorio llamado source dentro de /destination. Por ejemplo, los archivos de /source se copiarán a /destination/source/. Si no, rsync copia /source directamente dentro de /destination sin crear un subdirectorio adicional. Es decir, los archivos de /source se copiarán directamente a /destination/.

##### **5.6.3 Haciendo back ups  Incrementales Inversos**

Como se vio en la sección anterior, cada vez que haces una copia y sincronizas, el directorio donde tienes el espejo es exactamente igual al directorio fuente. Esto puede ser un problema en algunas situaciones, ya que no permite controlar los cambios realizados en los archivos. Para resolver esto, puedes usar las opciones --backup y --backup-dir de rsync. Los back ups  generados con estas opciones se llaman **inversos** porque la copia completa es la más reciente, a diferencia de tar.
  
**Script Simple para Hacer back ups  Incrementales Inversos con rsync**

  
```bash
#!/bin/bash
_# Directorio fuente_

SOURCE_DIR=/root
_# Directorio de destino_

DEST_DIR=/backup/rsync-backup/

_# Archivo de exclusiones: lista de archivos a excluir_

EXCLUDES=/backup/excludes.txt

_# Nombre de la máquina de back up_

BSERVER=localhost  
_# Fecha para el back up: año, mes, día, hora, minuto, segundo_

BACKUP_DATE=$(date +%Y%m%d%H%M%S)


_# Opciones para rsync_

OPTS="--ignore-errors --delete-excluded --exclude-from=$EXCLUDES \ --delete --backup --backup-dir=$DEST_DIR/backups/$BACKUP_DATE -av"

_# Transferencia real_

rsync $OPTS $SOURCE_DIR root@$BSERVER:$DEST_DIR/complet
```
  
• SOURCE_DIR: Directorio que se va a respaldar.
• DEST_DIR: Directorio donde se almacenarán los back ups .
• EXCLUDES: Archivo que contiene la lista de archivos/directorios a excluir del back up.
• BSERVER: Nombre o dirección IP de la máquina de back up.
• BACKUP_DATE: Fecha y hora actual en formato YYYYMMDDHHMMSS.
• OPTS: Opciones adicionales para rsync.

• **Opciones de** `rsync`:
• --ignore-errors: Ignora errores durante la transferencia.
• --delete-excluded: Elimina archivos excluidos del destino.
• --exclude-from: Especifica el archivo de exclusiones.
• --delete: Elimina archivos en el destino que ya no existen en la fuente.
• --backup: Realiza back ups  de los archivos que se van a sobrescribir o eliminar.
• --backup-dir: Directorio donde se almacenarán los archivos respaldados.
• -a: Modo archivo.
• -v: Modo verbose.

**Proceso de back up**
1. **Crear un Archivo en el Directorio Fuente y Sincronizar con el Script:**

```bash
touch /root/nuevo_archivo_inverso.txt
./script_back up.sh
```

2. **Modificar el Archivo Nuevo y Sincronizar de Nuevo:**

```bash
echo "Contenido actualizado" >> /root/nuevo_archivo_inverso.txt

./script_back up.sh
```

3. **Eliminar el Archivo y Sincronizar de Nuevo:**

```bash
rm /root/nuevo_archivo_inverso.txt
./script_back up.sh
```

**¿Qué Ocurre con el back up Cuando el Archivo Nuevo es Modificado?**

Cuando el archivo nuevo (nuevo_archivo_inverso.txt) es modificado y se ejecuta nuevamente el script de rsync, el archivo actualizado se copia al directorio de destino (/backup/rsync-backup/complet/). Además, la versión anterior del archivo se mueve al directorio de back ups  (/backup/rsync-backup/backups/20240113130000/), preservando así las versiones anteriores.

**¿Qué Ocurre Cuando el Archivo es Eliminado?**

Al eliminar el archivo (nuevo_archivo_inverso.txt) y ejecutar nuevamente el script de rsync, el archivo es eliminado del directorio de destino (/backup/rsync-backup/complet/). Sin embargo, una copia del archivo eliminado se almacena en el directorio de back ups  (/backup/rsync-backup/backups/20240113130000/), permitiendo su recuperación si es necesario.

##### **5.6.4 Backups con Snapshots**
  
Una posibilidad que ofrece rsync es realizar back ups  incrementales donde, utilizando las propiedades de los hard link, las copias incrementales parecen copias completas. Esto se logra aprovechando que los hard links permiten que múltiples nombres de archivo apunten al mismo inodo, lo que facilita la creación de snapshots que consumen menos espacio en disco.

**Hard links** *

El nombre de archivo no representa el archivo en sí mismo, es solo un hard link al inodo. Esto permite que un archivo (inode) tenga más de un hard link. Por ejemplo, si tienes un archivo llamado file_a, puedes crear un enlace a él llamado file_b:

```bash
ln file_a file_b
```

Usando el comando stat es posible saber cuántos hard links  tiene un archivo:

```bash
stat file_a
```
  

1. **¿Cómo puedes detectar si** file_a **y** file_b **pertenecen al mismo inodo?**

Utilizando el comando stat en ambos archivos y comparando el número de inodo.

```bash
stat file_a
stat file_b
```

Si ambos muestran el mismo número de inodo (Inode:), entonces pertenecen al mismo inodo.

  
2. **¿Qué ocurre con** file_b **si hay cambios en el contenido de** file_a?

Dado que ambos archivos apuntan al mismo inodo, cualquier cambio en el contenido de file_a también se refleja en file_b, ya que ambos son el mismo archivo a nivel de sistema de archivos. Cambian las fechas de ACCESS, CHANGE y MODIF.

3. **¿Qué ocurre con** file_b **si hay cambios en los permisos de** file_a?

Ambos tendrán los mimos permisos.

4. **¿Qué ocurre con** file_b **si copias otro archivo, sobrescribiendo** file_a **con** cp file_c file_a?

Si sobrescribes file_a con cp file_c file_a, file_a ahora apuntará a un nuevo inodo que contiene el contenido de file_c. Sin embargo, file_b seguirá apuntando al inodo original de file_a, manteniendo su contenido previo.

5. **¿Y si lo sobrescribes con la opción** --remove-destination **de** cp?

Usar cp --remove-destination file_c file_a primero elimina file_a y luego crea una nueva copia con el contenido de file_c. Esto rompe el hard link  entre file_a y file_b. Ahora, file_a apunta al nuevo contenido, mientras que file_b sigue apuntando al inodo original con el contenido previo.

6. **¿Y qué ocurre con** file_b **si** file_a **es eliminado?**

Si eliminas file_a (rm file_a), file_b seguirá existiendo y apuntando al mismo inodo. El archivo no se elimina del sistema de archivos hasta que se eliminen **todos** los hard links  que apuntan a él. Por lo tanto, file_b mantendrá el contenido original incluso después de eliminar file_a.

###### Back ups tipo Snapshot

Los back ups  tipo snapshot permiten crear múltiples copias de seguridad que parecen copias completas de un sistema de archivos sin requerir todo el espacio en disco necesario para almacenar todas las copias. Esto se logra combinando los comandos rsync y cp -al, aprovechando las propiedades de los enlaces duros para minimizar el uso de espacio.

El proceso general para crear back ups  snapshot utilizando cp y rsync es el siguiente:
```bash
_# Eliminar la copia más antigua_
rm -rf backup.3
_# Mover las copias existentes una posición hacia atrás_
mv backup.2 backup.3
mv backup.1 backup.2
_# Crear una nueva copia utilizando enlaces duros_
cp -al backup.0 backup.1

_# Sincronizar el directorio fuente con la copia más reciente_
rsync -a --delete source_directory/ /backup.0/
  ```
  
1. **Eliminar la Copia Más Antigua:**

```bash
rm -rf backup.3
```

Elimina la copia de back up más antigua para hacer espacio para la nueva copia.
  2. **Mover las Copias Existentes:**

```bash
mv backup.2 backup.3
mv backup.1 backup.2
  ```
  
Desplaza las copias de back up actuales hacia posiciones más antiguas.

3. **Crear una Nueva Copia con Enlaces Duros:**

```bash
cp -al backup.0 backup.1
```

Crea una nueva copia (backup.1) que comparte los mismos inodos que backup.0, utilizando enlaces duros (-l) y preservando los atributos (-a).

4. **Sincronizar con** rsync:

```bash
rsync -a --delete source_directory/ /backup.0/
```
  
Sincroniza el directorio fuente con backup.0, copiando solo las diferencias y eliminando archivos que ya no existen en la fuente.
  
**Ventajas y Desventajas**

• **Ventajas:**
• **Eficiencia en el Uso de Espacio:** Las copias incrementales solo almacenan las diferencias, reduciendo el espacio necesario.
• **Simulación de Copias Completas:** Las copias snapshot parecen copias completas, facilitando la restauración.
• **Desventajas:**
• **Permisos y Propiedades:** Las copias de back up de días anteriores heredan los permisos y propiedades del back up actual, lo que puede no ser deseable.


**Uso de la Opción --link-dest de rsync**
Para optimizar el proceso y preservar permisos y propietarios de copias anteriores, se puede utilizar la opción --link-dest de rsync, eliminando la necesidad del comando cp -al.

**Comandos Actualizados:**
```bash  
_# Eliminar la copia más antigua_
rm -rf backup.3
_# Mover las copias existentes una posición hacia atrás_
mv backup.2 backup.3
mv backup.1 backup.2
mv backup.0 backup.1

_# Sincronizar con `rsync` utilizando `--link-dest`_
rsync -a --delete --link-dest=../backup.1 source_directory/ /backup.0/
```

• --link-dest=../backup.1**:** Indica a rsync que use backup.1 como referencia para enlaces duros. Los archivos que no han cambiado se enlazan al back up anterior, optimizando el uso de espacio y preservando permisos y propietarios.

**Script para back ups  Snapshot**

A continuación, se presenta un script básico para realizar back ups  snapshot utilizando rsync con la opción --link-dest. Este script debe ser adaptado según las necesidades del sistema.
  
```bash
#!/bin/bash
_# Sección: Ubicaciones de Archivos_
SOURCE_DIR=/root
DEST_DIR=/backup/rsync-backup
EXCLUDES=/backup/excludes.txt
BSERVER=localhost
BACKUP_DATE=$(date +%Y%m%d%H%M%S)

_# Opciones para rsync_
OPTS="--ignore-errors --delete-excluded --exclude-from=$EXCLUDES \
--delete --backup --backup-dir=$DEST_DIR/backups/$BACKUP_DATE -av"

_# Transferencia real usando `--link-dest`_
rsync -a --delete --link-dest=../backup.1 $SOURCE_DIR/ $DEST_DIR/backup.0/
```


• SOURCE_DIR: Directorio que se respalda (/root).
• DEST_DIR: Directorio donde se almacenan los back ups  (/backup/rsync-backup).
• EXCLUDES: Archivo que contiene la lista de archivos/directorios a excluir.
• BSERVER: Máquina de back up (en este caso, localhost).
• BACKUP_DATE: Fecha y hora actual para identificar el back up.

• **Opciones de** rsync:

	• --ignore-errors: Ignora errores durante la transferencia.
	• --delete-excluded: Elimina archivos excluidos del destino.
	• --exclude-from: Especifica el archivo de exclusiones.
	• --delete: Elimina archivos en el destino que ya no existen en la fuente.
	• --backup: Realiza back ups  de los archivos que se van a sobrescribir o eliminar.
	• --backup-dir: Directorio donde se almacenarán los archivos respaldados.
	• -a: Modo archivo.
	• -v: Modo verbose.
	• --link-dest=../backup.1: Utiliza backup.1 como referencia para enlaces duros.

**Respuestas a las Preguntas de 5.6.5**

1. **¿Cómo es el comando** rsync **en el script para hacer las copias snapshot?**

El comando rsync en el script utiliza la opción --link-dest para crear enlaces duros con el back up anterior, optimizando el uso de espacio y preservando permisos y propietarios.

```bash
rsync -a --delete --link-dest=../backup.1 /root/ /backup/rsync-backup/backup.0/
```
  
2. **¿Qué ocurre con el back up después de la ejecución del script?**
Cada vez que se ejecuta el script:
• La copia más antigua (backup.3) se elimina.
• Las copias existentes se mueven una posición hacia atrás (backup.2 a backup.3, backup.1 a backup.2, backup.0 a backup.1).
• Se crea una nueva copia (backup.0) que parece una copia completa pero utiliza enlaces duros para compartir archivos inalterados con backup.1.
Esto permite tener cuatro copias de back up que parecen completas pero que ocupan espacio equivalente a la suma del directorio fuente más los cambios en los últimos tres días.

3. **¿Cuál es el tamaño del directorio** /backup.0 y de otros directorios de back up?

• /backup.0: Tamaño equivalente al directorio fuente actual más los cambios recientes.

• **backup.1**, **backup.2**, **backup.3**: Tamaño mínimo ya que comparten archivos inalterados mediante enlaces duros. Solo aumentan en tamaño si hay nuevos cambios en los archivos.

4. **¿Dónde está la información más reciente después de una restauración?**

La información más reciente se encuentra en el directorio backup.0, ya que es la copia sincronizada más reciente del directorio fuente.

5. **¿Qué comando se puede usar para recuperar los datos?**

Para restaurar los datos desde el back up más reciente (backup.0), se puede utilizar el comando rsync de la siguiente manera:

```bash
rsync -a --delete /backup/rsync-backup/backup.0/ /root/
  ```
  

• -a: Modo archivo, preserva permisos, propietarios, grupos, etc.
• --delete: Elimina archivos en el destino que no existen en el origen.
• /backup/rsync-backup/backup.0/: Directorio de back up más reciente.
• /root/: Directorio de destino donde se restaurarán los archivos.


# Practica 6 ASO

Ésta práctica consiste en inciarnos al cloud público (AWS). Ésta práctica se divide en tres sub apartados:

## Poner en marcha un sitio de Wordpress en la nube

### 1. Crear una base de datos MySql con Amazon RDS

![[Pasted image 20241214165911.png]]![[Pasted image 20241214170908.png]]

![[Pasted image 20241214170948.png]]
![[Pasted image 20241214171016.png]]
![[Pasted image 20241214171040.png]]
![[Pasted image 20241214171112.png]]

### Crear una instancia EC2

![[Pasted image 20241214172703.png]]

![[Pasted image 20241214172733.png]]![[Pasted image 20241214172824.png]]
![[Pasted image 20241214172754.png]]

![[Pasted image 20241214172828.png]]

![[Pasted image 20241214172855.png]]
![[Pasted image 20241214172922.png]]
![[Pasted image 20241214172946.png]]
![[Pasted image 20241214173012.png]]


### Configurar tu base de datos RDS

![[Pasted image 20241214173151.png]]
![[Pasted image 20241214173215.png]]
![[Pasted image 20241214173334.png]]

![[Pasted image 20241214173435.png]]

### Configurar WordPress en EC2

![[Pasted image 20241214174055.png]]

![[Pasted image 20241214174644.png]]

> **OJO:** DB_HOST se refiere al Endpoint:

![[Pasted image 20241214181804.png]]


![[Pasted image 20241214174708.png]]


![[Pasted image 20241214180053.png]]

### Crear una página web simplona sin DataBase

*Pregunta del 23-24 q2*
1. Ves a la web de AWS awsacademy.instructure.com
2. Inicia sessión y launchea el "Learner Lab"
3. Haz una nueva instancia de EC2 con Amazon linux
4. Selecciona la instance type que te diga el enunciado.
5. Todo default 
6. Llámale como quieras

7. Crea un nuevo security group, y añade estas Inbound Rules:
	- Permitir tráfico HTTP (80), source: la que te diga el enunciado
	- Permitir tráfico SSH (22), source: tu IP
8. Crea tu key pair y descárgalo
9. Dale a launch

10. Abre la terminal de Linux del ordenador y haz:
```bash 
chmod 400 Descarregues/clau-examen.pem
ssh -i Desscarregues/clau-examen.pem ec2-user@<ip-Publica-ec2>
```
*La IP pública la puedes encontrar haciendo click sobre esta instància en 2nda col*
11. Deberías estar en la terminal de la instancia. Ejecuta las siguientes comandas:
```bash
# Actualiza paquetes
sudo yum update -y
# Instala apache
sudo yum install -y httpd
# Inicia apache
sudo systemctl start httpd
sudo systemctl enable httpd
```
12. Con el navegador, escribe la IP pública en la barra y mira si está activo.
13. Si esta activo crea el archivo html y pega el código que te dan en el enunciado.
```bash
sudo nano /var/www/index.html
```

## Amazon S3 (Amazon Simple Storage Service)*
 ![[Pasted image 20241214195351.png]]

![[Pasted image 20241214195414.png]]
![[Pasted image 20241214195445.png]]

![[Pasted image 20241214195509.png]]

![[Pasted image 20241214195534.png]]

![[Pasted image 20241214195559.png]]

![[Pasted image 20241214195638.png]]

![[Pasted image 20241214195655.png]]

![[Pasted image 20241214195709.png]]

![[Pasted image 20241214195734.png]]

![[Pasted image 20241214195751.png]]
![[Pasted image 20241214195806.png]]


## Lambda functions

> Servicio en la nube basado en funciones y que elimina la necesidad de levantar una infraestructura complexa.
> 
![[Pasted image 20241214203616.png]]


![[Pasted image 20241214203639.png]]


![[Pasted image 20241214203658.png]]

 ![[Pasted image 20241215123253.png]]