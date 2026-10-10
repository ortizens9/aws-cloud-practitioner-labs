## Lab 4 - ELB(Balanceador de carga) + Auto Scaling Group

1.**Lanzar 2 instancias EC2 diferentes**

![una instancia y otra](/AWS-labs/lab-4-ELB+ASG//Capturas/31.png)

-Antes que nada vamos a crear unos textos diferentes para una instancia y otra.

![Lanzar instancias](/AWS-labs/lab-4-ELB+ASG//Capturas/1.png)

-Vamos al servicio EC2 en nuestra cuenta IAM en la consola AWS y hacemos clic en lanzar instancias de Ubuntu server 24.04. Le damos un nombre "Mi instancia 1".
La vamos a crear sin par de claves pese a que ya sabemos que no es lo recomendado.

![el texto que hemos creado antes](/AWS-labs/lab-4-ELB+ASG/Capturas/2.png)

-Nuevo grupo de seguridad. Activamos permitir el tráfico HTTP. Le damos a "detalles avanzados", vamos donde dice Datos de usuario y pegamos el texto que hemos creado antes-> Lanzar instancia.
Y ahora repetimos el proceso con otra, instancia llamada "Mi instancia 2", pero añadiendo ésta al mismo grupo de seguridad que la primera "launch-wizard-3. Y en esta le ponemos el otro texto.

![Comprobamos que funcionan](/AWS-labs/lab-4-ELB+ASG/Capturas/3.png)

-Comprobamos que funcionan. Copiando las direcciones IP públicas.(Una vez en funcionamiento)

2.**Creación ALB**

![ALBLab4](/AWS-labs/lab-4-ELB+ASG/Capturas/4.png)
![us-east-1a y us-east-1b](/AWS-labs/lab-4-ELB+ASG/Capturas/30.png)

-En EC2 donde dice Equilibrio de carga-> Balanceadores de carga-> Crear balanceador de carga. Y le damos a ALB (Application Load Balancer/Balanceador de carga de aplicaciones). Le voy a dar de nombre ALBLab4. Estará expuesto a Internet y de IPv4. Y vamos a seleccionar us-east-1a y us-east-1b (mínimo).
Donde dice grupos de seguridad(en la creación del ALB, le damos a "cree un nuevo grupo de seguridad", esto nos abrirá otra pestaña donde configurar este grupo. Le pondremos de nombre Gruposeguridad-ALB-Lab4. Esto permitira el HTTP dentro del ALB.

![entrada de HTTP](/AWS-labs/lab-4-ELB+ASG/Capturas/5.png)
![un grupo de destino](/AWS-labs/lab-4-ELB+ASG/Capturas/9.png)
!["TargetGroupLab4"](/AWS-labs/lab-4-ELB+ASG/Capturas/10.png)
 
-Creamos la regla que será una de entrada de HTTP para 0.0.0.0/0(Cualquier origen). Unimos el ALB a ese grupo creado. Y luego donde dice Agentes de escucha y direccionamiento->Crear un grupo de destino (también se nos abrirá otra ventana nueva). Le damos el nombre TargetGroupLab4 y lo dejamos tal cual está, con HTTP.

![2 instancias](/AWS-labs/lab-4-ELB+ASG/Capturas/11.png)
![grupo de destino](/AWS-labs/lab-4-ELB+ASG/Capturas/6.png)

Incluimos como pendientes las 2 instancias que hemos creado, lo creamos y una vez creado volvemos otra vez a la pestaña por donde estabamos creando el ALB y ponemos el TargetGroup4 como grupo de destino. Copiamos el nombre del ALB: ALBLab4-493378900.us-east-1.elb.amazonaws.com.

![Texto 1](/AWS-labs/lab-4-ELB+ASG/Capturas/13.png)
![texto 2](/AWS-labs/lab-4-ELB+ASG/Capturas/14.png)

Y si lo refrescamos varias veces vemos como se van alternando las intancias, con los diferentes textos.

3.**Plantilla de lanzamiento**

![Plantillas de lanzamiento](/AWS-labs/lab-4-ELB+ASG/Capturas/15.png)
![Plantilla-Lab4](/AWS-labs/lab-4-ELB+ASG/Capturas/16.png)
![Ubuntu server](/AWS-labs/lab-4-ELB+ASG/Capturas/17.png)

-En EC2 vamos a la izquierda en el mismo sitio donde dice instancias, hay un lugar que dice Plantillas de lanzamiento, vamos a crear una. Le damos de nombre "Plantilla-Lab4", seleccionamos el tipo de AMI que hemos usado para crear las instancias: Ubuntu Server. Y tipo de servidor t2.micro(de capa gratuita). De grupo de seguridad el "launch-wizard-3". Y pegamos el texto de datos de usuario anterior.

4.**Auto Scaling Group!**

![Auto Scaling](/AWS-labs/lab-4-ELB+ASG/Capturas/18.png)
![ASG-Lab4](/AWS-labs/lab-4-ELB+ASG/Capturas/19.png)
![2 subredes diferentes](/AWS-labs/lab-4-ELB+ASG/Capturas/20.png)
![creado antes TargetGroupLab4](/AWS-labs/lab-4-ELB+ASG/Capturas/21.png)

-Después de crear el template. Vamos a Grupos de Auto Scaling y creamos uno que vamos a llamar "ASG-Lab4". Seleccionamos Plantilla-Lab4 como plantilla de lanzamiento. Ponemos 2 subredes diferentes como zona de disponibilidad(para alta disponibilidad). La asociamos a un balanceador existente y elegimos el grupo destino que hemos creado antes "TargetGroupLab4".

![comprobaciones de estado de ELB](/AWS-labs/lab-4-ELB+ASG/Capturas/22.png)
![Configuramos el tamaño del grupo](/AWS-labs/lab-4-ELB+ASG/Capturas/23.png)
![una política de escalado de seguimiento de destino](/AWS-labs/lab-4-ELB+ASG/Capturas/24.png)

-Activamos las comprobaciones de estado de ELB. Configuramos el tamaño del grupo: de capacidad deseada 2, de mínima capacidad 1 y de máxima 3. Seleccionamos una política de escalado de seguimiento de destino (Target Tracking Policy), tipo de métrica  Utilización de CPU y como valor destino 70%. Todo lo demás, siguiente y siguiente.
Ahora Launch Template crea 2 instancias nuevas que sustituyen a las que ya teníamos y se registrarán en el Target Group del ALB. Y lo que pasará es que si la CPU supera el 70%, el ASH añadirá otra instancia automáticamente.

5.**Instance connect**

![nos conectemos con IP pública](/AWS-labs/lab-4-ELB+ASG/Capturas/25.png)
![Una vez dentro](/AWS-labs/lab-4-ELB+ASG/Capturas/26.png)

-Una vez configurado si voy a una de mis instancias y la selecciono, puedo darle donde dice conectar, una vez nos conectemos con IP pública y podremos entrar vía Instance Connect. Una vez dentro hacemos un _sudo apt-get update && sudo apt-get install_ -y _stress-ng_.

![durante 5 minutos](/AWS-labs/lab-4-ELB+ASG/Capturas/28.png)
![se creará otra más](/AWS-labs/lab-4-ELB+ASG/Capturas/29.png)
![se creará otra más](/AWS-labs/lab-4-ELB+ASG/Capturas/29.png)

-Una vez tengamos instalado stress-ng, lo ejecutamos durante 5 minutos con el comando _stress-ng --cpu 1 --timeout 300s_. Esto hará que a parte de las instancias que tenemos se creará otra más(se escalará a 3). Se autoescalará debido a stress-ng porque superará el 70% de CPU.

#Con esto creamos un servicio altamente disponible con EC2, ELB y ASG.
