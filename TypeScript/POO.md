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
	this.name = name;
	this.address = address;
	
	}

}
```