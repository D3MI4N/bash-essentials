# Guia de comandos básicos para bash

**DISCLAIMER**: la idea no es que se sienten a aprender los comandos que les explique, a la larga eso no les va a servir. Peguenle una leida y tenganlo como una referencia. En el momento que necesitan usar un comando, vienen y lo buscan. Con el tiempo de usar la consola les van a empezar a salir naturalmente.

**DISCLAIMER 2**: yo estoy acostumbrado a trabajar en Linux. Bash es bash y es igual tanto en Linux como en macOS, pero puede ser que exista alguna diferencia con algún comando en macOS a como yo lo explique acá (me sorprendería que pasara igualmente, especialmente para estos comando básicos). Cualquier cosa, el comando `man` (de 'manual', explicado más adelante, es su amigo).

# Generalidades

### Argumentos de un comando

Muchos comandos en bash suelen llevar parámetros o argumentos; a veces obligatorios, a veces opcionales. Esos parámetros se escriben después del comando en sí y, generalmente, después de las opciones extra que tenga el comando (vamos a hablar de las opciones en el apartado siguiente).

Ejemplo:

* El comando `ls` permite listar archivos dentro de una carpeta. Se puede ejecutar:
    1. Sin parámetros, escribiendo solo `ls`. En este caso, lista los archivos de la carpeta de trabajo actual (current working directory).
    2. Pasandole una carpeta o archivo como parámetro. `ls /home/ppaglilla` lista los archivos de la carpeta '/home/ppaglilla'.
    3. A ambas opciones anteriores se les pueden agregar opciones del comando. Una es la opción `-l` (explicada más adelante de `ls`). Podriamos reeplazar el comando del punto 1 por `ls -l` y el comando del punto 2 por `ls -l /home/ppaglilla`.

### Opciones y flags

La gran mayoría de los comandos en bash tiene configuraciones opcionales en la forma de flags.

Los flags generalmente se escriben:
* Con un guión y una letra. Ejemplo: `ls -a` (lista archivos, incluyendo archivos ocultos).
* Con dos guiones y una palabra (version extendida). Ejemplo: `ls --all` (equivalente a `ls -a`).

A veces, los flags pueden llevar parámetros extra. Por ejemplo, en el comando `tail`. `tail` muestra las últimas lineas de un archivo y se usa de la forma `tail mi-archivo.txt`. Por defecto muestra las últimas 10 lineas del archivo. Suponiendo que quisiera mostrar las últimas 20 lineas del archivo, podría ejecutar `ls -n 20 mi-archivo.txt`. El flag `-n` me permite especificar la cantidad de lineas que quiero mostrar, el 20 es el parámetro para el flag con el cual indico dicha cantidad de lineas.

Los comandos suelen tener muchas opciones para usar. Yo voy a mostrar las más comunes.

### Manuales

Existe un comando llamado `man` que permite mostrar el manual de un comando en particular. Podemos usarlo de la forma `man COMANDO`.

**Ejemplo:** ejecutar el comando `man ls`, muestra el manual para el comando `ls`.

# Comandos

## Manejo de archivos y carpetas

### ls

`ls` (list) permite listar carpetas y archivos. Sus opciones permiten, además; cosas como mostrar archivos ocultos, mostrar información de los archivos además de sus nombres, ordenar los archivos, listar de forma recursiva, etc.

**Uso:** `ls [OPCIONES] [ARCHIVOS O CARPETAS]`

**Opciones:**

* `-l`: muestra información extra de los archivos. Incluye tamaño del archivo, permisos, usuario dueño, ultima fecha de modificación y otros detalles.
* `-a` o `--all`: incluye archivos ocultos en el listado.
* `-h` o `--human-readable`: cuando se usa `-l`, escribe el tamaño de los archivos en forma legible (eg: 1K (1 kilobyte), 234M (234 megabytes), 2G (2 gigabytes)). Por defecto el tamaño se escribe en bytes.
* `-S`: ordenar por tamaño de archivo descendentemente.

