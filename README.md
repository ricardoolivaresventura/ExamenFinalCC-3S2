# ExamenFinalCC-3S2
ExamenFinalCC-3S2 curso Desarrollo de Software

# Pregunta 1
¿Cómo pueden los clientes encontrar microservicios y sus instancias?
Cuando tenemos un microservicio y lo instanciamos, a cada instancia se le asigna una dirección IP dinámica, al ser esta dirección IP dinámica, esto dificulta que un cliente pueda realizar la solicitud a dicha instancia, por tal motivo, cuando utilizamos una infraestructura de microservicios se expone una API REST a través del protocolo HTTP, de tal manera que el cliente realiza las peticiones contra esta API y de esta manera se puede comunciar con el microservicio.

# Pregunta 2
Cuando tenemos una infraestructura de microservicios, muchas veces se suelen ocultar algunos microservicios del acceso externo, es decir no se puede acceder directamente a ellos ni tampoco mediante una API REST, pero sí se pueden acceder de manera indirecta, ya que, hay otros microservicios que sí se liberan para ser usados por algún cliente externo y estos microservicios "públicos" internamente pueden hacer uso de los microservicios que están ocultos. Ahora, estos microservicios que están públicos, deben estar protegidos contra las solicitudes de clientes malintencionados, ya que, todo el sistema se puede ver comprometido. Entonces, para prevenir cualquier ataque lo que podemos hacer es implementar medidas de seguridad, tales como:
- Podemos implementar un firewall, con esto podemos proteger los microservicios del acceso no autorizado y no verificado.
- Implementar un sistema robuesto de autorización y autenticación, esto lo podemos ver en la mayoría de sistemas, por no decir todos, generalmente se suele usar OAuth para implementar estos sistemas, ya que, es un estándar utilizado por grandes aplicaciones del mercado.
- Otra forma de protección para los microservicios, es haberlos desarrollado con buenas prácticas y con tolerancia a fallos, es decir, si en algún momento el microservicio es vulnerado, entonces deberá seguir funcionando correctamente, a pesar del fallo de uno o varios de sus componentes debido a la vulneración que sufrió. Esto puede servir para aquellas aplicaciones que son utilizadas por miles de usuarios a diario y que si deja de funcionar, entonces muchos usuarios pueden perder horas valiosas de su tiempo o incluso perder información valiosa y eso es algo que se quiere evitar a toda costa.

# Pregunta 3
El realizar solicitudes sincrónicas puede llevar a una mala experiencia de usuario, ya que, la aplicación o sistema se suele bloquear hasta que la solicitud sea respondida. Es decir, si realizar una solicitud muy pesada que involucra a varios microservicios, entonces el tiempo de respuesta será muy elevado. La solución más apropiada sería utilizar una comunicación asincrónica. Este tipo de comunicación no bloquea E/S, sino devuelve el control al flujo inicial sin esperar una respuesta. Con este tipo de comunicación se suele liberar el hilo de solicitud de manera que se puedan manejar más solicitudes a pesar que no hayan subprocesos disponibles, debido a que, a diferencia de la comunicación sincrónica, esta crea como una cola de solicitudes que se van tomando a medida que se liberan los recursos disponibles del sistema operativo. Otro beneficio de la asincronicidad es que evitamos los largos tiempos muertos que ocurren con la comunicación sincrónica. Un claro ejemplo podría ser Youtube, cuando vemos un video, este se va cargando a medida que nosotros vamos avanzando en el video, en este caso se está usando la comunicación asincrónica, caso contrario, youtube se bloquearía a cada instante esperando la respuesta del microservicio para cargar más minutos del video.

# Responde e implementa cada una de las siguiente preguntas relacionadas a las actividades desarrolladas en clase.

# 1
Ejecuta couchDB como un contenedor Docker y publica su puerto, de la siguiente manera
a. Ejecuta el contenedor
- Con el comando "docker run couchdb" ejecutamos la imagen couchdb como contenedor
b. Publica el puerto de couchDB
