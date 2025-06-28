# aws-cloud-practitioner-labs
## Lab 1-S3-bucket: Crear un bucket S3 en AWS

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

-Para ello con nuestro usuario IAM(creado con todos los permisos) nos vas al servicio EC2, en EC2 clicamos en [Lanzar Instancias EC2](AWS-labs/lab-2-ecd-ssh/1.png)
Escogemos una sencilla, en este caso una [Amazon Linux/t2 micro](AWS-labs/lab-2-ecd-ssh/2.png) le creamos una [clave RSA](AWS-labs/lab-2-ecd-ssh/3.png) y de formato .pem ya que estamos desde Windows.
[Permitimos el acceso de trático SSH](AWS-labs/lab-2-ecd-ssh/4.png) y la creamos.

2.**Conexión SSH**

-Ahora desde la [terminal](AWS-labs/lab-2-ecd-ssh/6.png) que tengamos y estando en la carpeta donde hemos guardado nuestra clave pem escribimos: ssh.exe -i claveslab2.pem ec2-user@35.180.140.117 (que es la IP de nuestra instancia EC2)

Puede pasar como es el caso que nos diga que no tenemos permiso para acceder a la clave. Tendremos que desactivar los permisos de herencia desde propiedades y dárselos únicamente al usuario con el que vamos a hacer la operación. Yéndonos a [propiedades->seguridad](AWS-labs/lab-2-ecd-ssh/7.png), luego a [cambiar](AWS-labs/lab-2-ecd-ssh/8.png),[2](AWS-labs/lab-2-ecd-ssh/9.png)

y luego a deshabilitar herencia->[convertir los permisos heredados en permisos explícitos en este objeto](AWS-labs/lab-2-ecd-ssh/10.png) y borrarlos hasta únicamente dejar los de [mi usuario](AWS-labs/lab-2-ecd-ssh/11.png). Esto ya nos dejará entrar a la instancia [vía SSH](AWS-labs/lab-2-ecd-ssh/13.png).

3.**Instalar servidor web**

-Ejecutamos el comando: [sudo yum install httpd -y](AWS-labs/lab-2-ecd-ssh/15.png) y se nos [instalará](AWS-labs/lab-2-ecd-ssh/16.png).

## Lab 3- Monitorización básica con CloudWatch usando AWS CLI

-Para este lab, voy a crear un nuevo usuario IAM. Lo llamaremos pepe.

-Para ello vamos desde nuestro usuario root, a la consola AWS.
Vamos al [servicio IAM](AWS-labs/lab-3-iamclicloudwatch/1.png)->Personas->Crear persona->Le damos nombre ['pepe'](AWS-labs/lab-3-iamclicloudwatch/2.png).(No es necesario darle acceso a la consola AWS)

-[Creamos un nuevo grupo](AWS-labs/lab-3-iamclicloudwatch/3.png) y le adjuntamos los permisos que queremos que tenga este usuario. En este caso [CloudWatchReadOnlyAccess](AWS-labs/lab-3-iamclicloudwatch/4.png).

-Vamos al usuario creado y en la pestaña credenciales de seguridad, vamos donde dice: [Claves de acceso](AWS-labs/lab-3-iamclicloudwatch/5.png). Le damos a crear[(Interfaz Línea de comandos/CLI)](AWS-labs/lab-3-iamclicloudwatch/6.png).
Esto nos genera una clave (que no debemos compartir bajo ningún concepto, ya que supondría un fallo de seguridad).
Después de haber bajado AWS CLI para nuestro PC en mi caso Windows.

-Nos conectamos vía [CLI en el powershell](AWS-labs/lab-3-iamclicloudwatch/7.png) o cmd de nuestro PC, con el comando _aws configure --profile Pepe_. Nos preguntará por nuestra clave ID, por la clave de acceso secreta, la región donde nos queremos conectar:eu-west-3 y el formato de salida: json.
-Usamos el comando: _aws cloudwatch list-metrics --namespace AWS/EC2 --region eu-west-3 --profile Pepe --output table_ y nos daria [esta respuesta](AWS-labs/lab-3-iamclicloudwatch/8.png)

-[¿Qué es lo que pasaria si borrasemos los permisos?](AWS-labs/lab-3-iamclicloudwatch/9.png) Nos daría [este error](AWS-labs/lab-3-iamclicloudwatch/10.png), de esta manera vemos que actuamos con el principio de mínimo privilegio. Que significa que la mejor práctica es dar los mínimos permisos posibles para tener mayor seguridad.

