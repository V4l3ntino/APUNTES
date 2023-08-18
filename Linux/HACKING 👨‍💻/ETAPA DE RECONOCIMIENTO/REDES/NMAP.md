-----
- Tags: #Linux #Nmap #Hacking #Escaneo #Reconocimiento #Wireshark #tcpdump
------
- **-p**: indica el rango de puertos que se quiere escanear, podemos indicarle un puerto
específico, un rango de puertos o indicarle que escanee todo los puertos,
- **-vvv**: triple verbose sirve para que mientras se está ejecutando el escaneo se reporte todos
los resultados por pantalla, con una sola *v* también funciona pero agregando tres nos
mostraría información adicional sobre los paquetes enviados y recibidos durante el escaneo..
Esto permite agilizar el trabajo porque no tienes que esperar hasta que el escaneo concluya.
- **--open**: este parámetro sirve para que solo muestre por pantalla aquellos puertos que están
abiertos
- **-sT**: indica que realice el escaneo de tipo TCP Connect. Este tipo de escaneo se basa en establecer una conexión TCP completa con el objetivo de determinar si el puerto está abierto, cerrado o filtrado.
- **-sU**: indica que realice el escaneo de tipo UDP. Este tipo de escaneo se basa en establecer una conexión UDP con el objetivo de determinar si el puerto está abierto, cerrado o filtrado.
- **-sS**: lo explico mejor en este enlace.([[TCP-UDP]])
- **--min-rate**: este parámetro sirve para indicar cuantos paquetes quieres que se tramite en un
segundo.
- **-F**: (que significa "Fast Scan" o "Escaneo Rápido") es una opción predefinida en Nmap que escanea un conjunto limitado de puertos comunes y rápidos. Este conjunto incluye los puertos más utilizados y relevantes, como el puerto 80 para HTTP, el puerto 443 para HTTPS, entre otros. El objetivo del escaneo rápido es identificar rápidamente los servicios expuestos en un objetivo sin realizar un escaneo exhaustivo de todos los puertos posibles.(No recomendable puede dar falsos positivos)
- **--top-ports**: escanea los puertos más comunes de la cantidad que le especifiques.
- **-n**: sirve para indicar que no quieres que se aplique la resolución dns en el scaneo ya que
esto podría ralentizar el escaneo en algunos casos.
- **-Pn**: sirve para indicar que no realice un ping al host.
Por defecto, Nmap utiliza un método de ping para descubrir si el host está activo antes de
comenzar el escaneo, lo que puede ser útil para reducir el tiempo de escaneo en redes
grandes, pero puede dar resultados falsos negativos en algunos casos (por ejemplo, cuando
el host está configurado para no responder a los ping). Desactivando esta funcionalidad
Nmap intentará realizar el escaneo directamente, sin verificar si el host está en línea o no.
Esto puede ser útil en situaciones en las que se sabe que el host objetivo no responde a los
ping, pero aún se desea realizar un escaneo de puertos.
- **-o**: exporta los resultados del escaneo a un archivo.
- **-oN**: esto exporta los datos en un archivo en formato nmap. El formato nmap lo que hace es
representar la información tal y como se representó en consola.
- **-oG**: con este parámetro estaríamos indicando que los resultados del escaneo se exporten a
un archivo de salida en formato grepeable. Esto es muy útil porque nos ayuda a realizar
búsquedas y análisis de manera precisa y eficiente mediante comandos de texto.
- **-sV**: nos indica la versión y el servicio que hay por detrás de esa máquina que estamos
escaneando.
- **-sC**: con este parámetro estaríamos aplicando un conjunto de scripts básicos de nmap que
nos puede ayudar para recopilar información adicional sobre los servicios que se están
ejecutando en los puertos escaneados.
- **-sCV**: es la combinación de las dos opciones: "-sC" y "-sV". Nos permite realizar una
exploración exhaustiva de los servicios que se están ejecutando en los puertos escaneados.
Esto incluye la detección de versiones de los servicios, así como la ejecución de scripts de
enumeración predeterminados para recopilar información adicional sobre los servicios.
- **–sA**: se utiliza para detectar si existe algún firewalls que esté corriendo por detrás
- **-A**: Esta opción incluye varios sub-parámetros que se ejecutan en conjunto, como el escaneo
de puertos, detección de versiones, detección de scripts y otros. Por lo que con esta opción
podemos habilitar la detección de sistema operativo y versión del software que se está
ejecutando en los puertos que se están escaneando.
- **-O**: se utiliza para realizar una detección del sistema operativo de los dispositivos de red que
se están escaneando. Nmap utiliza técnicas de fingerprinting (huellas dactilares) para
identificar el sistema operativo.
- **-T4**: Esta opción establece el tiempo de retardo entre paquetes de Nmap. El valor "4" es el
máximo posible e indica que el escaneo se realizará a una velocidad agresiva, lo que
acelerará el proceso de escaneo pero también aumentará la probabilidad de que algunos
paquetes sean descartados o ignorados por el sistema remoto o los firewalls. Los valores que
existen son: 0, 1, 2, 3, 4. Siendo el 0 el valor más bajo que haga que el escaneo sea más lento
pero más discreto y el 4 donde el escaneo sea más rápido pero menos sigiloso(Mayor número de logs en el sistema). 

