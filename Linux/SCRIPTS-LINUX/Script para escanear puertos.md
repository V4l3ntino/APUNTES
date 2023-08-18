-----
- Tags: #Linux #Script #escaner-puertos #scan-ports
----
```bash 
#!/bin/bash
#SALIDA DEL PROGRAMA
function ctrl_c (){
        echo -e "\n [+] Salida \n"
        exit 1
}

trap ctrl_c INT

#COLORES
greenColour="\e[0;32m\033[1m"
endColour="\033[0m\e[0m"

for port in {1..1000};
do
(timeout 1 echo "" > /dev/tcp/localhost/$port)2>/dev/null && echo -e " ${greenColour}[+] OPEND PORT $port${endColour}" || echo " [-] CLOSED PORT $port" &
done; wait
```

1.  La función `ctrl_c` se define para capturar la señal de interrupción (Ctrl+C) y ejecutar una acción. En este caso, muestra un mensaje de salida y termina el programa.
    
2.  La línea `trap ctrl_c INT` configura el trap para capturar la señal SIGINT (Ctrl+C) y ejecutar la función `ctrl_c`.
    
3.  Se definen dos variables de color para imprimir mensajes en verde y restablecer el color a su valor predeterminado.
    
4.  El bucle `for` recorre los números del 1 al 65536, asignando cada número a la variable `port`.
    
5.  Dentro del bucle, se ejecuta el comando `(timeout 1 echo "" > /dev/tcp/localhost/$port) 2>/dev/null`. Este comando intenta establecer una conexión TCP a `localhost` en el puerto especificado. Si la conexión tiene éxito (es decir, el puerto está abierto), se enviará una cadena vacía y se redireccionará a `/dev/null` para descartar cualquier salida. Si la conexión falla (es decir, el puerto está cerrado), se descartará cualquier salida de error.

6. El comando `timeout` establece un límite de tiempo para la ejecución de un comando. En el contexto del script, el comando `timeout 1` se utiliza para limitar el tiempo de espera de la conexión TCP a 1 segundo. 
    
7.  A continuación, se utiliza una estructura condicional (`&&`) para imprimir un mensaje indicando que el puerto está abierto si la conexión fue exitosa. En caso contrario (`||`), se imprime un mensaje indicando que el puerto está cerrado.
    
8.  El operador `&` al final de la línea permite que el bucle continúe ejecutándose en segundo plano mientras se inicia una nueva iteración. Esto permite que el escaneo de puertos sea más rápido y eficiente.
    
9.  Finalmente, se utiliza el comando `wait` para esperar a que todas las tareas en segundo plano finalicen antes de finalizar el programa.
-----
### Relacionados
- Enlace a las [[Tareas 📋]], el curso se encuentra en la carpeta 40
- [[Script para ver host en tu red]]