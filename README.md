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

# Pregunta 4
- ¿Cómo obtengo una imagen completa de la configuración que existe para todas las instancias de microservicio en ejecución?
Los microservivios se suben a un servidor para que esté disponible para los clientes, en la configuración de este servidor podemos agregar todas las variables de entorno, configuraciones, comandos para ejecutar diferentes scripts, etc y como estos microservicios están subidos en este servidor, entonces pueden acceder a ellos. Y al tener toda esta información disponible, entonces simplemente podemos construir su imagen, el cual podemos almacenarlo en este servidor o en otro y simplemente para usarlo en estos microservicios en ejecución tendremos que bajar la imagen y ejecutarla.
- ¿Cómo actualizar la configuración y me aseguro de que todas las instancias de microservicio afectadas se actualicen correctamente?
Podríamos tener un script el cual tendrá comandos que descarguen la última versión de la imagen que contiene la configuración, entonces cuando se actualiza esta imagen, simplemente ejecutamos el script y todas las instancias de los microservicios que utilizan esta imagen se actualizarán correctamente

# Pregunta 5
Antes de responder a las preguntas, daremos una breve definición de los logs, los cuales nos informan de todo aquello que pueda estar funcionando de forma incorrecta dentro de un sistema y, para nuestro caso, nos puede informar qué está fallando en nuestra infraestructura de microservicios.

- ¿Cómo se obtiene una descripción general de lo que sucede en el entorno del sistema cuando cada instancia de microservicio escribe en su propio archivo log local?
Para obtener una descripción general de los logs de los microservicios, necesitamos unificarlos a esto se le llama "centralización de logs". Este método consiste en centralizar, unir o recoger los logs de todos los microservicios y mandarlos a un servidor, en el cual se ejecutará un programa capaz de analizar todos los logs recolectados. De esta manera es como podemos obtener una descripción general de lo que ocurre en el sistema, ya que, tendremos todos los logs reunidos en un único punto. La buena noticia es que ya existen muchos servicios en el mercado que nos pueden ayudar con esto, por ejemplo, Datadog, Fluentd, Graylog o el mismo AWS (Cloudwatch) que expone toda una interfaz en la cual se pueden visualizar todos los logs de un sistema.

- ¿Cómo averiguo si alguna de las instancias de microservicio tiene problemas y comienza a escribir mensajes de error en sus archivos logs?
En la pregunta anterior a esta se mencionó algunos softwares que nos ayudan con el monitoreo de los logs de todos los microservicios, entonces en el registro unificado de estos softwares podemos ver cuándo una instancia en específico falla.

- Si los usuarios finales comienzan a informar problemas ¿Cómo puedo encontrar mensajes logs relacionados? Es decir, ¿cómo puedo identificar qué instancia de microservicio es la causa raíz del problema?
Generalmente lo que se hace es lo siguiente, si el usuario reporta un problema sobre cierta pantalla de una aplicación, entonces el desarrollador acude a esa pantalla en ambiente de stagging o sandbox, realiza las pruebas pertinentes para ver qué puede estar fallando con el microservicio que se utiliza en dicha pantalla, del error obtenido también podemos obtener el "trace-id", el cual es un código que nos permite identificar la solicitud, entonces el desarrollador pasa este código al equipo de DevOps para que desde el software, que utilizan para gestionar los logs (por ejemplo, Cloudwatch), pueda buscar los logs correspondientes a este trace id, además en dicho log también se puede ver qué ha fallado e incluso cuál es el nombre o identificador del microservicio que ha fallado, entonces una vez identificado el microservicio que falló, el equipo de DevOps se lo puede comunicar al equipo de Backend para que realice el correspondiente fix al microservicio que falló

# Pregunta 6
- Si los usuarios finales comienzan a presentar casos de soporte con respecto a una falla específica ¿Cómo podemos identificar el microservicio que causó el problema, es decir, la causa raíz?
Al igual que el último item de la pregunta 6, lo que podemos hacer es obtener el traceId de la petición y utilizarlo en el software que empleamos para gestionar los logs, aquí podemos buscar los logs correspondientes a este traceId, además al encontrar dichos logs, también podemos ver todos los microservicios involucrados en esta petición y, así mismo, saber qué microservicio(s) fallan para poder solucionarlo.

