-----
- Tags: #Linux #Fuzzing #Indirecto #Recopilación 
-----
Podemos usar las siguientes páginas webs para recolectar información de las url de una página web.
- [Phonebook](https://phonebook.cz/): aquí podemos recolectar rutas de una página web, además nos permite encontrar subdominios e incluso [[Formas de recolectar correos electrónicos]]. 
- Podemos utilizar una herramienta en github llamada [ctfr](https://github.com/UnaPibaGeek/ctfr) que se encargaría de reportar la información de forma indirecta pero mostrandola en consola.
- [Sublister](https://github.com/aboul3la/Sublist3r): otra herramienta de github que nos permite recolectar información de ineternet obteniendo subdominios, rutas...

### Instalación de sublister

```bash
git clone https://github.com/aboul3la/Sublist3r.git
cd Sublist3r
sudo python3 setup.py install 
pip install -r requirements.txt 
```

### Demostración de la herramienta
```bash
python3 sublist3r.py -d gmail.com
```

- python3 sublister.py> con esto ponemos en ejecución la herramienta
- -d: indicamos el dominio que queramos pasarle.

### Relacionados
- Enlace a [[INTRODUCCIÓN AL HACKING📋]], esto se explica en  la carpeta 10 de SEC3.
- [[Fuzzing directo]]
- [[Formas de recolectar correos electrónicos]]