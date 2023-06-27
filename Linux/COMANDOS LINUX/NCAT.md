-----
- Tags: #Linux #ncat #conexiones-cifradas
------

### Conexiones cifradas a puertos

Con **ncat** podemos usar el parámetro **-ssl** para conectarnos a un puerto en específico  con el protocolo ssl para que la comunicación vaya **encryptado**.
```bash
ncat --ssl localhost 30001

```

Poner en escucha un puerto con ncat es lo mismo que [[Netcad]] 
```bash
ncat -nlvp 443 -e /bin/bash
```

-e: (execute) sirve para indicar que ejecute una acción, en este caso está ofreciendo por el puerto 443 una bash

### Relacionados
---
- [[Netcad]] (Conectarse a un puerto simplemente)
- Enlace a las [[Tareas 📋]], el curso se encuentra en la carpeta 38