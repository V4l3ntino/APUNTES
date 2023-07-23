------
- Tags: #Linux #Comandos #Crontab #Tareas-programadas #watch
------
```bash
/etc/cron.d
```

La ruta "/etc/cron.d" en sistemas Unix/Linux se utiliza para almacenar archivos de configuración que definen tareas cron específicas del sistema, permitiendo la automatización de tareas recurrentes en momentos determinados.

Antes de nada hay que verificar que el servicio de cron está activo, en Archlinux/Archcraft el servicio se llama:
```bash
sudo systemctl status cronie.service
```
En caso de que no esté activo pués en vez de **status** ponemos **start**
El nombre del servicio en ubuntus seria
```bash
sudo systemctl status crond
```

### Parámetros de crontab
------
- Página web para repasar crontab: [site24x7](https://www.site24x7.com/es/tools/crontab/cron-generator.html)

```bash 
*****
```

Cada asterisco representa una posición, y cada posición representa:
1. El primero -> Minutos
2. El segundo -> Horas
3. El tercero ->  Días
4. El cuarto -> Mes
5. El quinto -> De Lunes a Domingo (Días de la semana), Se puede representar de las siguientes tres maneras
	1. Lunes -> **1 -> MON -> MONDAY**
	2. Martes -> **2 -> TUE -> TUESDAY**
	3. Miércoles -> **3 -> WED -> WEDNESDAY**
	4. Jueves -> **4 -> THU -> THURSDAY**
	5. Viernes -> **5 -> FRI -> FRIDAY**
	6. Sábado -> **6 -> SAT -> SATURDAY**
	7. Domingo -> **0 -> SUN -> SUNDAY**

- \*/: Una barra al lado del punto significa que quieres que se haga la tarea cada x tiempo, ejemplo: `*/5` Si esto lo representamos en la primera posición estaríamos diciendo que cada cinco minutos de cada hora se ejecute la tarea.
- L: Esto equivale a (last) es decir el último de algo, en este caso solo se podría aplicar en la posición de Los días de la semana (5º Posición) y en los días del mes (3º Posición)

Si combinas la 3º posición y la 5º pasa lo siguiente:
```bash
* * 3 * MON
```

> Esto indica que la tarea se ejecutará cada minuto de cada hora del tercer día de cada mes y así como los Lunes, es decir que se ejecutará la tarea los días 3 de cada més y además los días que sean Lunes.

Si queremos añadirle más días de la semana sería:
```bash
* * 3 * MON,THU,SAT
```

> Si queremos añadir más campos haciendo referencia a una posición simplemente lo ponemos entre comas.

### Locura máxima
```bash
* 2,4,5-7/2 3,5 * MON,THU,SAT
```
Cada minuto, a las 02:00 AM, a las 04:00 AM, y cada 2 horas, entre las 05:00 AM y las 07:59 AM, los días 3 y 5 del mes, y los lunes, jueves y sábados. Este resultado lo he obtenido de la página [site24x7](https://www.site24x7.com/es/tools/crontab/cron-generator.html)

### Prácticas con crontab
----
Quiero hacer un script que se ejecute cada cinco minutos y almacene el output de un comando a un archivo llamado log

*script.sh*
```bash
#!/bin/bash
ifconfig > ~/log.txt
```

*Crontab*
En la ruta /etc/cron.d metemos un archivo txt que tenga mínimo el privilegio de lectura con el siguiente contenido:
```bash
@reboot valen ~/script.sh &>/dev/null
5 * * * * valen ~/script.sh &>/dev/null
```
@reboot -> es un parámetro adicional que se usa si quieres que la tarea se ejecute cuando el sistema operativo se inicie.
valen -> especifico que la tarea deberá ejecutarse como el usuario valen
~/script.sh -> es la ruta donde se escuentra el script que es lo mismo que poner /home/valen/script.sh
&/dev/null -> redirigo el sterr y el stout al dev null para que no muestre nada acional por pantalla.

### El comando watch 
> Si queremos hacer un **ls**, y que este dure **durante un cierto tiempo**,  mostrando contenido actualizado todo el rato ponemos lo siguiente, también se puede aplicar a cualquier otro comando, por ejemplo whoami, ifconfig, etc.
```bash
watch -n 1 ls
watch -n 1 cat log.txt
```


### Referencias
----
- [[Redireccionamiento de Flujo]]
- [[Creación de usuarios,grupos, y gestión de permisos]]
- El enlace a las [[Tareas 📋]], este tema se encuentra desde la carpeta 45 - 48.
