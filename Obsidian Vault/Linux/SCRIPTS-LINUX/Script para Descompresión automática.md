----
- Tags: #Linux #Comprimir-Descomprimir #Script 
-----

Este script sirve para descomprimir archivos que estén comprimidos en otros archivos, es decir si hay un archivo que está comprimido en otro archivo y ese mismo archivo esta comprimido en otro archivo y así sucesivamente.

```bash
#!/bin/bash

function ctrl_c (){
        echo -e "\n [+] Saliendo \n"
        exit 1
}

#CTRL+C
trap ctrl_c INT

#COLORES
greenColour="\e[0;32m\033[1m"
endColour="\033[0m\e[0m"
redColour="\e[0;31m\033[1m"
blueColour="\e[0;34m\033[1m"
yellowColour="\e[0;33m\033[1m"
purpleColour="\e[0;35m\033[1m"
turquoiseColour="\e[0;36m\033[1m"
grayColour="\e[0;37m\033[1m"

7z x data.gz

NextName="$(7z l data.gz | tail -3 | head -1 | awk 'NF{print $NF}')"

###########################################################################################

echo -e " El nombre extraido:  ${yellowColour}${NextName}${endColour}"
sleep 1

while [ ${NextName} ]; do
7z x ${NextName} 2>/dev/null
NextName="$(7z l ${NextName} 2>/dev/null | tail -3 | head -1 | awk 'NF{print $NF}')"
echo -e "El nombre extraido: ${yellowColour}${NextName}${endColour}"
sleep 1
done
```

-----
Enlace a las [[Tareas 📋]], este tema se muestra en la carpeta 36
- [[Comprimir y Descomprimir archivos con 7z]]
