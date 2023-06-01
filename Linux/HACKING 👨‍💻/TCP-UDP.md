-----
- Tags: #Nmap #TCP #Three-way-handshake #UDP #NMAP-sS
-------

### TCP
Es un protocolo de la capa de transporte que se encarga de la transmisión de datos de forma segura, para ello utiliza un método de transmisión por confirmación, también llamado el "Three Way Handshake".
Cuando un dispositivo inicia una comunicación por un puerto TCP a través de un servicio;
1. Lo primero que hace es mandarle un paquete de inicio de sesión (SYN), 
2. Después el receptor responde con un paquete de confirmación indicando que efectivamente está activo el puerto por el que va a iniciarse la sesión (SYN ACK),  
3. Finalmente el dispositivo emisor envía un nuevo paquete indicando que ha confirmado la respuesta del receptor y ahora ambos dispositivos saben que van a iniciar una comunicación por ese puerto(paquete ACK). 

Ahora cada vez que el emisor envié un paquete de datos el receptor, este devolverá un mensaje de confirmación al dispositivo emisor indicando que le ha llegado el paquete (ACK), este paquete se conoce como **acknowlage**. Y así es como funcionará la comunicación de aquí en adelante, el emisor envía un paquete y espera la respuesta del servidor (ACK) para enviar el siguiente paquete, en caso de que no reciba el ACK por parte del servidor pués volverá a enviar el mismo paquete de datos asegurándose así que los datos lleguen a su destino.

> [[NMAP]] recurre de este proceso, el Three Way Handshake, para averiguar si un puerto está activo o cerrado, ya que sabiendo si el puerto está activo o cerrado podemos saber también el tipo de servicio que corre por detras. Cada puerto  se utiliza por un servicio en concreto, para el servicio ssh utiliza el puerto 22, para el FTP el puerto 20 y 21, para las páginas webs el puerto 80 y para las páginas webs seguras con certificado TLS el puerto 443. Sabiendo esto podemos enumerar todos los puertos que están activos y descubrir los servicios que corren detrás de esos puertos.

### Nmap el parámetro -sS
Sabiendo esto podemos explicar ahora que es lo que hace el -sS (escaneo TCP SYN), nmap envía un paquete SYN al servidor y espera a que este le conteste con un paquete (SYN ACK) en caso de que esté abierto, si el servidor no tiene el puerto abierto entonces enviará un paquete **RST** (RESET||REICINIO), indicando que el puerto se encuentra cerrado y no está dispuesto a iniciar ninguna sesión. 
Si de lo contrario el servidor responde con un SYN ACK entonces el emisor entenderá que el puerto está abierto.
En ese caso Nmap envía un paquete RST después de recibir el paquete SYN-ACK para limpiar la conexión sin establecer una conexión completa. Esto se hace por varias razones:

1. **Eficiencia**: Al no establecer una conexión completa, se ahorra tiempo y recursos, ya que Nmap no necesita finalizar la conexión de manera formal antes de continuar con el escaneo de otros puertos.
    
2. **Limpieza de registros**: Al enviar un paquete RST, Nmap asegura que no se generen registros de sesión innecesarios en el servidor escaneado. Sin embargo, es importante tener en cuenta que esto no garantiza eliminar todos los registros de sesión en el servidor, ya que puede haber otras formas de registro o monitoreo de actividades en el sistema.
    
3. **Menor impacto**: Al no completar la conexión, Nmap evita el establecimiento de una conexión real y cualquier interacción adicional que pueda desencadenar respuestas o comportamientos no deseados en el servidor escaneado.

### UDP
El protocolo UDP se caracteriza por su velocidad y falta de confirmación de entrega, lo que lo hace menos confiable pero más rápido que TCP. Se utiliza en situaciones donde la velocidad de transmisión es más importante que la integridad de los datos, como en aplicaciones de streaming en tiempo real, donde se prioriza la reproducción continua del contenido.(Esto significa que el emisor simplemente envía los datos al receptor sin preocuparse si estos llegan correctamente o no)

### Relacionados
---
- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se muestra en SEC2 'CONCEPTOS BÁSICOS' 