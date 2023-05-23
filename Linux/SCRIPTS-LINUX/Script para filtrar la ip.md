-----
- Tags: #Linux #Filtrar-ip #Comandos #Script 
-------

### Crear scripts
Bueno ahora que sabemos filtrar los datos vamos con el script, voy a filrar por la ip utilizando la mayoría de parámetros que he mostrado en los apuntes. Para mostrar el contenido resultado de una serie de comandos se debe meter entre paréntesis y con el dolar al principio, este indica que quieres ver el contenido interpretado entre paréntesis

```bash
#!/bin/bash

echo -e "\n [+] La dirección IP privada es: \n $(ip a | grep "wlan0" | tail -n 1 | tr 'inet' ' ' | awk '{print $1}' FS="/")\n""
```

Otra forma más sencilla sería
```bash
#!/bin/bash

echo -e "\n [+] La dirección IP privada es: $(ifconfig | grep 192 | awk '{print $2}')\n"
```

### Meter colores al script

Para ello tenemos que tener una serie de variables declaradas, los colores puedes buscarlos en internet para representarlos en bash. Con esto podemos representar el output mucho más bonito con colorines
```bash
#!/bin/bash
#Paleta de colores
greenColour="\e[0;32m\033[1m"

endColour="\033[0m\e[0m"

redColour="\e[0;31m\033[1m"

blueColour="\e[0;34m\033[1m"

yellowColour="\e[0;33m\033[1m"

purpleColour="\e[0;35m\033[1m"

turquoiseColour="\e[0;36m\033[1m"

grayColour="\e[0;37m\033[1m"

echo -e "\n ${yellowColour}[+]${endColour} ${blueColour}La dirección IP privada es:${endColour} ${greenColour} $(ifconfig | grep 192 | awk '{print $2}')${endColour}\n" 

```

