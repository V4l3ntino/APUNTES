-----
- Tags: #Linux #Osint #Reconocimiento 
----
Existe una página web capaz de reportar datos relevantes como redes sociales o páginas webs asociadas a una persona en función de la imagen que subas. 

- [pimeyes.com](https://pimeyes.com/es) -> Esta página web no es del todo gratuita, solo nos deja realizar 3 búsquedas por día, está un poco limitada pero aun así es bastante útil.

### [Dehashed.com](https://dehashed.com/)
Esta es otra página web de pago que permite listar información de base de datos que han sido liqueadas por brechas de seguridad. Aveces te puede reportar credenciales de usuarios que han sido expuestos.


### Geolocalizar la posición de una foto a través de los meta-datos

Podemos obtener mucha información con los metadatos de una imagen, como el tipo de móvil que tomó la foto, el modelo de la cámara, la fecha exacta cuando se tomó la foto y lo más heavy la posición exacta donde se tomó.
Para ello tenemos que descargarnos una selfie cualquiera por internet, bien podemos guardarnos la imagen o podemos recurrir del comando wget, tan sencillo como hacer los siguiente:
```bash
wget https://urldelafoto.jpg
```

Ahora usaremos la herramienta **exiftool**, que viene preinstalada en Kali o Parrot y haremos lo siguiente:
```bash
exifttool foto.jpg
```
Esto nos arrojará un montón de información, pero a nosotros solo nos interesa una cosa, la GPS Position, que no siempre vendrá en todas las fotos ya que no siempre se publica todos lo metadatos de una foto. En caso de que sí aparezca este apartado nos puede mostrar algo como esto `48 deg 50' 0.72" N` 
Pues bien esto tal cual no nos sirve para copiar y pegar en google maps, lo que tenemos que hacer es añadirle un par de parámetros más:
```bash
exiftool -n -p '$GPSPosition' foto.jpg
```

También podemos sacar por separado la Latitud y la Longitud
```bash
exiftool -n -p '$GPSLatitude,$GPSLongitude' foto.jpg
```





----
### Relacionados
- [[Formas de recolectar correos electrónicos]]
- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se explica en la carpeta 5 de SEC3