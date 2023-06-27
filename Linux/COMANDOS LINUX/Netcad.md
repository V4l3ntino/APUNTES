-----
- Tags: #Linux #puertos #netcat #nc 
----

### Conectarse por un puerto

```bash
nc localhost 30000
```

### Ponerse en escucha por un puerto
```bash
nc -nlvp 8080
```

1. n: especificamos que no queremos que nos haga resolución DNS
2. l: (listen) indicamos que vamos a ponernos en modo escucha
3. v: es de verbose y sirve para que a medida que se está ejecutando nos muestre la información por consola
4. p: sirve para indicarle un número de puerto local

-----
### Relacionados

- [[NCAT]] (Conectarse a un puerto cifrando la comunicación)
- Enlace a las [[Tareas 📋]], el curso se encuentra en la carpeta 39
