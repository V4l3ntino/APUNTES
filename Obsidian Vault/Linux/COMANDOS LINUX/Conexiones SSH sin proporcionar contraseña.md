	-----
- Tags: #Linux #ssh #Conectarse-sin-contraseña
-----

## 1º Método

Con **ssh-keygen** creamos una clave pública y otra privada, simplemente tenemos que copiar el archivo **id_rsa.pub** con el nuevo nombre **authorized_keys**, y luego pasarlo a la máquina huésped (SERVIDOR) en el directorio ~/.ssh De manera que cuando nos vallamos a conectar a ese servidor teniendo esa clave autorizada en nuestra ruta también podremos conectarnos a la máquina sin proporcionar contraseña.
```bash
cd .ssh
ssh-keygen
#Damos enter repetidas veces hasta generar las claves
cp id_rsa.pub authorized_keys
#Ahora debemos copiar ese mismo archivo en el servidor en la misma ruta
scp authorized_keys valen@192.168.0.101:~/.ssh/
#Y ya solo quedaría conectarse como siempre pero esta vez sin proporcionar la contraseña
ssh valen@192.168.0.101
```

## 2º Método

Através de la clave privada, podemos utilizar la id_rsa privada para conectarnos al servidor, pero para esto debemos tenerla primero. Generamos una clave con **ssh-keygen** y con el comando **ssh-copy-id -i** y el nombre **id_rsa** ponemos el servidor valen@192.168.0.101, lo que hará esto es generar una authorized_keys (clave pública) através de la clave privada en el servidor dentro de la ruta .ssh, nos pedirá la contraseña del servidor y ya la próxima vez que queramos conectarnos pues no nos pedirá la contraseña.
```bash
ssh-keygen
ssh-copy-id -i id_rsa valen@192.168.0.101
#Ponemos la contraseña del servidor y ya la próxima vez que nos conectemos lo haremos sin la contraseña.
ssh valen@192.168.0.101
```

Lo mismo podemos hacerlo viceversa, seguimos los mismo pasos en la otra máquina y podremos conectarnos desde una máquina sin proporcionar contraseña, da igual desde que máquina te conectes, ambas se podrán conectar sin proporcionar contraseña.

Estos dós métodos representan lo mismo, conectarse desde una máquina a otra a través de la clave pública, una lo hacemos a mano cambiándo el nombre a la clave pública y metiéndola en el servidor y la otra lo hacemos automáticamente a través de la clave privada, porque a través de la clave privada se obtiene la clave pública y esta se envía directamente al servidor que nos queramos conectar.

## 3º Método

En el caso que solo tengamos la id_rsa del servidor (su clave privada) al que nos queramos conectar pués simplemente con el siguiente comando podemos conectarnos sin proporcionar contraseña:
```bash
ssh -i id_rsa valen@192.168.0.101
```

Esto lo que hace es utilizar la clave privada que tenemos del servidor y usarla como método de autenticación, de manera que el servidor verá que la clave privada coincide con la suya y nos permitirá conectarnos.

### Recuerda
----
> La claves asimétricas funcionan con dos claves, una pública y la otra privada. La clave pública es el resultado de multiplicar dos números primos muy grandes, através de la clave pública no se puede deducir la clave privada porque averiguar cuáles son los dos número primos que se están multiplicando es muy complejo y requiere de alto rendimiento para averiguarlo.
---

### Relacionados

-  Enlace a las [[Tareas 📋]], este tema se muestra en la carpeta 37