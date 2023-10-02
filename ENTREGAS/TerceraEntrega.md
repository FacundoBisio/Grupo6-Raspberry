# Segunda entrega

## Esquema de la red

_**Advertencia:** Este esquema va a ser el que yo utilizaré para explicar la configuración, podéis usar el esquema que os plazca._

En vez de utilizar el rango que por defecto nuestro router trae incorporado (192.168.1.0/24 o 192.168.0.0/24) lo cambiaremos, por ejemplo, por 192.168.66.0/24, así si algún dispositivo queda con una configuración incorrecta al instante veremos que algo está pasando, ya que **quedará totalmente aislado de la red**.

Reservaremos un espacio de direcciones comprendido entre la 192.168.66.100 y 192.168.66.119 donde ubicaremos el **router** (192.168.66.100), la Raspberry Pi (192.168.66.101) y en mi caso el **ordenador fijo y un htpc** (192.168.66.110 y 111). El resto del espacio, 192.168.66.1-192.168.66.99 y 192.168.66.120-192.168.66.254, será utilizado como **rango de asignación dinámica**, un rango innecesariamente grande para una red doméstica, pero que resulta interesante de configurar. Con esto en cuenta estos serían los datos:

- **Red:** 192.168.66.0
- **Máscara de subred:** 255.255.255.0
- **Rango DHCP:** 192.168.66.1-192.168.66.99, 192.168.66.120-192.168.66.254.
- **Gateway:** 192.168.66.100.
- **Raspberry:** 192.168.66.101.
- **Reservas DHCP:** 192.168.66.110 y 192.168.66.111.
- **DNS:** El que queramos, la ip de nuestro router, los DNS de nuestro ISP, los de Google…

## Instalación del servidor DHCP en Raspbian

Para instalar el servidor DHCP deberemos conectarnos vía SSH a nuestra Raspberry Pi e instalar isc-dhcp-server  con el gestor de paquetes de Raspbian:

```bash
$ sudo apt-get install isc-dhcp-server
```

Al instalarlo recibiremos el siguiente aviso:

_[FAIL] Starting ISC DHCP server: dhcpd[….] check syslog for diagnostics. … failed!_ _ failed!_

Esto se da porque actualmente no existe una configuración buena establecida, que es lo que haremos a continuación.

## Configuración del servidor DHCP

Hay dos archivos de configuración importantes que debemos conocer a la hora de instalar nuestro servidor DHCP:

### /etc/default/isc-dhcp-server

En este archivo podremos configurar la interfaz de red en la que ejecutaremos el servicio. Así que deberemos abrir el archivo (_$ sudo nano /etc/default/isc-dhcp-server_) y buscar la línea **“INTERFACES”** para dejarla tal que así:

```bash
1 INTERFACES=“eth0”
```

### /etc/dhcp/dhcpd.conf

Una buena práctica antes de ponernos a modificar dicho archivo o cualquier otro archivo de configuración es la de hacer una copia de seguridad del mismo, para eso:

```bash
1 $ sudo cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.backup
```

Hecho esto ya estamos listos para modificar el archivo. En este archivo **reside el grueso de la configuración**, desde aquí definiremos las opciones globales, los rangos de DHCP y sus respectivas opciones.

Para editarlo, como siempre:

```bash
1 $ sudo nano /etc/dhcp/dhcpd.conf
```

Nos encontraremos con un archivo bastante extenso aunque la mayoría comentado con # al principio de la línea. Podemos optar por borrar todo su contenido o bien por modificar y añadir las líneas que nos interesan. Sea como sea, para que el servicio funcione con los datos que hemos establecido al principio de esta entrada necesitaremos estos datos:

