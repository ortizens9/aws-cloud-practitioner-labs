# [Introduction to Amazon Virtual Private Cloud](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/1.png)
Acabo de hacer un Lab de Amazon llamado [_“Introduction to Amazon VPC”_](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/2.png).
Para que tanto vosotros como yo, vayamos entendiendo qué hacemos y qué nos pide y qué estamos viendo. Que ya de por si nos da unas instrucciones. Voy a explicar mejor algunos conceptos.

## El primer objetivo de este lab es crear la VPC con el asistente de VPC

·**Una VPC** es una nube privada, donde los clientes pueden hacer lo que podrían hacer en una nube privada normal, pero esta nube está alojada en la nube.

<ins> **Diferencias entre Private Cloud(Nube privada) vs Virtual Private Cloud(Nube Privada Virtual)** </ins>

·**Una nube privada** es una infraestructura dedicada a una sola organización. Esta puede ser on-premise(en tu hardware físico) o alojada por un tercero, pero esta **no se comparte con nadie**, es de un tenedor. Tu te ocupas completamente del mantenimiento, el costo es elevado y tienes el control total.

·**La Virtual Private Cloud** es una nube privada pero está aislada dentro de una nube pública. Tu red es privada pero el hardware **es compartido**, es de múltiples tenedores(diferentes empresas, etc).
Su costo es bajo, pagas por lo que usas y el mantenimiento lo hace el proveedor, ya sea AWS, Azure en el caso de Microsoft o Google en el caso de GDP. Tienes el control total a nivel lógico.

Cada VPC tiene su bloque CIDR(Enrutamiento entre dominios sin clase) de IPs privadas, **este bloque grande**, lo divides en subredes que tiene sus propios rangos dentro de este.

En este lab [nos pide](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/3.png) que creemos dentro de la VPC una subred pública _(10.0.25.0/24)_ y una privada _(10.0.50.0/24)_. En el bloque que en este caso es el _10.0.0.0/16_. Con la puerta de enlace en una sola **Zona de disponibilidad**. Y sin ningún punto de enlace. [Todo esto con el asistente](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/4.png. Después de esto nos pide que copiemos el _ID de la VPC_ y lo peguemos en un editor de texto.

## Como segundo objetivo, nos anima a explorar la VPC.

Yendo a esta y [observando sus diferentes características](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/5.png). Viendo por ejemplo su puerta de enlace. La puerta de enlace de internet(**Internet Gateway**) conecta la VPC a Internet.

Ahora nos dice que vayamos a [Subredes](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/6.png). **Las subredes** existen únicamente en una zona de disponibilidad, y tiene un rango o intervalo de direcciones IP.
Si hacemos clic a una subred, veremos que cada una tiene un ID único, y que cada subred tiene 251 IP disponibles de 256 ya que las otras 5 están reservadas para: dirección de red, router vlc, dns de Amazon, una para futuro uso y  direcciónn de broadcast.

Cada subred está asignada a una tabla de enrutamiento que especifica las rutas que sigue el tráfico que sale de la subred. Indica hacia dónde se debe dirigir el tráfico en función del destino. Estas no filtran el tráfico, solo lo dirigen.

Para [filtrar el tráfico](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/7.png) las subredes tienen algo llamado **Access Control List**(ACLs), que permiten y deniegan. Estas por defecto permiten todo el tráfico entrante y saliente.

_No se puede acceder directamente a las subredes privadas desde Internet_, estas tienen una capa adicional de seguridad.
Existe algo llamado puertas de enlace de direcciones de red(NAT) o **NAT gateways**, que permiten que los recursos que están dentro de la subred privada [tengan conexión a internet](/AWS-labs-oficiales/Lab1-IntroductiontoVLC/Capturas/8.png).

Después de estos pasos, realizamos un cuestionario relacionado con esto para ver si lo hemos entendido.
