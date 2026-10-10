## Lab 3- Monitorización básica con CloudWatch usando AWS CLI

-Para este lab, voy a crear un nuevo usuario IAM. Lo llamaremos pepe.
![servicio IAM](/AWS-labs/lab-3-iamclicloudwatch/Capturas/1.png)
!['pepe'](/AWS-labs/lab-3-iamclicloudwatch/Capturas/2.png)
-Para ello vamos desde nuestro usuario root, a la consola AWS.
Vamos al servicio IAM)->Personas->Crear persona->Le damos nombre 'pepe' (No es necesario darle acceso a la consola AWS).

![Creamos un nuevo grupo](/AWS-labs/lab-3-iamclicloudwatch/Capturas/3.png)
![CloudWatchReadOnlyAccess](/AWS-labs/lab-3-iamclicloudwatch/Capturas/4.png).
-Creamos un nuevo grupo crearemos un nuevo grupo y le adjuntamos los permisos que queremos que tenga este usuario. En este caso (CloudWatchReadOnlyAccess).

![Claves de acceso](/AWS-labs/lab-3-iamclicloudwatch/Capturas/5.png)

-Vamos al usuario creado y en la pestaña credenciales de seguridad, vamos donde dice:. Le damos a crear Interfaz Línea de Comandos.
Esto nos genera una clave (que no debemos compartir bajo ningún concepto, ya que supondría un fallo de seguridad).
Después de haber bajado AWS CLI para nuestro PC en mi caso Windows.

![CLI en el powershell](/AWS-labs/lab-3-iamclicloudwatch/Capturas/7.png) 
-Nos conectamos vía SLI en powershell o cmd de nuestro PC, con el comando _aws configure --profile Pepe_. Nos preguntará por nuestra clave ID, por la clave de acceso secreta, la región donde nos queremos conectar:eu-west-3 y el formato de salida: json.
![esta respuesta](/AWS-labs/lab-3-iamclicloudwatch/Capturas/8.png)
-Usamos el comando: _aws cloudwatch list-metrics --namespace AWS/EC2 --region eu-west-3 --profile Pepe --output table_ y nos daria esta respuesta.

![¿Qué es lo que pasaria si borrasemos los permisos?](/AWS-labs/lab-3-iamclicloudwatch/Capturas/9.png)
![este error](/AWS-labs/lab-3-iamclicloudwatch/Capturas/10.png)
-¿Qué es lo que pasaria si borrasemos los permisos? Nos daría este error, de esta manera vemos que actuamos con el principio de mínimo privilegio. Que significa que la mejor práctica es dar los mínimos permisos posibles para tener mayor seguridad.