```bash
1 #Opciones globales
2 ddns-update-style none; #Puede actualizar los registros de un DNS si la IP de un 3 3 3 servidor de la LAN cambia, no nos interesa.
4
5 option domain-name "home.local"; #Establecemos un nombre de dominio.
6 option domain-name-servers 8.8.8.8, 8.8.4.4; #Configuramos los servidores DNS.
7
8 default-lease-time 259200; #Tiempo por defecto de la concesión en segundos.
9 max-lease-time 604800; #Tiempo máximo de la concesión en segundos.
10
11 authoritative; #Establece el servidor como principal.
12 log-facility local7;
13
14 #Opciones de subred
15 subnet 192.168.66.0 netmask 255.255.255.0 { #Declaración de la subred.
16 range 192.168.66.1 192.168.66.99; #Primer rango de direcciones.
17 range 192.168.66.120 192.168.66.254; #Segundo rango de direcciones.
18 option routers 192.168.66.100; #Gateway (nuestro router).
19 option subnet-mask 255.255.255.0; #Máscara de subred.
20 option broadcast-address 192.168.66.255; #Dirección de broadcast
21 }
22
23 #Reserva de direcciones
24 host timbleck-pc1 { #Declaramos la reserva
25 hardware ethernet 00:11:22:33:44:55; #Dirección MAC del dispositivo.
26 fixed-address 192.168.66.110; #Dirección IP reservada.
27 }
28 
29 #Reserva de direcciones
30 host timbleck-pc2 { #Declaramos la reserva
31 hardware ethernet 00:00:00:11:11:11; #Dirección MAC del dispositivo.
32 fixed-address 192.168.66.110; #Dirección IP reservada.
33 }
```
Es importante respetar la sintaxis del archivo (sobretodo sus “;” ya que son fáciles de olvidar).

Si bien he intentado comentar cada línea para que se entienda su significado paso a explicar la estructura del archivo. El archivo consta de tres partes en este ejemplo:

- **Opciones globales:** La primera parte del archivo, aquí se declaran las opciones que serán comunes para todas las subredes que configuremos en el servidor.
- **Opciones de subred:** Son opciones que sólo son válidas para dicha subred.
- **Reserva de direcciones:** Asociamos direcciones MAC a direcciones IP, cuando estas se conectan en vez de darles una IP de alguno de los rangos configurados les dará la que hayamos configurado manualmente.

## Evitando el desastre inminente

Con todo esto configurado estamos a un comando del desastre: en el momento en el que activemos el servicio de DHCP el servidor va a empezar a asignar IP’s de un rango cuyo gateway no existe, además de ser un rango distinto al de su propia IP, así que perderemos la conectividad hacia Internet y hacia nuestro servidor DHCP.

Para ahorrarnos el tener que configurar las IP’s a mano vamos a hacer las cosas en el **orden correcto**. El primer paso va a ser **cambiar la IP interna de nuestro router** y asignarle la que hemos convenido, así que nos conectamos a su servidor web y le configuramos la IP 192.168.66.100. Además, deberemos **desactivar el servicio de DHCP** del mismo desde su panel de control.

Lo siguiente será cambiar la IP de nuestra Raspberry Pi. Editando el archivo **/etc/network/interfaces**:

```bash
1 iface eth0 inet static
2 address 192.168.66.101
3 netmask 255.255.255.0
4 gateway 192.168.66.100
```

Y reiniciando el dispositivo. Al reiniciar el dispositivo la Raspberry volverá a intentar levantar el servicio, y **esta vez debería hacerlo con éxito** puesto que todas las opciones han sido correctamente configuradas.

Ahora nos toca volver a solicitar una IP vía DHCP en los distintos dispositivos de la red. Para hacerlo podemos reconectar la red físicamente o bien:

- **En Linux:** Escribimos en un terminal: $ sudo dhclient -r.
- **En Windows:** Escribir en un terminal: ipconfig /release, y luego, ipconfig /renew.

Con todo esto hecho ya deberíamos estar funcionando con **nuestro nuevo esquema de red** en la nueva subred 192.168.66.0/24 sin que los dispositivos que a partir de ahora se conecten noten el cambio.