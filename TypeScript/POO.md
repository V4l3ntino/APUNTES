Crear una clase:

``` typescript
class Person {
	private name: string;
	private address: string;
	
	
	constructor(name: string, address: string){
	this.name = name;
	this.address = address;
	}

}

```

En typescript no es tan común que las propiedades sean declaradas, ya con crear el constructor typescript automáticamente generará las propiedades de esa clase, ejemplo:

```typescript
class Person {

	constructor(
		private name: string, 
		private address: string){
	
	}

}
```

Ni si quiera es necesario igualar los parámetros a los atributos porque eso también lo hace automáticamente

Clases extendidas
--

Una clase extendida es una clase que hereda los atributos de la clase padre y además alberga sus propios atributos.

```typescript

class Cosa {
	constructor (private cosa1: string, private cosa2: string){}
}

class Person extends Cosa {

	constructor(
		private name: string,
		private address: string,
		cosa1:string,
		cosa2: string,
	){
		super(cosa1,cosa2)
		this.name = name;
		this.address = address;
	}

}


```

Con super indicamos que los atributos que le pasamos como parámetro son igual a los atributos de la clase padre, el super debe ir al principio de todo en el constructor y siempre debe ser declarado.