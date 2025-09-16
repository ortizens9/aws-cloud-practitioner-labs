## Lab 2-Lanzar instancia EC2 y conectarse vía SSH
#Objetivo: Entender servidores virtuales y acceso remoto

1.**Lanzar instancia EC2**

-Para ello con nuestro usuario IAM(creado con todos los permisos) nos vas al servicio EC2, en EC2 clicamos en [Lanzar Instancias EC2](/AWS-labs/lab-2-ecd-ssh/Capturas/1.png)
Escogemos una sencilla, en este caso una [Amazon Linux/t2 micro](/AWS-labs/lab-2-ecd-ssh/Capturas/2.png) le creamos una [clave RSA](/AWS-labs/lab-2-ecd-ssh/Capturas/3.png) y de formato .pem ya que estamos desde Windows.
[Permitimos el acceso de trático SSH](/AWS-labs/lab-2-ecd-ssh/Capturas/4.png) y la creamos.

2.**Conexión SSH**

-Ahora desde la [terminal](AWS-labs/lab-2-ecd-ssh/Capturas/6.png) que tengamos y estando en la carpeta donde hemos guardado nuestra clave pem escribimos: ssh.exe -i claveslab2.pem ec2-user@35.180.140.117 (que es la IP de nuestra instancia EC2)

Puede pasar como es el caso que nos diga que no tenemos permiso para acceder a la clave. Tendremos que desactivar los permisos de herencia desde propiedades y dárselos únicamente al usuario con el que vamos a hacer la operación. Yéndonos a [propiedades->seguridad](AWS-labs/lab-2-ecd-ssh/Capturas/7.png), luego a [cambiar](AWS-labs/lab-2-ecd-ssh/Capturas/8.png),[2](AWS-labs/lab-2-ecd-ssh/Capturas/9.png)

y luego a deshabilitar herencia->[convertir los permisos heredados en permisos explícitos en este objeto](AWS-labs/lab-2-ecd-ssh/Capturas/10.png) y borrarlos hasta únicamente dejar los de [mi usuario](AWS-labs/lab-2-ecd-ssh/Capturas/11.png). Esto ya nos dejará entrar a la instancia [vía SSH](AWS-labs/lab-2-ecd-ssh/Capturas/13.png).
