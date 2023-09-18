## Instalación del Sistema Operativo

En primer lugar, es necesario realizar el proceso de formateo en la Raspberry Pi, es decir, eliminar todos los datos almacenados en ella para comenzar desde cero. Para llevar a cabo esta acción, insertamos la tarjeta de memoria MicroSD en un ordenador y empleamos la aplicación predeterminada Raspberry Pi Imager.

En el caso de que esta aplicación no esté preinstalada, debemos ejecutar el siguiente comando en la consola:

```bash
user@user: sudo apt install rpi-imager
```

Luego, vamos a necesitar ejecutar este comando con permisos de administrador (sudo) para instalar la aplicación Raspberry Pi Imager (rpi-imager) utilizando el comando "apt". Esto es importante porque esta aplicación será esencial para los próximos pasos.

Despues, llega el momento de elegir la opción de formateo y seleccionar la memoria que queremos borrar. Una vez que tengamos todo configurado, hacemos clic en "Write". Después de que el proceso termine, nuestra Raspberry Pi ya estaria completamente vacía, sin ningún sistema operativo anterior.

El próximo paso es instalar un nuevo sistema operativo. Lo vamos a hacer utilizando la misma herramienta que usamos para el formateo, es decir, Raspberry Pi Imager. En este caso, vamos a instalar el sistema operativo Raspberry Pi OS Lite (x64), que se encuentra en la sección "Raspberry Pi OS (other)". La razon de esta elección es que no vamos a necesitar la interfaz de usuario de escritorio para nuestro proyecto. Solo tenemos que seleccionar nuevamente la memoria y hacer clic en "Write". Una vez que termine el proceso, estaremos listos para empezar a trabajar directamente con Raspberry Pi a través de su interfaz. 

![](https://github.com/FacundoBisio/Grupo6-Raspberry/blob/main/RASPABERRY%20INSTALATION/Img/img1.png)