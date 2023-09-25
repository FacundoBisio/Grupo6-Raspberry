# Segunda entrega

### introduccion
Nosotros representamos el grupo 6 del Instituto Técnico Salesiano Villada, en la asignatura de sistemas y telecomunicaciones, conformado por los estudiantes Asis Tomas, Bisio Facundo, Mendez Fabricio y Montini Francisco. Como punto de partida en nuestro proyecto relacionado con Raspberry Pi, nos proponemos llevar a cabo el formateo de nuestra unidad "Raspberry", la instalación de un nuevo sistema operativo en ella y la creación de una conexión con otras computadoras a través del protocolo SSH.

## Instalar Xorg

1. *Verificar si Xorg está instalado*:
   La mayoría de las distribuciones de Linux, como Ubuntu, Fedora y Debian, ya incluyen el servidor Xorg por defecto. Puedes verificar si está instalado ejecutando el siguiente comando en la terminal:

```bash
user@user: Xorg -version
```

Si Xorg no está instalado, puedes instalarlo utilizando el gestor de paquetes de tu distribución. Por ejemplo, en Ubuntu, puedes usar `apt`:

```bash
user@user: sudo apt update
user@user: sudo apt install xorg
```
2. *Iniciar el Servidor X*:
   Una vez que Xorg esté instalado y configurado, puedes iniciar el servidor X ejecutando el siguiente comando:

```bash
user@user: startx
```

Esto debería iniciar el servidor X y cargar un entorno gráfico, si está instalado. Si deseas usar un entorno de escritorio específico, debes instalarlo antes de iniciar el servidor X.

Recuerda que el servidor X se configura automáticamente durante la instalación del sistema operativo y se inicia cuando inicias sesión en un entorno gráfico. Solo en casos específicos de configuración avanzada o problemas de configuración es necesario intervenir manualmente en la configuración del servidor X.

## Iniciar con aplicacion grafica

1. Instalar `gedit`, si no está instalado:

```bash
user@user: sudo apt update
user@user: sudo apt install gedit
```

2.  Crear en el servidor raspaberry un archivo de texto ,el cual, iremos a modificar proximamente desde la computadora conectada:
    
```bash
user@raspberrypi: touch ejemplo1
```

3. Salir de la conexion y realizar la misma pero con "-X" para poder modificar los archivos del sistema conectado:

```bash
user@user: ssh -X username@Ipaddress
```

Luego poder modificar el archivo creado a traves de raspberry desde la computadora recientemente conectada:

```bash
user@user: gedit ejemplo1
```

4. Visualizar el archivo modificado `ejemplo1` en la raspberry a traves de cat:

```bash
user@raspberrypi: cat ejemplo1
```


### Objetivo:
Instalando aplicaciones gráficas en la raspberry podamos correrlas por ssh sin que nuestro servidor realice las tareas de procesamiento del video, sino que simplemente se envíen los datos remotamente y podamos generar las ventanas y los gráficos en el host cliente.

