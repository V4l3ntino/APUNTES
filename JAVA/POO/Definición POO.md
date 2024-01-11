---
tags:
  - POO
  - CONSTRUCTOR
  - CLASES
  - JAVA
---

- Clases: es un molde o plantilla mediante la cuál podemos construir objetos. Las clases se podría asociar en base de datos como tablas.
	- Atributos: elementos que forman una clase
	- Constructor: es el método de la clase que sirve para inicializar los objetos, el nombre del constructor debe tener siempre el mismo nombre que el de la clase.
	- Métodos

- Objetos: serían como los registros de una tabla, los objetos de nuestro programa van a poder interactuar entre sí 

- Encapsula-miento: mecanismo mediante el cual un objeto oculta parte de su estructura y/o comportamiento a los demás objetos.

(Más información) --> [[1.4_Atributos_y_Métodos.pdf]]

## Estructura de una Clase
En una clase el nombre siempre debe tener la Primera letra en mayuscula

```JAVA
// El nombre de la clase debe ser el mismo que el nombre del fichero
public class Coche {
	//Atributos
	private String marca;
	private String modelo;
	private int anio;
	//Constructor
	public Coche(String marca, String modelo, int anio){
		this.marca = marca;
		this.modelo = modelo;
		this.anio = anio;
	}
	//Método de la clase 
	public void arrancarCoche(){
			System.out.println("El coche %s %s %d ha arrancado".formatted(
			marca, modelo, anio)); 
	}
}
```

**Package**: un paquete es una unidad organizativa de código que permite agrupar las clases de una manera lógica, es decir sería una carpeta que alberga los archivos. Los paquetes también se pueden organizar de forma jerárquica, es decir paquetes que alberguen otro paquetes.

**Marcadores de posición**
Los `%s` y `%d` son marcadores de posición que se llenarán con valores específicos.

- `%s` es un marcador para una cadena de texto.
- `%d` es un marcador para un número entero.
`.formatted()` es un método que toma los argumentos proporcionados y los inserta en los marcadores de posición correspondientes en la cadena de texto.

## Clase App 

Es la clase principal que alberga el método main, este es el método que se ejecuta cuando tu aplicación comienza a correr. Dentro de este método puedes inicialiar tu programa (crear objetos, llamar a otras clases y métodos). Es el punto de inicio de la ejecución de tu programa.

```JAVA
public class App{
	public static void main(String[] args) {
		Coche coche = new Coche("Ford", "Focus", 2020);
			coche.arrancarCoche();
	}
}
```

**Instanciar**: usamos esta palabra cuando creamos un objeto concreto usando la plantilla de una clase en el método main de la clase App.

Apuntes en PDF
----

![[1.2_Mi_primera_clase.pdf]]

----
Relacionado:

- [[Constructor POO]]