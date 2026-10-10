## Lab 2-Lanzar instancia EC2 y conectarse vía SSH
#Objetivo: Entender servidores virtuales y acceso remoto

1. **Lanzar instancia EC2**

-Para ello con nuestro usuario IAM(creado con todos los permisos) nos vas al servicio EC2, en EC2 clicamos en lanzar instancias EC2. ![lanzar Instancias EC2](/AWS-labs/lab-2-ecd-ssh/Capturas/1.png) ![Amazon Linux/t2 micro](/AWS-labs/lab-2-ecd-ssh/Capturas/2.png)
Escogemos una sencilla, en este caso una Amazon Linux/t2_micro  le creamos una clave RSA y de formato .pem ya que estamos desde Windows.
Permitimos el acceso de tráfico SSH y la creamos. ![Permitimos el acceso de trático SSH](/AWS-labs/lab-2-ecd-ssh/Capturas/4.png)

2. **Conexión SSH**

!(/AWS-labs/lab-2-ecd-ssh/Capturas/6.png)
-Ahora desde la terminal que tengamos y estando en la carpeta donde hemos guardado nuestra clave pem escribimos: ssh.exe -i claveslab2.pem ec2-user@35.180.140.117 (que es la IP de nuestra instancia EC2)

Puede pasar como es el caso que nos diga que no tenemos permiso para acceder a la clave. Tendremos que desactivar los permisos de herencia desde propiedades y dárselos únicamente al usuario con el que vamos a hacer la operación. Yéndonos a propiedades->seguridad ![propiedades->seguridad](/AWS-labs/lab-2-ecd-ssh/Capturas/7.png)
![cambiar](/AWS-labs/lab-2-ecd-ssh/Capturas/8.png),![2](/AWS-labs/lab-2-ecd-ssh/Capturas/9.png)
Luego a AWS-labs/lab-2-ecs-ssh.

![a](/AWS-labs/lab-2-ecd-ssh/Capturas/10.png)
![b](/AWS-labs/lab-2-ecd-ssh/Capturas/11.png)
y luego a deshabilitar herencia->convertir los permisos heredados en permisos explícitos en este objeto y borrarlos hasta únicamente dejar los de mi usuario. Esto ya nos dejará entrar a la instancia vía SSH.
[vía SSH](/AWS-labs/lab-2-ecd-ssh/Capturas/13.png).
