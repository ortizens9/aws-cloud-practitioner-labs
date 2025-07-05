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

## Lab 4 - ELB(Balanceador de carga) + Auto Scaling Group

1.**Lanzar 2 instancias EC2 diferentes**

-Antes que nada vamos a crear unos textos diferentes para [una instancia y otra](AWS-labs/lab-4-ELB+ASG/31.png)
  
-Vamos al servicio EC2 en nuestra cuenta IAM en la consola AWS y hacemos clic en [Lanzar instancias](AWS-labs/lab-4-ELB+ASG/1.png) de Ubuntu server 24.04. Le damos un nombre "Mi instancia 1".
 La vamos a crear sin par de claves pese a que ya sabemos que no es lo recomendado.
Nuevo grupo de seguridad. Activamos permitir el tráfico HTTP. Le damos a "detalles avanzados", vamos donde dice Datos de usuario y pegamos [el texto que hemos creado antes](AWS-labs/lab-4-ELB+ASG/2.png).-> Lanzar instancia.
 Y ahora repetimos el proceso con otra, instancia llamada "Mi instancia 2", pero añadiendo ésta al mismo grupo de seguridad que la primera "launch-wizard-3.
 Y en esta le ponemos el otro texto.
[Comprobamos que funcionan](AWS-labs/lab-4-ELB+ASG/3.png). Copiando las direcciones IP públicas.(Una vez en funcionamiento)

2.**Creación ALB**

-En EC2 donde dice Equilibrio de carga-> Balanceadores de carga-> Crear balanceador de carga. Y le damos a ALB(Application Load Balancer/Balanceador de carga de aplicaciones). Le voy a dar de nombre [ALBLab4](AWS-labs/lab-4-ELB+ASG/4.png). Estará expuesto a Internet y de IPv4. Y vamos a seleccionar [us-east-1a y us-east-1b](AWS-labs/lab-4-ELB+ASG/30.png)(mínimo).
Donde dice grupos de seguridad(en la creación del ALB, le damos a "cree un nuevo grupo de seguridad", esto nos abrirá otra pestaña donde configurar este grupo. Le pondremos de nombre Gruposeguridad-ALB-Lab4. Esto permitira el HTTP dentro del ALB. Creamos la regla que será una de [entrada de HTTP](AWS-labs/lab-4-ELB+ASG/5.png) para 0.0.0.0/0(Cualquier origen). Unimos el ALB a ese grupo creado. Y luego donde dice Agentes de escucha y direccionamiento->Crear [un grupo de destino](AWS-labs/lab-4-ELB+ASG/9.png)(también se nos abrirá otra ventana nueva). Le damos el nombre ["TargetGroupLab4"](AWS-labs/lab-4-ELB+ASG/10.png) y lo dejamos tal cual está, con HTTP.
Incluimos como pendientes las [2 instancias](AWS-labs/lab-4-ELB+ASG/11.png) que hemos creado, lo creamos y una vez creado volvemos otra vez a la pestaña por donde estabamos creando el ALB y ponemos el TargetGroup4 como [grupo de destino](AWS-labs/lab-4-ELB+ASG/6.png). Copiamos el nombre del ALB: ALBLab4-493378900.us-east-1.elb.amazonaws.com. Y si lo refrescamos varias veces vemos como se van alternando las intancias, con los diferentes textos.[Texto 1](AWS-labs/lab-4-ELB+ASG/13.png) y [texto 2](AWS-labs/lab-4-ELB+ASG/14.png)

3.**Plantilla de lanzamiento**

-En EC2 vamos a la izquierda en el mismo sitio donde dice instancias, hay un lugar que dice [Plantillas de lanzamiento](AWS-labs/lab-4-ELB+ASG/15.png), vamos a crear una. Le damos de nombre [Plantilla-Lab4](AWS-labs/lab-4-ELB+ASG/16.png), seleccionamos el tipo de AMI que hemos usado para crear las instancias: [Ubuntu server](AWS-labs/lab-4-ELB+ASG/17.png). Y tipo de servidor t2.micro(de capa gratuita). De grupo de seguridad el "launch-wizard-3". Y pegamos el texto de datos de usuario anterior.

4.**Auto Scaling Group!**

-Después de crear el template. Vamos a Grupos de [Auto Scaling](AWS-labs/lab-4-ELB+ASG/18.png) y creamos uno que vamos a llamar [ASG-Lab4](AWS-labs/lab-4-ELB+ASG/19.png). Seleccionamos Plantilla-Lab4 como plantilla de lanzamiento. Ponemos [2 subredes diferentes](AWS-labs/lab-4-ELB+ASG/20.png) como zona de disponibilidad(para alta disponibilidad). La asociamos a un balanceador existente y elegimos el grupo destino que hemos [creado antes TargetGroupLab4](AWS-labs/lab-4-ELB+ASG/21.png). Activamos las [comprobaciones de estado de ELB](AWS-labs/lab-4-ELB+ASG/22.png). [Configuramos el tamaño del grupo](AWS-labs/lab-4-ELB+ASG/23.png): de capacidad deseada 2, de mínima capacidad 1 y de máxima 3. Seleccionamos [una política de escalado de seguimiento de destino](AWS-labs/lab-4-ELB+ASG/24.png)(Target Tracking Policy), tipo de métrica  Utilización de CPU y como valor destino 70%. Todo lo demás, siguiente y siguiente.
Ahora Launch Template crea 2 instancias nuevas que sustituyen a las que ya teníamos y se registrarán en el Target Group del ALB. Y lo que pasará es que si la CPU supera el 70%, el ASH añadirá otra instancia automáticamente.

5.**Instance connect**

-Una vez configurado si voy a una de mis instancias y la selecciono, puedo darle donde dice conectar, una vez [nos conectemos con IP pública](AWS-labs/lab-4-ELB+ASG/25.png) podremos entrar vía Instance Connect. [Una vez dentro](AWS-labs/lab-4-ELB+ASG/26.png) hacemos un _sudo apt-get update && sudo apt-get install_ -y _stress-ng_. Una vez tengamos instalado stress-ng, lo ejecutamos [durante 5 minutos](AWS-labs/lab-4-ELB+ASG/28.png) con el comando _stress-ng --cpu 1 --timeout 300s_. Esto hará que a parte de las instancias que tenemos [se creará otra más](AWS-labs/lab-4-ELB+ASG/29.png)(se escalará a 3). Se autoescalará debido a stress-ng porque superará el 70% de CPU.
Con esto creamos un servicio altamente disponible con EC2, ELB y ASG.
