-----
- Tags: #Linux #Hexadecimal #xxd #Comandos 
-----

### xxd
Con este comando podemos convertir el output en hexadecimal, ejempolo:
```bash
cat /etc/hosts | xxd

cat /etc/hosts | xxd -ps #Muestra en el output solo la parte hexadecimal

cat /etc/hosts | xxd -ps | xargs #Compacta en una misma línea el output hexadecimal

cat /etc/hosts | xxd -ps | xargs | tr -d ' ' #Compacta en una misma línea el output y además elimina los espacios.
```

Proceso inverso, pasar de exadecimal a un output claro
```bash
echo -e "23205374616e6461726420686f7374206164647265737365730a3132372e
302e302e3120206c6f63616c686f73740a3a3a3120202020202020206c6f
63616c686f7374206970362d6c6f63616c686f7374206970362d6c6f6f70
6261636b0a666630323a3a31202020206970362d616c6c6e6f6465730a66
6630323a3a32202020206970362d616c6c726f75746572730a2320546869
7320686f737420616464726573730a3132372e302e312e3120206465736b
746f70416e6f6e796d75730a" | xxd -ps -r
```
Con el parámetro -ps le indicamos que solo queremos la parte hexadecimal y con -r indicamos que queremos hacer el proceso inverso (reverse).

------
Relacionado:

- [[Comprimir y Descomprimir archivos con 7z]] 
- Enlace a las [[Tareas 📋]], este tema se muestra en la carpeta 36

