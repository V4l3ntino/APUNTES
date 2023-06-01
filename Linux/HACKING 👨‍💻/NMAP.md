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


### Prácticas
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

### TCPDUMP
---
Con la herramienta tcp dump podremos capturar paquetes de red y volcarlas a un archivo con extensión .cap para luego visualizar el contenido con wireshark.
``` bash
tcpdump -i wlan0 -w Captura.cap -v
```

- -i: para especificar la interfaz
- -w: (writte)para guardar el output en un archivo
- -v: verbose para que nos muestre contenido por consola mientras se esté ejecutando.

-----
### Relacionados 

- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se muestra en la carpeta 1 de la SEC3
- [[ARP-SCAN]]