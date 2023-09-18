## Conexión desde la Computadora

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