> 	Nmap por defecto realiza el escaneo con el protocolo TCP.

### Estados de un puerto
----
- **Abierto**
- **Cerrado**
- **Filtrado>** nmap no es capaz de decidir con certeza si el puerto se encuentra abierto o filtrado **(Esto no indica que el puerto esté cerrado)**. Esto se debe a que puede haber un firewall de por medio que esté molestando.


### Práctica 1 (Escaneos sencillos)
-----
Filtrar por puertos
```bash
nmap -p22 192.168.0.122
nmap -p20,21,22 192.168.0.122
nmap -p1-100 192.168.0.122
nmap -p1-65535 <====> nmap -p- 192.168.0.122

```

Filtrar por lo puertos más comunes que especifiques.
```bash
nmap --top-ports 500 192.168.0.122
nmap --top-ports 200 192.168.0.122
nmap --top-ports 100 192.168.0.122
```

Filtrar por puertos que estén únicamente abiertos.
```bash
nmap -p1-1000 --open 192.168.0.122
```

Agilizar el escaneo
```bash
nmap -p- --open -n -T5 192.168.0.122
```

Filtrar por puertos abiertos especificando el protocolo TCP conncet. 
```bash
nmap -p22 --open -sT -v -n 192.168.0.122
```

Filtrar por las versiones de los servicios que corren detrás de los puertos.
```bash
nmap -p22 -sV 192.168.0.122
nmap -p22,80 -sV 192.168.0.122
```

Reportar el tipo de sistema operativo que corre por detrás de la máquina.(No recomendable aplicar porque es muy agresivo y realiza muchas peticiones.)
```bash
nmap -O 192.168.0.122
```

