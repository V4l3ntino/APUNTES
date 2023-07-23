----
- Tags: #Linux #Comandos #Script  #macchanger #cambiar-mac 
----
Una vez sabemos como funciona [[Macchanger]] podemos hacer el siguiente script
```bash
#!/bin/bash

#COLORS
greenColour="\e[0;32m\033[1m"
endColour="\033[0m\e[0m"

sudo ifconfig wlan0 down
sudo macchanger -a wlan0 &>/dev/null
sudo ifconfig wlan0 up

echo -e "\nLa nueva mac de la ${greenColour}wlan0${endColour} es:${greenColour} $(ifconfig wlan0 | grep 'ether' | awk '{print $2}')\n"
```

Con esto puedo cambiar la mac de mi pc en cuestión de micro segundos y mostrar la nueva mac por consola filtrando los datos. Si no te suena algún parámetro de la última línea puedes chequear la siguiente página. [[Filtrar y ordenar datos]]

----
### Relacionados
- [[NMAP]]
- [[Macchanger]]