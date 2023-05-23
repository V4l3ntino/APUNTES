----
- Tags: #Linux #Comandos  
----

> En linux está el comando "exec" que nos permite redireccionar el flujo de la información donde nosotros queramos, es decir, podemos hacer que la información se rediriga hacia donde nosotros queramos.
   Para ello tenemos que manejar el stderr(ERRORES)  y el stdout(OUTPUT), el stderr se representa con el 2 y el stdout se representa con el 1.
   Si queremos que el output no se muestre por pantalla sino que se rediriga todo a un archivo pues ponemos lo siguiente

```bash
exec 1<>archivo.txt
```

Si lo que queremos es redirigir el stderr a un archivo lo que ocurrirá es que el prompt de la terminal no se mostrará por pantalla al igual que tampoco se verá ningún comando por pantalla cuando estés escribiendo, únicamente se mostrará el resultado del comando cuando le demos al enter.
```bash
exec 2<>archivo.txt
```

Y si queremos que tanto el stderr como el stdout se rediriga a un archivo para que no se muestre nada por pantalla pues hacemos lo siguiente
```bash
exec 1<>archivo.txt
exec 2<>&1
```

También podemos utilizar el exec para redirigir simplemente el output de un comando por ejemplo
```bash
exec 8<>archivo.txt
whoami >&8 
#De manera que el output del comando se mostrará en el archivo.txt porque apunta al id 8 que este a su     vez apunta al archivo.txt

exec 8>&- #Esto desvincula el id 8 con el archivo
```

También podemos redirigir el output de un comando a un archivo directamente especificando un nombre
```bash
ifconfig > resultado.txt
```

-----
Enlace a las [[Tareas 📋]], este tema se aborda desde la carpeta 3 - 4