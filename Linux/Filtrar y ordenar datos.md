----
- Tags: #Linux #Comandos #Filtrar-datos #Ordenar-datos  #tail #head #grep #tr #awk #cut #sort #string #rev #sed 
----

### Filtrar por grep
```bash
ifconfig | grep 192 #Muestra en el output las líneas que contengan 192
ifconfig | grep -E "192|wlan0" #Muestra en el output las líneas que contengan 192 y wlan0
ifconfig | grep -v 192 #Quita en el output lo que ponga 192, esto quitará toda la línea donde se encuentre el dato 192.
ifconfig | grep -vE "192|wlan0" #Quita en el output lo que ponga 192 y wlan0, esto quitará toda la línea donde se encuentre los datos wlan0 y 192.
```

### Ver el peso de un archivo 
```bash
du -h archivo.txt
```

### Ver cuantas líneas tiene un archivo
```bash
wc -l archivo.txt
```

### Comparar las líneas  de dos archivos distintos y ver las diferencias
```bash
diff archivo1.txt archivo2.txt #Muestra en rojo lo que se ha quitado y en verde lo que se ha metido en el archivo, El orden que pongas los archivos influye. Si quieres ver las diferencias entre un archivo respecto al otro tienes que poner primero el nombre del otro archivo y luego el nombre del archivo que quieres comparar, te mostrará en rojo lo que se ha quitado de ese archivo y en verde lo que se ha metido en ese archivo que quires comparar respecto al otro. En este ejemplo estamos viendo los cambios que hay del archivo2.txt respecto al archivo1.txt, te mostrará en verde lo que tiene metido como nuevo y en rojo lo que no tiene metido respecto al archivo1.txt
```

### Filtrar por líneas
```bash
tail -n 1 # Filtrar por la última línea de texto
tail -1 #Se puede omitir la -n y no pasa nada, hace lo mismo
head -n 1 # Filtar por la primera línea de texto
head -1 # Se puede omitir -n
awk 'NR==2' # Filtrar por la segúnda línea de texto
```

### Filtrar por argumentos(palabras)

```bash
awk '{print $1}' # Muestra solo la primera palabra del texto en la línea en la que te encuentres
awk 'NF{print $NF}' # Muestra el último argumento de la línea de texto en la que te encuentres
rev # Con rev puedes reversear la cadena de texto (darle la vuelta) y elegir así por la cadena que quieras, para luevo también volver a darle la vuelta
```


### Filtrar argumentos tomando algún delimitador
```bash
192.168.0.2/24
awk '{print $1}' FS="/" # Aquí sería que coges el primer argumento tomando como delimitador la barra, es decir que la barra sería como un separador(un espacio en blanco), de esta manera separas un argumento en dos y puedes seleccionar la parte que a tí te interesa.
192.168.0.2
cut -d '/' -f 1 # Pasa lo mismo, delimitas por la barra con el parámetro -d y luego coges el primer campo con el parámetro -f
```

### Filtrar argumentos haciendo conversiones
```bash
192.168.0.2/24
tr '/' ' ' # Con esto estamos convirtiendo la barra a un espacio para separar la ip del CIDR, luego podemos usar awk para poder coger el argumento que nos interesa que sería el primero, donde está la ip
192.168.0.2 24

tr '/' ' ' | awk '{print $1}'
192.168.0.2

tr -d ' ' # También podemos especificar que nos quite (delete), con el parámetro -d, los espacios de la cadena, también podemos especificarle letras, números, etc. 

sed 's/192/193/' # Con esto estamos sustituyendo el 192 del argumento por 193, con la s indicamos que queremos hacer una sustitución,

echo -e "hola prueba hola" | sed 's/hola/adios/g' # Con la g del final estamos indicando que sustituya la palabra hola en toda la línea, si lo ponemos sin la g solo sustituirá el primer match que encuentre.
```

### Filtrar datos en un archivo no legible
```bash
strings data.txt # Con string nos va listar solo la cadena de caractéres imprimibles, como puede ser letras, números, hastags, giones, barras...
strings data.txt | grep '=' # Ahora solo nos va a listar las cadenas de texto que puedan contener un igual.
```

### Ordenar un conjunto de datos almacendaos en un archivo
```bash
sort data.txt # Ordena por ordena alfabético los datos, mostrando el output mucho más claro.
sort data.txt | uniq -u # Muestra la única cadena de texto que no se repita en el archivo.
```


