----
- Tags: #Linux #Trastadas #Redireccionamiento-de-flujo #Cambiar-fondo-pantalla
----

Con **exec**[^1]  podemos también crear trastadas como esta
```bash
exec a<>a
exec 1 <> 1          
```
Esto lo que hará es que se cierre inmediatamente la terminal porque exec no es capaz de interpretarlo.
Si editamos el archivo .bashr o el archivo .zshrc y metemos este comando lo que pasará es que cada vez que se abra la terminal esta se cerrará automáticamente.

También podemos crear un script.sh que cambie constantemente el fondo de pantalla y poner en la bashrc que se ejecute siempre al  abrirse una terminal
```bash
source /home/usuario/script.sh
# También se puede poner
bash /home/usuario/script.sh
```

Script para cambiar el fondo de pantalla:
```bash
#! /bin/bash
for i in {1..10}
do
	gsettings set org.gnome.desktop.background picture-uri 'file:///ruta/al/fondo/de/imagen1.jpg'
	sleep 0.8
	gsettings set org.gnome.desktop.background picture-uri 'file:///ruta/al/fondo/de/imagen2.jpg'
done
```
> Esto hará que cambia el fondo de pantalla primero por la imágen 1 y después por la imágen 2, metiéndole entre medias un pequeño sleep para que se aprecie los cambios por pantalla.

---

### Referencias
[^1]: [[Redireccionamiento de Flujo]] explico mejor en que consiste el comando exec y como redirigir el flujo


