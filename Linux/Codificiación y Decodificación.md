--------
- Tags: #Linux #Comandos #base64 #encode #decode 
--------

###  Base64 
```bash
echo "Hola esto es una prueba" | base64     |  #Codificar cadena de texto
SG9sYSBlc3RvIGVzIHVuYSBwcnVlYmEK            |

echo 'SG9sYSBlc3RvIGVzIHVuYSBwcnVlYmEK' | base64 -d    | #Decodificar cadena de texto con el parámetro -d            
Hola esto es una prueba                                | 
```

### Cifrado cesar
Para esto cifrado lo único que debemos tener en cuenta es el número de posiciones que rota en el abecedario, sabiendo el número podemos hacerlo de varias manera, yo voy a mostrar dos:
Número de rotación = 13
1. Podemos visitar la siguiente página web ( [rot13.com](https://rot13.com/)) para que nos aplica el decode o el encode diréctamente
2. Podemos recurrir a la herramienta tr que explico como usarla en [[Filtrar y ordenar datos]], que además de sustituir carácteres nos permite poder realizar rotaciones en el abecedario

```bash 
cat data.txt  | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
```

Lo que estoy haciendo aquí es, primero, especificar el rango del abecedario empezando desde la A hasta la Z que es el primero y último caracter, luego indico el rango a partir de 13 posiciones, que sería desde la N hasta la Z y el resto que sería desde la A hasta la M, esto lo especifico primero en **mayúsculas** y luego lo repito para las **minúsculas**.

>Para codificar el texto, como es ***cifrado simétrico***, el comando anterior también nos valdría para la codificación. Simplemente tendríamos que tener dentro del archivo data.txt el contenido en texto claro y hacerle el tr para que te lo muestre ilegible.





