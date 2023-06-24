-----
- Tags: #FTP 
-----
Cuando está expuesto el puerto 20 y 21 por el servicio FTP debemos saber que versión corre por detrás 
```bash
sudo nmap -p21 -sVC 192.168.0.133
```

- -sVC: nos lanza una serie de scripts básicos de reconocimiento además de listar la versión del servicio que corre por detrás

Los servidores ftp aveces tiene configurado por defecto el usuario anonymous. Es un usuario invitado que no tiene contraseña y que nos podemos conectar fácilmente. Lanzando el conjunto de scripts básicos de reconocimiento podemos saber si el usuario anonymous está activo en el servicio ftp. 
También podemos lanzar directamente el script específico para averiguar el usuario anonymous de la siguiente manera:
```bash
sudo namp -p21 --script=ftp-anon 192.168.0.133 
```

### Hydra
**FTP**
En caso de que no exista podemos realizar un ataque de fuerza bruta con la siguiente herramienta:
```bash
sudo hydra -l user -P /usr/share/wordlist/rockyou.txt ftp://192.168.0.133 -t 15 -s 2121
```

- -l: (login) indicamos el usuario
- -P: (password) indicamos la contraseña
- -t: (threads) hilos para lanzar tareas en paralelo
- -s: (source port) sirve para indicarle el puerto en el que se encuentra el servicio. (Si no se indica el ataque se hará en el puerto por defecto del servicio, en este caso del ftp sería el 21)
> Hay que tener en cuenta que la mayúsculas y la minúsculas influyen en el comando. Cuando ponemos en mayúscula un parámetro estamos indicando una ruta de un archivo.txt con un conjunto de usuarios o contraseñas ejemplo:
```bash
sudo hydra -L /home/valen/usuarios.txt -P /usr/share/wordlist/rockoy.txt ftp://192.168.0133

sudo hydra -L /home/valen/usuario.txt -p contraseña123 ftp://192.168.0.133
```

**SSH**
```bash
sudo hydra -l user -P password.txt ssh://192.168.0.133 -s 22
```

### CODENAME DE UBUNTU(Versión de Ubuntus)
Codename es el **nombre código que se le da a una determinada versión de Ubuntu**. Cuando realizamos un scaneo a un servicio, por ejemplo al ssh, nos muestra la versión del servicio. Pues bién esa cabecera es el codename, si nosotros buscamos por internet el codename de la versión y ponemos al final launchpad podemos ver en la página de launchpad.net la versión de ubuntu que corre por detrás.
```bash
sudo nmap -p2222 -sCV localhost
Starting Nmap 7.94 ( https://nmap.org ) at 2023-06-18 16:47 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000071s latency).
Other addresses for localhost (not scanned): ::1

PORT     STATE SERVICE VERSION
2222/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 94:cc:12:90:d9:7a:9d:6f:19:8f:99:9c:e1:21:7d:fb (RSA)
|   256 ce:a3:e6:b3:23:cb:28:fd:c6:8e:88:4f:3c:ff:08:b0 (ECDSA)
|_  256 b9:9c:bc:32:95:34:6d:7d:c7:50:9c:5f:c9:c9:7b:7f (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.78 seconds
```

El codename en este caso sería **OpenSSH 8.2p1 Ubuntu 4ubuntu0.7**.