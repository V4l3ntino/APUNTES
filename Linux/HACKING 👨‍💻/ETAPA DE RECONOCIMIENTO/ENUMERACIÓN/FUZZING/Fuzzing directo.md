----
- Tags: #Linux #Fuzzing #Recopilación 
-----

Vamos a tirar de herramientas para la recolección de rutas en una url por fuerza bruta. A través de un diccionario iremos probando posibles rutas y recopilando aquellas que existen. También con los subdominios.
### SECLIST
Seclist es un repositorio de github que nos ofrece múltiples diccionarios para ataques de cualquier situación, viene bien tener este repositorio en este caso.
```bash
sudo git clone https://github.com/danielmiessler/SecLists.git
```

### Gobuster
-----------
Es una herramienta que podemos encontrar en [github](https://github.com/OJ/gobuster).
### Instalación
```bash
git clone https://github.com/OJ/gobuster.git
cd gobuster
go build .
```

### Uso
Enumerar subdominios
```bash
./gobuster vhost -u https://google.com -w /home/valen/diccionario.txt -t 20
./gobuster vhost -u https://google.com -w /home/valen/diccionarios.txt -t 20 | grep -v "403" #Con grep -v quito las líneas con cadenas 403.
```

- -u: para indicar una URL
- -w: ruta donde se encuentra el diccionarios (WORDLIST)
- -t: lanzar hilos (THREADS) que sirven para realizar múltiples tareas en paralelo, esto agiliza el escaneo

Enumerar rutas
```bash
./gobuster dir -u https://google.com -w ~/diccionario.txt -t 200
./gobuster dir -u https://google.com -w ~/diccionario.txt -t 200 --add-slash
./gobuster dir -u https://google.com -w ~/diccionario.txt -t 200 -add-slash -b 403,404
./gobuster dir -u https://google.com -w ~/diccionario.txt -t 50 -b 403,404 -x html,php,txt
./gobuster dir -u https://google.com -w ~/diccionario.txt -t 200 -x html,php -s 200 -b ''
```

### Wfuzz
------
Con wfuzz podemos fuzear lo que sea, no se aplica únicamente en rutas y subdominios, en este caso solo voy a mostrar como se hace para enumerar rutas y subdominios.

Enumerar rutas
```bash
wfuzz -c -t 20 -w /home/valen/diccionario.txt https://google.com/FUZZ
wfuzz -c -t 20 -w ~/diccionario.txt https://google.com/FUZZ/
wfuzz -c -t 20 -w ~/diccionario.txt https://google.com/FUZZ.html
wfuz -c -t 20 -w ~/diccionario.txt -z list,html-txt-php https://google.com/FUZZ.FUZ2Z
wfuzz -c --sl=216 -t 20 -w ~/diccionario.txt https://google.com/FUZZ
wfuzz -c --hl=216 -t 20 -w ~/diccionario.txt https://google.com/FUZZ
wfuzz -c --sw=20 -t 20 -w ~/diccionario.txt https://google.com/FUZZ
wfuzz -c --sh=20 -t 20 -w ~/diccionario.txt https://google.com/FUZZ
```

### Rangos
Enumerar productos existentes desde un rango
```bash
wfuzz -c -t 200 -z range,1-2000 'https://miwifi.com/shop/detail?product_id=FUZZ'
```

### Ffuff
----
[Ffuff](https://github.com/ffuf/ffuf) una herramienta parecida a wfuzz pero escrita en go. Go trabaja muy bien con sockets y conexiones y esto agiliza mucho más el escaneo.

Instalación
```bash
git clone https://github.com/ffuf/ffuf.git
cd ffuf
go build 
```

Uso, los parámetro son muy parecidos wfuzz
```bash
./ffuf -c -t 200 -w ~/diccionario.txt -u https://google.com/FUZZ -v | #La -v de verbose
```
Filtrar por códigos de estado, --mc=200, (match code)
```bash
./ffuf -c -t 200 -w ~/diccionario.txt -u https://google.com/FUZZ/ --mc=200
```

> El término **"FUZZ"** se utiliza para representar la posición en la url donde se insertarán los valores del diccionario.

Enumerar subdominios
```bash
wfuzz -c --hc=403,404 -t 20 -w ~/diccionario.txt -H "Host: FUZZ.google.com" https://google.com
wfuzz -c --sc=200 -t 20 -w ~/diccionario.txt -H "Host: FUZZ.google.com" https://google.com
```

- -c: (**Colors**) representa los datos con colorines
- -t: (**Threads**) igual que con gobuster es para indicar el número hilos
- --hc: (**Hide Code**) sirve para ocultar en el output las líneas con un código de estado específico, en esto caso el 403 que corresponde al Forbidden.
- --sc:(**Show Code**) este es lo contrario a --hc sirve para mostrar únicamente las líneas que contenga el código de estado especificado, en este caso el 200 que corresponde a exitoso.
- --sl: (**Show Line**) mostrar únicamente aquellas respuestas que contenga un número determinado de líneas.
- --hl:(**Hide Line**) ocultar todas las respuestas que contengan un número determinado de líneas
- --sw:(**Show Word**)
- --sh:(**Show Character**)
- -w: igual que con gobuster para indicar la **ruta del diccionario** 
- -H "Host: FUZZ.google.com": Define una **cabecera personalizada para el escaneo.** En este caso, se establece la cabecera `Host` con el valor "FUZZ.google.com". El término **"FUZZ"** se utiliza para representar la posición donde se insertarán los valores del diccionario.

----
### Relacionados
- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se explica en  la carpeta 10 de SEC3.
- [[Fuzzing indirecto]]
- [[Formas de recolectar correos electrónicos]]