## PARTICIONES EN LINUX
- Crear una particion primaria y 5 logicas.

- Una vez creadas, particionadas y montadas debe configurarse el sistema para que se monten
automáticamente al arrancar todas las particiones en diferentes carpetas en /mnt, por
ejemplo: /mnt/particion1

Para crear una partición primaria y cinco particiones lógicas en un disco nuevo en un servidor Linux, se puede utilizar una herramienta de particionamiento como "fdisk" o "parted". Una vez creadas las particiones, se deben montar en las carpetas deseadas en /mnt utilizando el comando "mount". Para que estas particiones se monten automáticamente al iniciar el sistema, se deben añadir las entradas correspondientes al archivo "/etc/fstab". Por último, se puede instalar un administrador web del servidor como "Webmin" para visualizar los datos de las particiones a través de una interfaz web.

### ¿QUÉ ES FDISK?
`"fdisk"`  es una herramienta de línea de comandos que se utiliza para crear, modificar y eliminar particiones en disco. Cuando se inicia "fdisk" para un disco específico, se entra en una interfaz interactiva que permite realizar diferentes operaciones.

### OPCIONES DE OPERACIONES CON FDISK:
Algunas de las opciones más comunes que se pueden utilizar en "fdisk" son:

- `n`: utilizado para crear una nueva partición. Puede especificar si se trata de una partición primaria o lógica y el número de partición.

- `p`: utilizado para mostrar el tablero de particiones existentes.

- `d`: utilizado para eliminar una partición existente.

- `t`: utilizado para cambiar el tipo de una partición existente.

- `w`: utilizado para guardar los cambios y salir de "fdisk".

- `q`: utilizado para salir de "fdisk" sin guardar los cambios.
### PASO 1:
#### Iniciar el Disco

Iniciar `fdisk` para el disco nuevo:
```bash
sudo fdisk /dev/sdb
```

### PASO 2: 
#### Crear Particion Primaria

Crear una partición primaria utilizando la opción `n`:
```bash
n
p
1
```
### PASO 3:
#### Crear Particiones Lógicas
Crear cinco particiones lógicas utilizando la opción `n` y especificando la opción `l` para indicar que se trata de una partición lógica:

- ***Primera Particion lógica:***
```bash
n
l
2
```
\
&nbsp;

- ***Segunda Particion lógica:***
```bash
n
l
3
```
\
&nbsp;

- ***Tercera Particion lógica:***
```bash
n
l
4
```
\
&nbsp;
- ***Cuarta Particion lógica:***
```bash
n
l
5

```
\
&nbsp;
- ***Quinta Particion lógica:***
```bash
n
l
6
```
\
&nbsp;
En este ejemplo primero se inicia **fdisk** para el disco `/dev/sdb`, luego se crea una partición primaria con número 1 utilizando las opciones `n` y `p`, y se crean tres particiones lógicas con números `2, 3, 4 y 5` utilizando las opciones `n` y `l`, y al final se guardan los cambios con `w`.
\
&nbsp;\
&nbsp;
### PASO 4:
#### Guardar Cambios
Guardar los cambios y salir de `fdisk`:
```bash
w
```
\
&nbsp;
### PASO 5:
- Una vez creadas las particiones, se deben montar en las carpetas deseadas en /mnt. Por ejemplo, si queremos montar la partición primaria en /mnt/particion1 y las particiones lógicas en /mnt/particion2, /mnt/particion3, etc., usamos el comando:
```bash
sudo mkdir /mnt/particion1 /mnt/particion2 /mnt/particion3 /mnt/particion4 /mnt/particion5
sudo mount /dev/sdb1 /mnt/particion1
sudo mount /dev/sdb2 /mnt/particion2
sudo mount /dev/sdb3 /mnt/particion3
sudo mount /dev/sdb4 /mnt/particion4
sudo mount /dev/sdb5 /mnt/particion5
```
\
&nbsp;

- Para que estas particiones se monten automáticamente al iniciar el sistema, se deben añadir las entradas correspondientes al archivo `"/etc/fstab"`. Por ejemplo:

\
&nbsp;


```bash
/dev/sdb1 /mnt/particion1 ext4 defaults 0 0
/dev/sdb2 /mnt/particion2 ext4 defaults 0 0
/dev/sdb3 /mnt/particion3 ext4 defaults 0 0
/dev/sdb4 /mnt/particion4 ext4 defaults 0 0
/dev/sdb5 /mnt/particion5 ext4 defaults 0 0

```
\
&nbsp;

### PASO 6: 
#### Instalar Administrador Web y Visualizar Datos

- Para instalar "Webmin" en un sistema Linux, primero debes agregar el repositorio de "Webmin" a tu sistema. Puedes hacerlo ejecutando el siguiente comando en tu terminal:

```bash
sudo echo "deb http://download.webmin.com/download/repository sarge contrib" >> /etc/apt/sources.list
```
\
&nbsp;
Luego, debes añadir la clave GPG del repositorio de "Webmin" ejecutando el siguiente comando:

```bash
wget http://www.webmin.com/jcameron-key.asc
sudo apt-key add jcameron-key.asc
```
\
&nbsp;
Una vez que hayas agregado el repositorio y la clave GPG, debes actualizar tu sistema e instalar "Webmin" ejecutando los siguientes comandos:
```bash
sudo apt-get update
sudo apt-get install webmin
```
\
&nbsp;
- Una vez que se complete la instalación, puedes acceder a "Webmin" desde un navegador web ingresando la dirección IP de tu servidor seguida de ":10000", por ejemplo: "http://your-server-ip:10000". Se te pedirá ingresar un nombre de usuario y una contraseña para iniciar sesión.

- Una vez que hayas iniciado sesión en "Webmin", puedes acceder a la sección de disco y particiones para ver los detalles de las particiones de tu sistema.