>Es mejor fijarnos en el TTL (Time To Live), representa el número de saltos que un paquete puede dar hasta llegar hasta su destino. Los paquetes son enrutados por distintos routers externos en interntet hasta llegar a su destino, pues bien por cada router que pasan el ttl disminuye -1. Esto es necesario porque los paquetes no siempre llegarán a su destino y para que no estén generando tráfico innecesario se le da un tiempo de vida, así se evita problemas de congestión en la red.
>	- Windows => 128 TTL
>	- Linux => 64 TTL
### Puertos filtrados, evadir un firewall con nmap
-----
Si tenemos un firewall de por medio que nos impida ver si un puerto está abierto o cerrado podemos hacer lo siguiente:
- **-f**: en Nmap se utiliza para realizar escaneos utilizando técnicas de fragmentación de paquetes, con el objetivo de evadir la detección de algunos firewalls que pueden estar configurados para bloquear paquetes completos. Sin embargo, la efectividad de esta técnica puede variar según la configuración y las capacidades del firewall en cuestión.
- **--mtu**: (Maximum transmission unit) **Unidad máxima de transmisión**, se utiliza para determinar el tamaño máximo de cada paquete en cualquier transmisión. El valor que le vallas a poner deberá ser mayor de 0 y múltiplo de 8 ya que lo que le estás indicando es el número de bytes máximo que va a tener cada segmento de datos. 
	Esto servirá para que cuando los datos del paquete superen el **mtu** indicado se **fragmenten a tantas unidades necesarias** para **reducir el tamaño de los datos** y que sea inferior al mtu. 
	Sabiendo esto podemos **jugar** con el tamaño del **mtu** de cada paquete y decidir si queremos enviar cada paquete con más o menos números de fragmentación, ya que al poner un **mtu bajo** como resultado los segmentos se fragmentarán a un **mayor número de unidades** y viceversa, al poner un **mtu alto** como resultado los segmentos se enviarán en un **menor número de fragmentos** o incluso sin llegar a fragmentarse.

### IDS
----
> Intrusion Detection System, es un dispositivo o aplicación de software que supervisa una red en busca de actividades maliciosas o violaciones de las políticas. Cualquier actividad maliciosa o infracción suele notificarse o recopilarse de forma centralizada mediante un sistema de gestión de eventos e información de seguridad.

Con nmap tenemos un parámetro para poder camuflar nuestra ip y evitar ser detectados:
**-D**: cuando se utiliza el parámetro -D con una lista de direcciones IP, Nmap envía paquetes de escaneo desde la dirección IP objetivo real junto con las direcciones IP de "engaño" especificadas. El objetivo de esto es confundir a los sistemas de detección de intrusiones y ocultar la dirección IP real del escaneo.(Hay que tener en cuenta que todo esto funciona solo en redes privadas, al salir a internet  este parámetro no funciona.)

### Establecer un puerto origen
----
Imagina que hay un firewall con una whitelist que permite filtrar datos únicamente a un rango de puertos determinados, nmap cuando realiza un escaneo abre un puerto aleatorio y tramita la solicitud por ese puerto, pues bien podríamos especificarle a nmap un puerto origen determinado y poder así acceder a la whitelist.
```bash
nmap -p22 --source-port 8080
```

### Spoofear la dirección mac 
---
Nmap tiene implementado un parámetro que no permite cambiar nuestra dirección mac al realizar el escaneo. Esto podría ser útil en caso de que haya una whitelist donde solo estén permitidas las comunicaciones con determinadas direcciones mac. También nos da cierto anonimato ya que no estaríamos exponiendo directamente nuestra dirección mac.
En caso de no queramos usar este parámetro podemos recurrir de [[Macchanger]] para cambiar la mac. También puedes ver el siguiente script donde te automatiza el proceso.[[Script para cambiar la mac]]

```bash
nmap -p22 192.168.0.122 --spoof-mac Samsung -Pn #Con esto indicamos que nos cambie la mac por una cuyo OUI sea de samsung
nmap -p22 192.168.0.122 --spoof-mac X.X.X.X.X.X -Pn # Con esto podemos indicar una dirección mac específica, la que nosotros queramos.
```

### Longitud de un paquete
----
Cuando se realiza un escaneo de puertos nmap manda paquetes de reconocimiento, esto paquetes tienen una longitud de datos predeterminada. Un firewall puede tener implementada una blacklist que bloquee los paquetes que coincidan con una logitud determinada para evitar escaneos. 
Pues bien podemos usar el parámetro **--data-length** para establecer una longitud distinta, es decir si ponemos un número al azar lo que hará nmap es sumarle la longitud base del paquete la cantidad que le hallamos especificado. Cambiando así la longitud de datos por defecto y saltándonos la blacklist del firewall.
```bash
nmap -p22 192.168.0.122 --data-length 29 
```

