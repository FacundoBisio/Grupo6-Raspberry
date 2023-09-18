## Creación de la SSH Key

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

![](https://github.com/FacundoBisio/Grupo6-Raspberry/blob/main/RASPABERRY%20INSTALATION/Img/Pasted%20image%2020230918101432.png)