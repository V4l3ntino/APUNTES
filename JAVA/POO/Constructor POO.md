El constructor de una clase sirve para inicializar los objetos de una clase, este debe tener el mismo nombre que la clase a la que pertenece. 
```JAVA
public Coche(String marca, String modelo, int anio){
		this.marca = marca;
		this.modelo = modelo;
		this.anio = anio;
	}
```

Una clase puede tener **cero, uno o más de un constructor**. Cuando la clase no tiene ningún constructor Java se encarga de proporcionar uno vacío. Podemos crear tantos constructores cuantos nosotros queramos con la restricción de que todos tienen que tener alguna diferencia.

Podemos crear constructores que se usen entre ellos, por ejemplo crear un constructor amplio que sea más general y otro más concreto que utilice los parámetros del primero.

Ejemplo de caso de uso: tenemos una serie de coches que fueron creados en un mismo año, podemos hacer un segundo constructor de dos formas.

1. Forma
	 ![[Pasted image 20231229153516.png]]
2. Forma
	![[Pasted image 20231229153216.png]]

Videos Relacionados
---
![Constructores](https://youtu.be/4pIcVlxh0lw?si=0nE8ArNizXUrdqz7)
![Crear objetos](https://youtu.be/zhUTqZk3-ks?si=xD2v7Pc1DfPyXGXZ)