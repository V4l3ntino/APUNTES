----
- Tags: #Linux #Scan-network #arpscan 
---- 

Con arp-scan podemos hacer un escaneo rápido de todos los host conectados a la red y ver su dirección mac.
```bash
arp-scan -I wlan0 --localnet 
```

- -I : indica la interfaz
- --localnet: indica la red local en la que te encuentras conectado

En ocasiones arp te reporta dispositivos duplicados que te saldrán entre paréntesis (DUPS), para no ver duplicados simplemente añadirmo el parámetro **--ignoredups**
```bash
arp-scan -I wlan0 --localnet --ignoredups
```


> En [[NMAP]] podemos hacer también un scaneo de todos los host de una red con el parámetro -sn también conocido ping sweep, que se encarga de hacer un barrido de ping a todos los host activos de una red, reportándonos tanto las ips como las macs correspondientes.

```bash
nmap -sn 192.168.1.0/24
```

---
### Relacionados
- [[NMAP]]
- [[MASSCAN]]