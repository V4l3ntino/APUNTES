----
- Tags: #Linux #Escaneo #puertos #masscan
-----
Masscan es una alternaitva a nmap que nos permite realizar una escaneo mucho más rápido. Esta herramienta es muy útil en redes empresariales donde se necesita realizar un escaneo masivo de puertos a los host activos dentro de una red.

Su uso es muy sencillo y parecido a nmap, algunos comandos de nmap son compatibles en masscan, pero hay que seguir la siguiente estructura:
- masscan \[puertos] \[ip] \[ratio --> número de paquetes a transmitir por segundo] 
```bash
masscan -p20,21,22,80,445,443,8080 -Pn 192.168.0.0/24 --rate=10000
masscan -p- -Pn 192.168.0.0/24 --rate=5000
masscan -p- -n -Pn 192.168.0.0/24 --rate=1000
masscan --top-ports -n -Pn 192.168.0.0/24 --rate=1000 -oG captura.cap
```

----
### Relacionados
- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto aparece en SEC3 en la carpeta 6
- [[NMAP]]
