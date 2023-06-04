----
- Tags: #Linux #Comandos #macchanger #cambiar-mac 
----
Con macchanger podemos cambiar la dirección mac de nuestra interfaz, pero para eso tenemos que previamente deshabilitar la tarjeta de red.
```bash
sudo ifconfig wlan0 down
```

Luego podemos usar macchanger de la siguiente forma
```bash
sudo macchanger -a wlan0 #Indicamos que quermos cambiar la mac por una cualquiera totalmente random
sudo macchanger -m X:X:X:X:X:X #Indicamos que quermos cambiar la mac por una específica la que nosotros le pongamos
```

> Hay que tener en cuenta que las direcciones mac se divide en 2 partes, la primera parte  son los primeros 3 bytes que hacen referencia al OUI (Organizationally Unique Identifier). Esto son los número que le pone cada fabricante ha su producto, es decir por ejemplo:
```
00:02:78 --> Samsung MagicLan
```
Esta OUI hace referencia a que el fabricante del producto es Samsung

Y los 3 últimos bytes ya si hacen referencia a la mac de cada usuario, estos tiene un número aleatorio para que cada dispositivo tenga su mac propia, de manera que continuando con el ejemplo anterior una mac aceptable sería:
```bash
00:02:78:02:3a:bc
```

> Ten en cuenta que las direcciones mac se representan en hexadecimal.

----
### Relacionados
- [[NMAP]]
- [[Script para cambiar la mac]]