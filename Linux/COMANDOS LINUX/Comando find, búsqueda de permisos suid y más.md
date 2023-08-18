- Tags: #comandos #Linux #Permisos #find

Para realizar una búsqueda de **permisos suid**  
```bash
sudo find / -type f -perm -4000 2>/dev/null
```

/ -->  Indica que quieres realizar la búsqueda desde la raíz del sistema
-type -->  para especificar que estamos buscando, f(folder, [archivo]), d(directory,[directorio])
-perm -->  para especificar el permiso que estamos buscando, 4000 permisos suid en octal

------
### Xargs
Con este comando podemos concatenar el output de un comando con otro, ejemplo:
```bash 
which passwd | xargs ls -l 
```

> En este caso cuando se ejecute el primer comando dará como resultado una ruta absoluta, por tanto el siguiente comando hará un ls -l a la ruta absoulta.

Realizar una búsqueda según el **nombre del archivo o carpeta**, listando también sus permisos. Se puede hacer también con xargs pero el propio find ya tiene un parámetro implementado para la búsqueda de permisos. Con xargs podríamos también listar paralelamente el contenido que hay dentro de un directorio.
```bash
find / -name passwd -ls 2>/dev/null

find / -name passwd 2>/dev/null | xargs ls -ld
```

Realizar una búsqueda según el **nombre incompleto**, para te interprete el * y no sea parte de la cadena de texto hay que escaparlo, por eso se pone con esta barra \
```bash
find / -name dex\* 2>/dev/null   #Esto quiere decir que el arhivo empieza por dex y termina por algo 
find / -name \*ex\* 2>/dev/null
find / -name dex\*.sh 2>/dev/null #Esto empiza por dex continúa por algo y termina por .sh
```

Realizar un búsqueda de archivos según el **grupo/usuario** al que pertenece
```bash
find / -group valen -type f 2>/dev/null

find / -user root -type f 2>/dev/null
```

Realizar una búsqueda de archivos pero que tengan **capacidad de (escritura,lectura,executables)**
```bash
find / -group root -type f -writable 2>/dev/null
find / -group root -type f -readable 2>/dev/null
find / -group root -type f -executable 2>/dev/null 
```

Realizar una búsqueda de archivos pero **descartando alguna capacidad** (escritura, lectura, executables)
```bash
find / -type f -readable ! -executable 2>/dev/null # Con la ! delante de la capacidad estamos descartando la capacidad de ejecución de los archivos
```

Realizar un búsqueda de archivos **filtrando por su tamaño**, hace falta tener en cuenta los siguientes parámetros básicos
-c --> bytes
-k --> kilobytes
-M --> megabytes
-G --> gigabytes 
si quieres buscar algo más específico pues pone man find y filtras poniendo la barra /
```bash
sudo find / -size 100c 2>/dev/null
```

### Busquedas de archivos por el contenido
Si quieres buscar un archivo según por el contenido que tenga y no por el nombre puedes hacer lo siguiente:
```bash
find / -type f -exec grep -l "#f0719b" {} \; 2>/dev/null
```

Esto hará una búsqueda de aquellos archivo que tengan como contenido el código hexadecimal #f0719b, '{}' esto indica que reemplaze el contenido por los nombres de los archivo encontrados y `\;` marca el final del comando `exec`.

----
Enlace a las [[Tareas 📋]], este tema se muestra en la carpeta 20