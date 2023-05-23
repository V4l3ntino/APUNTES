-----
- Tags: #Linux #script #ver-host #show-host 
-----
```bash
#!/bin/bash
function ctrl_c (){
	echo -e "\n[+] Saliendo \n"
	exit 1
}

#CONTROL C
trap ctrl_c INT

#COLORES
greenColour="\e[0;32m\033[1m"
endColour="\033[0m\e[0m"

for host in {1..254};
do
(ping -c 1 192.168.0.$host)&>/dev/null && echo -e " ${greenColour}[+] 192.168.0.$host HOST UP $port${endColour}" || echo " [-] $host HOST DOWN $port" &
done; wait
```

1.  La línea `for host in {1..254};` establece una variable `host` que tomará valores desde 1 hasta 254. Esto crea un bucle que se ejecutará para cada valor de host en ese rango.
    
2.  La siguiente línea `(ping -c 1 192.168.0.$host)&>/dev/null` realiza un comando de ping al host correspondiente dentro de la red local (192.168.0.x, donde `x` es el valor de `host` en cada iteración). El flag `-c 1` especifica enviar solo un paquete de ping, y `192.168.0.$host` forma la dirección IP de destino para el ping. El redireccionamiento `&>/dev/null` desvía tanto la salida estándar como la salida de error del comando ping al archivo `/dev/null`, lo que significa que no se mostrará ninguna salida en la consola.
    
3.  El siguiente fragmento `&& echo -e " ${greenColour}[+] 192.168.0.$host HOST UP $port${endColour}"` se ejecuta solo si el comando de ping anterior es exitoso. En este caso, muestra un mensaje indicando que el host está activo (UP). El texto se muestra en color verde debido al uso de las variables `greenColour` y `endColour`.
    
4.  Si el comando de ping no tiene éxito (el host está inactivo), se ejecuta el fragmento `|| echo " [-] $host HOST DOWN $port"`, que muestra un mensaje indicando que el host está inactivo (DOWN).
    
5.  Al final de cada iteración del bucle, el símbolo `&` colocado antes de `done` hace que el proceso se ejecute en segundo plano, lo que permite que el bucle continúe sin esperar a que el comando ping termine.
    
6.  El comando `wait` se utiliza al final del bucle para esperar a que todos los procesos en segundo plano se completen antes de finalizar la ejecución del script.
-----
### Relacionados

- Enlace a las [[Tareas 📋]], este curso se muestra en la carpeta 40
- [[Script para escanear puertos]]