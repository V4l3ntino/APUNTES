-----
- Tags: #Linux #Comandos #7z #Comprimir-Descomprimir 
------
### Comprimir una carpeta
```bash
7z a Comprimido.7z /home/valen/carpeta-a-comprimir
```
Donde a es para indicarle que quieres comprimir una carpeta, primero le pones el nombre de la carpeta con la extensión .7z y luego la ruta de la carpeta que deseas comprimir.

### Descomprimir una carpeta
```bash
7z l carpeta-comprimida.gz #Con el parámetro l indicamos que queremos listar el contenido del comprimido

7z x carpeta-comprimida.gz #Con el parámetro x indicamos que queremos extraer el contenido de la cartepa comprimida (Descomprimir)
```

> Lo bueno que tiene **7z** es que nos permite descomprimir cualquier archivo, da igual cuál sea su extensión que podremos extraer el contenido de la carpeta con el parámetro x. Esto nos **ofrece una facilidad increible** a la hora de descomprimir archivos.

-----
### Relacionados

- [[Script para Descompresión automática]]
- Enlace a las [[Tareas 📋]], este tema se muestra en la carpeta 36
- [[Archivos Hexadecimales]]