### Práctica 2 (Posibles escaneos para burlar un firewall)
----
Escanear un puerto fragmentando paquetes
```bash
namp -p22 -f 192.168.0.122 
```

Escanear un puerto indicando el tamaño máximo de cada paquete
```bash
nmap -p22 --mtu 8 192.168.0.122
```

Escanear un puerto camuflando nuestra ip
```bash
nmap -p22 192.168.0.122 -D 192.168.0.22,192.168.0.23,192.168.0.24,192.168.0.25,192.168.0.26,192.168.0.39 
```

Escanear un puerto spofeando la dirección mac por otra. 
```bash
nmap -p22 192.168.0.122 --spoof-mac Apple -Pn
```

Escanear un puerto jugando con la longitud de datos del paquete.
```bash
nmap -p22 192.168.0.122 --data-length 88
```

Escanear un puerto estableciendo un puerto origen.
```bash
nmap -p22 192.168.0.122 --source-port 8080
```

### Scripts de Nmap 
Existen una serie de scripts que te permiten reportar más información acerca de los servicios que corren detrás, usando el parámetro -sC nos ejecutaría un conjunto de scripts básicos para el reconocimiento. Es conveniente que este parámetro siempre valla acompañado del -sV para reportar la versión. También se pueden combinar estos dos parámetros y poner -sCV que va ser lo mismo que si lo pones por separado
```bash
nmap -p22 -sC -sV 192.168.0.122
nmap -p22 -sCV 192.168.0.122
```

> También puedes ejecutar scripts concretos de nmap según la categoría a la que pertenecen:
```bash
nmap -p22 192.168.0.122 --script="vuln and safe"
```
Ejecuta scripts de NSE (Nmap Scripting Engine) que están etiquetados como "vuln" (vulnerabilidad) y "safe" (seguro). Esto significa que se ejecutarán scripts específicos que buscan vulnerabilidades conocidas en el servicio SSH, pero solo aquellos scripts considerados seguros para evitar posibles problemas o daños en el objetivo.

### Fuzzing nmap
El fuzzing es una técnica utilizada ampliamente para el reconocimiento de rutas y directorios generalmente en una página web. Lo que hace es aplicar fuerza bruta probando un conjunto de rutas más comunes que están predefinidas en una lista y va probando una por una con el fin de encontrar rutas existentes en el sistema.
```bash
nmap -p80 192.168.0.1 --script http-enum
```
### TCPDUMP
---
Con la herramienta tcp dump podremos capturar paquetes de red y volcarlas a un archivo con extensión .cap para luego visualizar el contenido con [[Wireshark-Tishark]].
``` bash
tcpdump -i wlan0 -w Captura.cap -v
```

- -i: para especificar la interfaz
- -w: (writte)para guardar el output en un archivo
- -v: verbose para que nos muestre contenido por consola mientras se esté ejecutando.

### Práctica fuzzing local
Para practicar con nmap haciendo fuzzing podemos montarnos un sertvidor temporal http en python3 y luego probar hacer el ataque. Mientras ejecutamos el ataque podemos también poner en captura los paquetes con tcpdump y luego visualizar la información con tshark o con wireshark
```bash
sudo python3 -m http.server 80
sudo tcpdump -i lo -w captura.cap -v
sudo nmap -p80 127.0.0.1 --script http-enum
```

Esto es para hacerlo en local, lógicamente cuando quieras hacerlo con un dispositivo en la red tienes que adaptarlo especificando la interfaz en tcpdump y la ip destino en nmap.

-----
### Relacionados 

- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se muestra en la carpeta 1-6 de la SEC3
- [[ARP-SCAN]]
- [[MASSCAN]]
- [[Wireshark-Tishark]]