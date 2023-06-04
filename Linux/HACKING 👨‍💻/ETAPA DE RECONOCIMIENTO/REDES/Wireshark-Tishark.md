-------
- Tags: #Wireshark #Linux 
-----

Con wireshark podemos analizar el tráfico de la red, ver los paquetes que se están tramitando y monitorear el tráfico de la red.

Abrir una captura con wireshark 
```bash
wireshark Captura.cap &>/dev/null disown
```

Filtrar paquetes fragmentados
```bash
ip.flags.mf == 1
ip.flags.mf == 0 # Al contrario que antes ahora filtrarías por paquetes enteros.
```

Filtrar por un puerto
```bash
tpc.port == 22 # Filtramos por el puerto 22 en el protocolo TCP
udp.port == 22 # Filtramos por el puerto 22 en el protocolo UDP
```


### Tshark
Con tshakr podemos visualizar el contenido de una captura pero en consola.
```bash
tshark -r Captura.cap 2>/dev/null 
```

Podemos indicarle que tipo de paquetes queremos filtrar el contenido de la siguiente manera
```bash
tshark -r Captura.cap -Y "http" 2>/dev/null 
```

Puedes representar la data en formato json 
```bash
tshark -r Captura.cap -Y "http" -Tjson 2>/dev/null
```

Filtrar la data de un campo concreto, por ejemplo los campos que están en exadecimal
```bash
tshark -r Caputar.cap -Y "http" -Tfields -e tcp.payload 2>/dev/null
```

