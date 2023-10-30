# Instalación del Sistema Operativo
## STEP 1

En primer lugar, es necesario realizar el proceso de formateo en la Raspberry Pi, es decir, eliminar todos los datos almacenados en ella para comenzar desde cero. Para llevar a cabo esta acción, insertamos la tarjeta de memoria MicroSD en un ordenador y empleamos la aplicación predeterminada Raspberry Pi Imager.

En el caso de que esta aplicación no esté preinstalada, debemos ejecutar el siguiente comando en la consola:

```bash
user@user: sudo apt install rpi-imager
```

Luego, vamos a necesitar ejecutar este comando con permisos de administrador (sudo) para instalar la aplicación Raspberry Pi Imager (rpi-imager) utilizando el comando "apt". Esto es importante porque esta aplicación será esencial para los próximos pasos.

Despues, llega el momento de elegir la opción de formateo y seleccionar la memoria que queremos borrar. Una vez que tengamos todo configurado, hacemos clic en "Write". Después de que el proceso termine, nuestra Raspberry Pi ya estaria completamente vacía, sin ningún sistema operativo anterior.

El próximo paso es instalar un nuevo sistema operativo. Lo vamos a hacer utilizando la misma herramienta que usamos para el formateo, es decir, Raspberry Pi Imager. En este caso, vamos a instalar el sistema operativo Raspberry Pi OS Lite (x64), que se encuentra en la sección "Raspberry Pi OS (other)". La razon de esta elección es que no vamos a necesitar la interfaz de usuario de escritorio para nuestro proyecto. Solo tenemos que seleccionar nuevamente la memoria y hacer clic en "Write". Una vez que termine el proceso, estaremos listos para empezar a trabajar directamente con Raspberry Pi a través de su interfaz. 



## STEP 2: Hardware y Usuarios

En el siguiente paso, una vez retiremos la tarjeta de memoria MicroSD del ordenador y la insertemos nuevamente en nuestra Raspberry Pi, ya vamos a estar listos para comenzar con nuestras actividades. Conectamos un monitor a través de un cable HDMI, un teclado mediante un puerto USB y establecemos una conexión a través de un cable LAN, además de conectar el conector micro-USB para la alimentación. Con estos elementos en su lugar, estaremos preparados para iniciar nuestras labores.


Para dar inicio, necesitamos establecer un nuevo usuario. Le solicitaremos que elija un nombre de usuario y una contraseña, pero es esencial que los anote y los recuerde cuidadosamente. Una vez que haya finalizado el proceso de inicio de sesión, se le presentará una terminal que guarda semejanza con la que se encuentra en el sistema operativo Linux. Esta terminal opera utilizando el lenguaje Bash. A continuación, proporcionaremos una guía que contiene los comandos que debe introducir, junto con una breve descripción de la función de cada uno, para poner en marcha el servicio de SSH.



## STEP 3: Creación de la SSH Key

Para crear la conexión entre nuestro Raspberry Pi y ótras PCs, vamos a crear una llave SSH, que sirve para autenticar las conexiones. Para esto utilizaremos los siguientes comandos: 

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Utilizamos el servicio systemctl para ajustar la configuración del protocolo SSH. El primer comando activará automáticamente el servidor SSH al arrancar la mini computadora, mientras que el segundo comando lo activará solo para la sesión actual.

A continuación, vamos a ejecutar el siguiente comando:

```Bash
hostname –I
```

Este comando nos va a dar la dirección IP del ordenador Raspberry.





## STEP 4: Conexión desde la Computadora

En este momento, necesitamos disponer de otra computadora externa que emplearemos para establecer la conexión con la Raspberry Pi. En la consola de la PC que vamos a utilizar, es necesario ingresar el siguiente comando:

```Bash
sudo apt-get install openssh-server
```

Con la ejecución de este comando, procederemos a instalar Open SSH, que representa una implementación del protocolo SSH. A continuación, introduciremos los mismos comandos que previamente ejecutamos en la Raspberry Pi, de modo que podamos configurarla de manera idéntica.

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Por ultimo tenemos que ingresar el siguiente comando, cambiando "username" por el nombre de usuario que se estableció al iniciar por primera vez al Raspberry Pi, y también cambiando"Ipaddres" por la dirección de IP que nos dió la terminal de Raspberry al ejecutar el comando "hostname -I":

```bash
ssh username@Ipaddress
```

En este momento, si nos encontramos conectados a una red LAN, tenemos la capacidad de gestionar nuestra Raspberry Pi desde otra computadora. Para ilustrar esto, podemos emplear el siguiente comando en la interfaz de nuestra computadora como ejemplo:

```bash
touch ejemplo.txt
```

Con la ejecución de esta instrucción, generaremos un archivo llamado "ejemplo.txt" en el almacenamiento de nuestra Raspberry. Podremos confirmar la correcta creación del archivo si accedemos a la interfaz de Raspberry y ejecutamos el siguiente comando:

```bash
ls
```

Para terminar, si deseamos apagar nuestro Raspberry, ingresamos el comando (puede ser ingresado en la terminal de nuestra PC o la terminal de Raspberry):

```bash
shutdown
```

Y en la PC ingresamos el comando:

```bash
exit
```

para cerrar el servidor SSH y la sesión actual.