------
- Tags: #Crear-Usuarios #Crear-Grupos #Permisos #Contraseñas #Linux
----
Para ver los grupos a los que pertenecemos
```bash
cat /etc/group | grep "usuario"
usuario:x:1000: #el grupo al que pertenece el usuario tiene su mismo nombre
```
También podemos ver los grupos con el comando **id**, si queremos ver el tipo de shell que utiliza un usuario ponemos lo siguiente
```bash
cat /etc/passwd | grep "usuario"
```
Si queremos cambiar la contraseña a un usuario lo editamos en el /etc/shadow, si queremos cambiar la contraseña a un usarios
```bash
passwd usuario
```
Si queremos crear un usuario y asignarle una shell y un directorio
```bash
useradd pepe -s /usr/bin/bash -d /home/pepe
userdell pepe #Eliminar al usuario
```
> También podemos asignarle la shell editando el archivo /etc/passwd

Para crear un nuevo grupo, asignar ese nuevo grupo a un usuario
```bash
addgroup gruponuevo #Crear el grupo
usermod -a -G gruponuevo pepe # AMBOS HACEN LO MISMO, Asignar el gruponuevo a pepe
usermod -aG gruponuevo pepe   # AMBOS HACEN LO MISMO, Asignar el gruponuevo a pepe
dellgrup gruponuevo #Eliminar el grupo
```

Meter a un usuario nuevo en el **grupo de sudoers**
```bash
usermod -aG sudo pepe
```

## Variables de entorno
Para ver el tipo de shell que estamos usando
```bash
echo $SHELL
cat /etc/shells #para ver todas las shells que tenemos preinstaladas.
echo $PATH #Variable de entorno que nos puestra las rutas predeterminadas que utiliza el sistema para interpretar los comandos
echo $? #Que nos muestre el código de estado del último comando ejecutado, 1(Error), 127(Fallo), 0(Exitoso)
echo !$ #Con esto estamos representando el último comando ejecutado, otro ejemplo
whoami
!$ #Esto es igual a whoami
```

## Gestión de permisos

Para los permisos se puede trabajar de dos formas: Octales, Letras

### Letras
r(read)
w(write)
x(execute)
### Octales
4 --->  Read
2 --->  Write
1 ---> Execute

```bash
sudo chmod 777 archivo.txt
sudo chmod u=rwx,g=rwx,o=rwx archivo.txt

sudo chmod 400 archivo.txt
sudo chmod u=+r-,g=-,o=- archivo.txt

sudo chown user:root archivo.txt #Comando chown para cambiar el propietario de un archivo, primero se especifica el usuario y luego el grupo al que quieres que pertenezca.
```

## Permisos suid sguid
---
Este tipo de permisos especiales permite ejecutar un programa directamente como si fuera root durante el periodo de tiempo que se está ejecutando, cuando se asigna este tipo de permisos se sustituye la x por la s ya que hace lo mismo que la x pero como superusuario.
```bash
#Suid
sudo chmod 4700 archivo.txt
sudo chmod u=rws,g=-,o=- archivo.txt
#Sguid
sudo chmod 2777 archivo.txt
sudo chmod u=rwx,g=rws,o=rwx archivo.txt

```

## Permisos sticky bit
El permiso sticky bit ayuda a proteger los archivos dentro de un directorio compartido, permitiendo que los usuarios creen, modifiquen y eliminen solo sus propios archivos mientras se evita que modifiquen o eliminen los archivos de otros usuarios. Aunque el archivo no tenga permisos de escritura podríamos borrarlo siendo otro usuario porque si la carpeta que la contiene tiene los privilegios necesarios estos se aplican también a todo su contenido, para eso se utiliza el sticky bit, para que no puedas eliminar ni modifcar el contenido de la carpeta .
```bash
sudo chmod u=rwx,g=rwx,o=rwt archivo.txt
sudo chmod 1777 archivo.txt
```

## Permisos attr
Estos permisos son un paso más de los normales, es decir se utilizan una serie de atributos para modirficar el comportamiento de los archivos:
1.  +i (inmutable): Este atributo establece el archivo o directorio como inmutable, lo que significa que no se puede modificar, eliminar, renombrar o enlazar hasta que se elimine el atributo. Es útil para proteger archivos importantes contra modificaciones accidentales o maliciosas(Nisiquiera root puede eliminar o modificar el contenido).
    
2.  +a (añadir solo): Este atributo permite agregar datos a un archivo existente, pero no permite modificar o eliminar el contenido existente. Es útil en escenarios donde se necesita garantizar la integridad de los datos existentes.
    
3.  +d (no respaldar): Con este atributo, se indica al sistema que no realice copias de respaldo del archivo o directorio durante las operaciones de copia de seguridad. Puede ser útil para excluir archivos o directorios de los procesos de respaldo regulares.
    
4.  +s (secure deletion): Este atributo indica al sistema que al eliminar el archivo, se debe sobrescribir su contenido con ceros para evitar la recuperación de datos. Ayuda a garantizar una eliminación segura de archivos.
    
5.  +u (registro de actualización): Al habilitar este atributo, se crea un registro de actualización cada vez que se modifica el archivo. Puede ser útil para rastrear los cambios y la actividad realizada en un archivo específico.

```bash
sudo chattr +i -V prueba  #el -v indica verbose para ver los cambios aplicados
sudo lsattr -d prueba     #el lsattr es como un ls pero para ver estos atributos y -d que especifica el directorio
```

-----
Enlace a las [[Tareas 📋]], este tema se muestra desde la carpeta 6 - 13


