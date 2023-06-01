- Tags: #Linux #Capabilitis 

Capabilities = Capacidades 

>Las capabilities sirven para asignar **capacidades específicas** a un programa, en vez de otorgar todos los permisos. Por ejemplo Normalmente, cuando ejecutas un programa en Linux, heredas los permisos del usuario con el que iniciaste sesión. Esto significa que si ese usuario tiene privilegios administrativos (como root), el programa también tendrá todos esos privilegios. Sin embargo, esto puede ser arriesgado ya que un programa malicioso o con errores puede abusar de esos privilegios y causar daños en el sistema.

Con capabilities podemos asignar solo capacidades específicas a un programa, por ejemplo: utilizar funciones de red, realizar cambios en la configuración del sistema, entre otras cosas.

Yo voy a mostrar un ejemplo donde asignamos una capabiliti setuid que permite controlar o modificar nuestro identificador de usuario.
```bash
sudo setcap cap_setuid+ep /usr/bin/python
```

La notación "+ep" que se utiliza en el comando indica los permisos que se están configurando para la capacidad específica.

-   El símbolo "+" indica que se están agregando los permisos, en este caso, se está agregando la capacidad "cap_setuid".
-   El modificador "e"  significa que la capacidad se aplicará cuando el programa se ejecute.
-   El modificador "p" indica que los permisos se mantendrán incluso si el programa se copia o se mueve a otro lugar en el sistema.

Para quitar la capacidad usamos el siguiente comando:
```bash
sudo setcap -r /usr/bin/python
```
Con el parámetro -r lo que hacemos es **Revertir** los cambior aplicados anterior mente.

Bueno pero como hacemos para poder listar estas capacidades, pues con el comando getcap y de la siguiente manera:
```bash
sudo getcap -r / 2>/dev/null
```

Con el parámetro -r estamos indicando que realize un búsqueda **recursiva** desde el directorio raíz.

----
Enlace a las [[Tareas 📋]], este tema se muestra desde la carpeta 15