- Si un caso de soporte menciona problemas relacionados con una entidad específica, por ejemplo, un número de pedido específico ¿Cómo podemos encontrar mensajes de registro relacionados con el procesamiento de este pedido específico, por ejemplo, mensajes logs de todos los microservicios que estuvieron involucrados en su procesamiento?
Lo que podríamos hacer es agarrar este número de pedido específico y pasarlo como parámetro a la API correspondiente, en caso de obtener el error podemos obtener el traceId y con este código podemos rastrear todos los logs en el software, por ejemplo, cloudWatch y de esa manera podríamos ver la causa del error, así como también qué microservicio o cuáles son los microservicios que fallarán. Luego, el equipo de backend se deberá encargar de fixear los componentes que ocasionan el fallo de dichos microservicios

- Si los usuarios finales comienzan a presentar casos de soporte relacionados con un tiempo de respuesta inaceptablemente largo, ¿Cómo podemos identificar qué microservicio en una cadena de llamadas está causando la demora?
Es básicamente lo mismo que en los items anteriores, obtener el traceId, identificar el microservicio "A" que se utiliza, luego ver qué otros microservicios están siendo utilizados por este microservicio, luego analizar cada microservicio, de la siguiente manera, podemos realizar peticiones a estos microservicios y ver el tiempo de respuesta de cada uno de ellos y así poder identificar cuál es el que está generando que el microservicio "A" se demora mucho en responder.

# Responde e implementa cada una de las siguiente preguntas relacionadas a las actividades desarrolladas en clase.

# 1
Ejecuta couchDB como un contenedor Docker y publica su puerto, de la siguiente manera
a. Ejecuta el contenedor. Con el comando "docker run couchdb" ejecutamos la imagen couchdb como contenedor
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/docker-couchdb.PNG "")
b. Publica el puerto de couchDB
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/publish-couchdb.PNG "")

# 2
Crear una imagen de Docker con un servicio REST, respondiendo Hola Amigos CC-3S2 a localhost:8080/hola. Utiliza el lenguaje y el framework que prefieras.
a. Crear una aplicación web
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/api-rest-flask.PNG "")

b. Crear un Dockerfile para instalar dependencias y librerías

![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/flask-dockerfile.PNG "")

c. Construye la imagen

![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/image-flask+.PNG "")

d. Ejecuta el contenedor que publica el puerto

![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/run-flask.PNG "")

e. Verifica que se esté ejecutando correctamente utilizando el navegador

![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/api-rest-localhost.PNG "")

# 4
a. Crea un pipeline que ejecuta un script de Ruby que imprima Hola Mundo desde Ruby:
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/hola-mundo-ruby.PNG "")

b y c. Utiliza el siguiente comando de shell para crear el script hola.rb sobre la marcha y agregue el comando para ejecutar hola.rb
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/run-ruby.PNG "")

# 5
Crea un programa de Python que multiplique, sume, reste, divide dos números pasados como parámetros de línea de comandos. Agrega pruebas unitarias y publica el proyecto en Github
a. Crea dos archivos: calculador.py y test_calculador.py
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/calculador-python.PNG "")

b. Puedes usar la biblioteca unittest
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/test_calculador.PNG "")

c. Ejecutar el programa y la prueba unitaria
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/execute-calculador.PNG "")
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/execute-test-calculador.PNG "")

d. Subir a Github
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/calculadora-python-github.PNG "")

# 6
Crea el pipeline de integración continua para el proyecto de calculadora de Python
a. Usa Jenkinsfile para especificar el pipeline
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/calculador-python-jenkinsfile.PNG "")
b y c. Configura el trigger para que el pipeline se ejecute automáticamente en caso de que se haga commit en el repositorio. Python no Necesito el paso compile porque es un lenguaje interpretado
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/calculador-python-jenkinsfile-triggers.PNG "")
d. Ejecuta el pipeline y observa los resultados
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/ExamenFinalCC-3S2/main/execute-calculador-pipeline.PNG "")