**Ejemplos:**:

* `ls`: lista los archivos de la carpeta de trabajo actual (current working directory)
* `ls -l`: lista los archivos de la carpeta de trabajo actual, incluyendo información adicional.
* `ls -l -a` o `ls -la`: lista los archivos de la carpeta de trabajo actual, incluyendo información adicional y archivos ocultos.
* `ls mi-carpeta`: lista los archivos de la carpeta 'mi-carpeta'.
* `ls -la mi-carpeta`: lista los archivos de la carpeta 'mi-carpeta', incluyendo archivos ocultos e información adicional.
* `ls -l mi-archivo`: muestra información del archivo 'mi-archivo' (tamaño, permisos, etc).

### cd

`cd` (change directory) permite cambiar el current working directory a un directorio distínto.

**Uso:** `ls [CARPETA]`

Para especificar la carpeta a la que se quiere cambiar, se pueden especificar dos tipos de ruta:

* Absoluta: especificando la ruta completa de la carpeta. Por ejemplo: `cd /home/ppaglilla/Projects`
* Relativa: especificando la ubicación de la carpeta a partir del current working directory actual. Suponiendo que mi current working directory fuera '/home/ppaglilla', `cd Projects` es equivalente a `cd /home/ppaglilla/Projects`.

Siempre que tengamos que referenciar archivos o carpetas, se va a poder hacer de esas dos formas.

Además, existe una carpeta especial dentro de todos los directorios en los sistemas UNIX llamada '..'. Esta es una referencia al directorio padre del actual. Suponiendo que mi current working directory es '/home/ppaglilla'; puedo usar `cd ..` para subir una carpeta, es decir, para cambiar el working directory a '/home'.

**Ejemplos:**

* `cd mi-carpeta`: cambia a la carpeta 'mi-carpeta' dentro del actual working directory
* `cd mi-carpeta/mi-otra-carpeta`: igual al ejemplo anterior, pero bajando dos niveles. Cambia a la carpete 'mi-otra-carpeta', que se encuentra dentro de 'mi-carpeta', que a su vez está en el working directory actual.
* `cd /home/ppaglilla/Projects`: cambia a la carpeta '/home/ppaglilla/Projects' usando una ruta absoluta (no importa cual es mi working directory actual).
* `cd ..`: sube una carpeta.
* `cd`: usado solo, cambia al directorio home del usuario actual.

### pwd

`pwd` (present working directory) muestra por pantalla el current working directory.

### mkdir

`mkdir` (make directory) crea una o varias carpetas.

**Uso:** `mkdir CARPETAS`

Al igual que para referenciar carpetas en `cd`, podemos usar rutas absolutas o relativas.

**Ejemplos:**

* `mkdir mi-carpeta`: crea la carpeta 'mi-carpeta' en el current working directory.
* `mkdir /home/ppaglilla/digitas`: crea una carpeta llamada 'digitas' en el directorio '/home/ppaglilla'.

### cp

`cp` (copy) permite copiar archivos

**Uso:** `cp [OPCIONES] ORIGEN DESTINO`

**Opciones:**

* `-r` o `--recursive`: copia de forma recursiva, necesario para copiar carpetas.

**Ejemplos:**

* `cp archivo.py mi-carpeta/`: copia el archivo 'archivo.py' a la carpeta 'mi-carpeta'.
* `cp archivo.py mi-carpeta/nombre-cambiado.py`: copia el archivo 'archivo.py' a 'mi-carpeta', pero cambiando el nombre de la copia a 'nombre-cambiado.py'
* `cp archivo1.txt archivo2.txt mi-carpeta/`: copia ambos archivos .txt a la carpeta 'mi-carpeta'
* `cp -r una-carpeta/ otra-carpeta/`: copia la carpeta 'una-carpeta' con todos sus contenidos a 'otra-carpeta'.

