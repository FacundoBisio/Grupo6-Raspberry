# Segunda entrega

### introduccion

Para comenzar, vamos a detallar el proceso de configuración paso a paso para lograr nuestro objetivo, que es instalar una aplicación gráfica en una Raspberry Pi y ejecutarla de forma remota desde una computadora conectada a través de SSH. Este enfoque nos permite aprovechar el poder de procesamiento de la Raspberry Pi mientras visualizamos la aplicación en la computadora cliente.

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

## Iniciar con una aplicacion grafica

### Paso por paso

Para comenzar, vamos a detallar el proceso de configuración paso a paso para lograr nuestro objetivo, que es instalar una aplicación gráfica en una Raspberry Pi y ejecutarla de forma remota desde una computadora conectada a través de SSH. Este enfoque nos permite aprovechar el poder de procesamiento de la Raspberry Pi mientras visualizamos la aplicación en la computadora cliente.

**Paso 1: Instalar `gedit`, si no está instalado:**

En primer lugar, debemos asegurarnos de que la aplicación `gedit` esté instalada en nuestra Raspberry Pi. `gedit` es un editor de texto simple pero útil que usaremos como ejemplo en este proceso. Puede instalarlo usando el administrador de paquetes de su sistema, como `apt` en Raspbian.

**Paso 2: Crear un archivo de texto en la Raspberry Pi:**

Ahora, en la Raspberry Pi, vamos a crear un archivo de texto que más adelante modificaremos desde la computadora cliente. Esto se puede hacer utilizando el comando `touch` o cualquier editor de texto de su elección. Por ejemplo:

```bash
touch ejemplo1
```

Este archivo servirá como un ejemplo de archivo que deseamos editar de forma remota.

**Paso 3: Conectar a la Raspberry Pi a través de SSH:**

En este punto, hemos creado el archivo en la Raspberry Pi y ahora necesitamos conectarnos a ella desde nuestra computadora cliente utilizando SSH. Puede hacerlo con el siguiente comando:

```bash
ssh -X usuario@direccion_ip_raspberry
```

Asegúrese de que la opción `-X` esté habilitada en su conexión SSH para permitir el reenvío de X11. Esto es esencial para poder visualizar aplicaciones gráficas de forma remota.

**Paso 4: Modificar el archivo desde la computadora cliente:**

Una vez que esté conectado a la Raspberry Pi a través de SSH con reenvío de X11 habilitado, puede utilizar su editor de texto favorito, como `gedit`, para editar el archivo que creó en el Paso 2. Por ejemplo:

```bash
gedit ejemplo1.txt
```

Esto abrirá la aplicación `gedit` en su computadora cliente, pero la ejecución real y el procesamiento de `gedit` se realizarán en la Raspberry Pi. Puede editar el archivo y guardar los cambios como lo haría normalmente.

**Paso 5: Visualizar el archivo modificado en la Raspberry Pi:**

Después de realizar las modificaciones en el archivo desde la computadora cliente, es posible que desee verificar el contenido del archivo en la Raspberry Pi. Esto se puede hacer utilizando el comando `cat`. Por ejemplo:

```bash
cat ejemplo1.txt
```

Esto mostrará el contenido actualizado del archivo en la terminal de la Raspberry Pi.

## Conclusión:

Al seguir estos pasos, hemos logrado instalar una aplicación gráfica en una Raspberry Pi y ejecutarla de forma remota desde una computadora cliente a través de SSH con reenvío de X11 habilitado. Esto nos permite aprovechar la capacidad de procesamiento de la Raspberry Pi mientras interactuamos con la aplicación de manera gráfica desde nuestra computadora. Este enfoque es útil en situaciones en las que deseamos ejecutar aplicaciones gráficas en hardware más ligero y visualizarlas en una computadora más potente, lo que puede ser beneficioso para tareas de procesamiento de video u otras aplicaciones intensivas en gráficos.



### Objetivo:
Instalando aplicaciones gráficas en la raspberry podamos correrlas por ssh sin que nuestro servidor realice las tareas de procesamiento del video, sino que simplemente se envíen los datos remotamente y podamos generar las ventanas y los gráficos en el host cliente.



