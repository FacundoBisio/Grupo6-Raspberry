# Instalacion de servicio FTP
### Alumnos: Asis Tomas, Facundo Bisio, Fabricio Mendez y Francisco MOntini

# Índice 
1. [Introducción](#introducción)
2. [Objetivo](#objetivo)
3. [Instalación del servidor ftp](#instalación-del-servidor-ftp)
4. [Configuración](#configuración)
5. [Conexión al servicio](#conexión-al-servicio)
6. [Conclusión](#conclusión)

# Introducción
En esta entrega veremos la instalación de un servidor FTP básico (vsftpd) en nuestra Raspberry, FTP significa “File Transfer Protocol”, Protocolo para la Transferencia de Archivos. Es un programa especial que se ejecuta en un servidor conectado normalmente en Internet (aunque puede estar conectado en otros tipos de redes, como la LAN en nuestro caso). La función del mismo es permitir el desplazamiento de datos entre diferentes servidores / ordenadores. Básicamente un cliente puede subir archivos al servidor para que otros puedan acceder a él. Luego configurarlo para que la Raspberry sea el servidor de la red LAN de nuestra mesa. Donde probaremos la accesibilidad al servicio utilzando como cliente ftp la aplicación "Filezilla".

## Objetivo
El propósito de esta entrega es establecer una conexión entre dos dispositivos utilizando el protocolo FTP, con el fin de facilitar la transferencia de archivos posteriormente.

## Instalación del servidor ftp
Para empezar, encenderemos y conectaremos la Raspberry. Antes de proceder con la instalación del servidor correspondiente, es importante actualizar la lista de paquetes utilizando el siguiente comando:

```bash
sudo apt update
sudo apt upgrade
```
Después de que la Raspberry esté en funcionamiento, para instalar el servidor FTP, será necesario emplear el comando que se indica a continuación:

```bash
sudo apt install vsftpd
```

Al emplear el comando "sudo", se utilizarán los privilegios de superusuario, seguido de "apt", que es el administrador de paquetes por defecto en Ubuntu, y finalmente, se usará "install" junto con el nombre del paquete correspondiente al servidor FTP.

## Configuración
En primer lugar, es necesario editar el archivo ubicado en "/etc/vsftpd.conf" y descomentamos los siguientes parámetros:

```bash
local_enable=YES
write_enable=YES
```
En este paso, lo que hacemos es permitir la escritura de los archivos a los usuarios de la Raspberry Pi, descomentando estas dos líneas de codigo.

Luego tendremos que reiniciar el servicio:

```
sudo service vsftpd restart
```

## Conexión al servicio
Una vez que hemos instalado nuestro servidor FTP, vamos a ver si funciona, para ello, descargamos [Filezilla](https://filezilla-project.org/) que es un cliente FTP. Al abrirlo nos aparecerá una ventana tal como esta:

![imagen1](imagen1.png)

Tendremos que conectarnos al servidor FTP ingresando la IP de la Raspberry, (que en nuestro caso es 192.169.6.2). También ingresaremos el usuario y la contraseña de nuestra Raspberry.

## Conclusión
En esta cuarta entrega, logramos alcanzar nuestro objetivo de manera exitosa. Principalmente, adquirimos conocimientos sobre lo que representa un Servidor FTP, que es la abreviatura de "File Transfer Protocol" o Protocolo de Transferencia de Archivos. La función principal de este protocolo es permitir la transferencia de datos entre distintos servidores u ordenadores, lo que significa que un cliente puede cargar archivos en el servidor para que otros tengan acceso a ellos.

Por lo tanto, procedimos a instalar el servidor FTP y luego lo configuramos de manera que la Raspberry actúe como servidor en la red LAN de nuestra área de trabajo. Posteriormente, evaluamos la accesibilidad del servicio utilizando la aplicación "Filezilla" como cliente FTP.