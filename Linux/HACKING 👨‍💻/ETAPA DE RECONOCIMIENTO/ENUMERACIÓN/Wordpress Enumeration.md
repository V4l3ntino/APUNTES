-------
- Tags: #wordpress #web
------
### Exploitdb
Sirve para mostrar las vulnerabilidades que existen sobre una versión de un programa concreto. También contempla muchos exploits para gestores de contenidos como wordpress. Podemos visitar la propia página web en [exploit-db.com](https://www.exploit-db.com/)  o usar la herramienta searchsploit.
```bash
sudo apt install exploitdb
#Ejemplo
searchsploit wordpress user enumeration
```

Examinar el código del exploit:
```bash
searchsploit -x 49192
```
El código se muestra en la ruta del exploit.

### Whatweb
Es una buena herramienta para saber que gestor de contenido corre por detrás de la web, a veces podemos ver hasta la versión 
```bash
whatweb miwifi.com
```

### Wpscan
Esta herramienta es muy útil para enumerar todo tipo de vulnerabilidades de una página web siempre y cuando lo que corra por detrás sea wordpress. Para que sea útil necesitamos un api token que lo conseguimos cuando nos registramos en su página web. [wpscan.com](https://wpscan.com/register)
```bash
wpscan --url https://miwifi.com -e vp --api-token="..."
```

-e: (enumerate) sirve para enumerar distintos tipos de vulnerabilidades, también se puede poner --enumerate. En este caso estamos enumerando los plugins vulnerables.

**Tipos de parámetros para la enumeración**
 vp-->Vulnerable plugins
 ap--> All plugins
 p-->Popular plugins
 vt-->Vulnerable themes
 at-->All themes
 t-->Popular themes
 tt-->Timthumbs
 
 > TimThumb era un popular script de redimensionamiento de imágenes utilizado en muchos temas y plugins de WordPress. Sin embargo, en el pasado, se descubrieron varias vulnerabilidades en TimThumb que podrían permitir a un atacante ejecutar código malicioso en el servidor.
 
 cb-->Config backups
 dbe-->Db exports
 u-->User IDs range. e.g: u1-5
      Range separator to use: '-'
      Value if no argument supplied: 1-10
 m-->Media IDs range. e.g m1-15
      Note: Permalink setting must be set to "Plain" for those to be detected
      Range separator to use: '-'
      Value if no argument supplied: 1-100
Separator to use between the values: ','
Default: All Plugins, Config Backups
Value if no argument supplied: vp,vt,tt,cb,dbe,u,m
Incompatible choices (only one of each group/s can be used):
 - vp, ap, p
 - vt, at, t

```bash
wpscan --url https://miwifi.com --enumerate vp,vt,tt,cb,dbe,u --api-token="..."
```
En este caso lo que estamos enumerando es
- vp: plugins vulnerables
- vt: temas vulnerables
- tt: la herramienta buscará activamente archivos y directorios relacionados con TimThumb en el sitio web objetivo. Esto incluye buscar ubicaciones típicas donde se encuentra el script, como "/wp-content/themes" y "/wp-content/plugins".
  El escaneo de TimThumb con Wpscan puede ayudar a identificar versiones obsoletas o vulnerables de TimThumb que podrían explotarse para obtener acceso no autorizado al sitio web o para ejecutar código malicioso.
- cb: busca y escanea posibles copias de seguridad de configuraciones en un sitio de WordPress, que pueden contener información sensible.
- dbe: busca archivos de exportación de bases de datos en un sitio de WordPress, los cuales pueden contener información sensible.
- u: identificar usuarios por ids.

### CURL
La herramienta curl es una utilidad de línea de comandos que permite realizar solicitudes HTTP, HTTPS y otros protocolos desde la línea de comandos o scripts. Con curl, puedes enviar y recibir datos a través de URL, lo que la convierte en una herramienta versátil para interactuar con servicios web, descargar archivos, probar APIs y más. Puedes usar curl para realizar solicitudes GET, POST, PUT, DELETE, entre otras, y recibir las respuestas correspondientes desde el servidor.
> Esta herramienta también es útil  para enumerar plugins de una página web.

Tramitar una petición por get
```bash
curl -s -X GET "https://miwifi.com"
```

- "-s" es el parámetro que significa "silent" o "silencioso". Esto indica a curl que no muestre ninguna salida o información adicional, lo que lo hace útil cuando solo estás interesado en el resultado de la solicitud sin necesidad de ver mensajes de progreso o detalles adicionales.
    
- "-X GET" es el parámetro que especifica el método de solicitud HTTP a utilizar. En este caso, se establece como "GET", lo que indica que se realizará una solicitud GET al servidor. El método GET se utiliza para recuperar información o recursos del servidor.

Tramitar una petición por post enviando un archivo.[[Wordpress XMLRPC.php]]
```bash
curl -s -X POST "https://miwifi.com/xmlrpc.php" -d@file.xml
```
- "-d@": sirve para indicarle el archivo que quieres enviar.


### Enumerar usuarios 
Rutas vulnerables comunes en WordPress que podrían permitir la enumeración de usuarios:

1. Enumeración de usuarios a través de la API REST:
    
    - Ruta: `/wp-json/wp/v2/users`
    - Algunas versiones antiguas de WordPress permiten la enumeración de usuarios mediante esta ruta de la API REST.
2. Enumeración de usuarios mediante el archivo de registro:
    
    - Ruta: `/wp-content/debug.log`
    - Si la opción de depuración está habilitada en la configuración de WordPress, los mensajes de registro pueden contener información sobre usuarios.
3. Enumeración de usuarios a través del archivo de autor:
    
    - Ruta: `/?author=<ID>`
    - Algunas versiones antiguas de WordPress permiten la enumeración de usuarios mediante la visualización de entradas de blog asociadas a los diferentes ID de usuario.
4. Enumeración de usuarios a través de archivos de sitemap personalizados o vulnerables:
    
    - Ruta: `/wp-sitemap-users-1.xml`
    - Algunos complementos o configuraciones personalizadas pueden generar archivos de sitemap que revelen información de los usuarios.

------
### RELACIONADOS
- [[Herramientas]]
- [[Wordpress XMLRPC.php]]