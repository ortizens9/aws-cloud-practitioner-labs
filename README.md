# aws-cloud-practitioner-labs
## Lab 1-S3-bucket: Crar un bucket S3 en AWS

#Objetivo
Aprender a crear un bucket en S3 y subir un archivo

##Pasos

1.**Crear el bucket**:
 -Ir al servicio S3 en la consola de AWS
 -Hacer clic en "Crear bucket(Create bucket)" [Captura de Consola AWS](/AWS-labs/lab-1-s3-bucket/capturas/2.png)
 
 -Ponerle un nombre, yo le he puesto mi-bucket-ortizens9-2025 [Poniendo el nombre](/AWS-labs/lab-1-s3-bucket/capturas/1.png)
 
 -Acordarse siempre de en qué zona lo creamos en mi caso eu-north-1
 
 -Por ahora dejamos bloqueado todo el acceso público y desactivadas, también las versiones de bucket
 [Desactivado acceso público](/AWS-labs/lab-1-s3-bucket/capturas/3.png)
  
2.**Subir archivo**:

 -Entramos en el bucket, le damos a "Cargar(upload)"  [Cargar](/AWS-labs/lab-1-s3-bucket/capturas/5.png)
 
 -Añadir archivos, vamos al directorio donde tenemos el archivo holamundo.txt y lo subimos [holamundo](/AWS-labs/lab-1-s3-bucket/capturas/6.png)

##Conclusión:
He aprendido a usar S3 para almacenar objetos.

## Lab 2-Lanzar instancia EC2 y conectarse vía SSH
#Objetivo: Entender servidores virtuales y acceso remoto

1.**Lanzar instancia EC2**
-Para ello con nuestro usuario IAM(creado con todos los permisos) nos vas al servicio EC2, en EC2 clicamos en Lanzar instancias. [Lanzar Instancia EC2](AWS-labs/lab-2-ecd-ssh/1.png)
Escogemos una sencilla, en este caso una [Amazon Linux/t2 micro](AWS-labs/lab-2-ecd-ssh/2.png) le creamos una [clave RSA](AWS-labs/lab-2-ecd-ssh/3.png) y de formato .pem ya que estamos desde Windows.
[Permitimos el acceso de trático SSH](AWS-labs/lab-2-ecd-ssh/4.png) y la creamos.

2.**Conexión SSH**
-Ahora desde la [terminal](AWS-labs/lab-2-ecd-ssh/6.png) que tengamos y estando en la caepeta donde hemos guardado nuestra clave pem escribimos: ssh.exe -i claveslab2.pem ec2-user@35.180.140.117 (que es la IP de nuestra instancia EC2)

Puede pasar como es el caso que nos diga que no tenemos permiso para acceder a la clave. tendremos que desactivar los permisos de herencia desde propiedades y dárselos únicamente al usuario con el que vamos a hacer la operación. Yéndonos a [propiedades->seguridad](AWS-labs/lab-2-ecd-ssh/7.png), luego a [cambiar](AWS-labs/lab-2-ecd-ssh/8.png),[2](AWS-labs/lab-2-ecd-ssh/9.png)

y luego a deshabilitar herencia->[convertir los permisos heredados en permisos explícitos en este objeto](AWS-labs/lab-2-ecd-ssh/10.png) y borrarlos hasta únicamente dejar los de [mi usuario](AWS-labs/lab-2-ecd-ssh/11.png). Esto ya nos dejará entrar a la instancia [vía SSH](AWS-labs/lab-2-ecd-ssh/13.png).

3.**Instalar servidor web**
-Ejecutamos el comando: [sudo yum install httpd -y](AWS-labs/lab-2-ecd-ssh/15.png) y se nos [instalará](AWS-labs/lab-2-ecd-ssh/16.png).