### mv

`mv` (move) permite mover archivos. Se usa exactamente igual que `cp`.

**Uso:** `mv [OPCIONES] ORIGEN DESTINO`

**Opciones:**

* `-r` o `--recursive`: mueve de forma recursiva, necesario para mover carpetas.

**Ejemplos:**

* `mv archivo.py mi-carpeta/`: mueve el archivo 'archivo.py' a la carpeta 'mi-carpeta'.
* `mv archivo.py otro-nombre.py`: cambia el nombre de 'archivo.py' a 'otro-nombre.py'.
* `mv archivo.py mi-carpeta/nombre-cambiado.py`: mueve el archivo 'archivo.py' a 'mi-carpeta', cambiandole el nombre a 'nombre-cambiado.py'
* `mv archivo1.txt archivo2.txt mi-carpeta/`: mueve ambos archivos .txt a la carpeta 'mi-carpeta'
* `mv -r una-carpeta/ otra-carpeta/`: mueve la carpeta 'una-carpeta' con todos sus contenidos a 'otra-carpeta'.

### rm

`rm` (remove) borra archivos.

**Uso:** `rm ARCHIVOS`

**Opciones (usar con cuidado!!):**:

* `-r` o `--recursive`: borra de forma recursiva, necesario para borrar carpetas.
* `-f` o `--force`: fuerza el borrado de los archivos.

**Ejemplos:**

* `rm archivo.txt`: borra el archivo 'archivo.txt'
* `rm -r carpeta`: borra la carpeta 'carpeta'

### nano

`nano` es un editor de texto de consola. Util si se quiere editar algo rápido sin salir de la consola.

**Uso:**: `nano ARCHIVO`

Si el archivo ya existe, lo abre para editar. Si el archivo no existe, lo crea en blanco.

Una vez dentro de nano, usar:

* `CTRL + O` y después `ENTER` para guardar
* `CTRL + X` para salir

**Ejemplos:**:

`nano script.py`: abre el archivo 'script.py' para editar. Si no existe, lo crea.

### cat

`cat` muestra los contenidos de un archivo en la consola. Util para ver rápido archivos de texto chicos.

**Uso:**: `cat ARCHIVO`

**Ejemplos:**:

`cat script.py`: muestra el contenido de 'script.py' en la consola.

### less

`less` permite ver los contenido de un archivo de una forma más amigable que `cat`. Permite scrollear el archivo.

**Uso:**: `less ARCHIVO`

**Ejemplos:**:

`less script.py`: muestra el contenido de 'script.py' en la consola.

### head

`head` muestra las primeras lineas de un archivo de texto. Por defecto muestra 10 lineas.

**Uso:** `head ARCHIVO`

**Opciones:**:

* `-n CANTIDAD`: muestra `CANTIDAD` de lineas en vez de mostrar 10.

**Ejemplos:**

* `head archivo.txt`: muestra las primeras 10 lineas de 'archivo.txt'
* `head -n 20 archivo.txt`: muestra las primeras 20 lineas de 'archivo.txt'

### tail

`tail` muestra las ultimas lineas de un archivo de texto. Por defecto muestra 10 lineas.

**Uso:** `tail ARCHIVO`

**Opciones:**:

* `-n CANTIDAD`: muestra `CANTIDAD` de lineas en vez de mostrar 10.
* `-f` o `--follow`: muestra las ultimas lineas del archivo, actualizandose si se escribe en el archivo mientras `tail` sigue abierto. Util para ver archivos de log mientras se escriben. Terminar la ejecución con `CTRL + C`.

**Ejemplos:**

* `tail archivo.txt`: muestra las últimas 10 lineas de 'archivo.txt'
* `tail -n 20 archivo.txt`: muestra las últimas 20 lineas de 'archivo.txt'
* `tail -f archivo.txt`: muestra la últimas 10 lineas de 'archivo.txt', actualizandose si se escribe en el archivo.

---

