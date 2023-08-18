----
- Tags: #Linux #Crontab #change-wallpaper 
------
Para cambiar el fondo de pantalla se necesita utilizar el comando feh, en ArchLinux, en Gnome es otro comando. Pero para que funcione hay que especificar la pantalla en la que se quiere aplicar el comando feh, almenos hay que especificarlo cuando ponemos una tarea en cron. Ya que cuando se aplica una tarea cron y se ejecuta un script que sirve para cambiar la pantalla este necesita saber sobre que monitor hay que aplicar el comando feh. 
Para saber cuál es tu monitor puede poner los siguiente comandos:
```bash
echo $DISPLAY
env | grep -i "display"
```

Display es una variable del sistema donde contiene el número que hace referencia al monitor que estás utilizando. Generalmente suele ser `:0`

Dentro de la ruta /etc/cron.d creamos un archivo y ponemos lo siguiente:
```bash
@reboot valen DISPLAY=:0 bash /home/valen/script.sh
* * * * * valen DISPLAY=:0 bash /home/valen/scripts/changeWallpR.sh
```

### scritp 
```bash
#!/bin/bash
#Change Random Wallpaper Desktop
min=1
max=6
random_number=$(shuf -i "$min-$max" -n 1)
if [[ $random_number = 1 ]];then
    feh --bg-fill /home/valen/Imágenes/wallp1.jpg
fi
if [[ $random_number = 2 ]];then
    feh --bg-fill /home/valen/Imágenes/wallp2.jpg
fi
if [[ $random_number = 3 ]];then
    feh --bg-fill /home/valen/Imágenes/wallp3.jpg
fi
if [[ $random_number = 4 ]];then
    feh --bg-fill /home/valen/Imágenes/wallpkakashi.jpg
fi
if [[ $random_number = 5 ]];then
    feh --bg-fill /home/valen/Imágenes/wallpsimpson.jpg
fi
if [[ $random_number = 6 ]];then
    feh --bg-fill /home/valen/Imágenes/wallpsportcar.jpg
fi
```

### REFERENCIAS
---
- https://superuser.com/questions/1033903/why-doesnt-cronjob-execute-feh-command
- [[Filtrar y ordenar datos]]