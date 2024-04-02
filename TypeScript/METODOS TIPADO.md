
Variables
--

Al declarar variables podemos asignarle el tipo de dos maneras, poniendo el tipo explícitame con dos puntos o asignándole un valor directamente y que typescript se encargue de darle un tipo a ese valor

``` TYPESCRIPT

const nombre = 'paco'

const nombre: String 

```

También podemos declarar una variable con dos tipos, añadiendo un pipe entre cada tipo indicamos que la variable podría ser por ejemplo de tipo String o de tipo Number

``` Typescript
const variable: String | number
```

Si queremos que en vez de una cadena de caracteres sea una palabra concreta 

``` typescript
const variable: 'Hola Mundo' | number
```

Y lo mismo en el tipo number

```typescript
const variable: 'Hola Mundo' | 12
```

Con esto le estamos indicando que la variable solo puede ser 'Hola Mundo' o el número 12

Arrays
--

Para tipar un lista se debe añadir "[ ]"  después del tipo, por ejemplo 

```typescript
const skills: (number | string | boolean) [] = ['Bash', 'Counter', 'Healing', 123, true];
```

Esto le indica a typescript que cada objeto que hay en la lista separado por comas puede ser o un string, un número o un booleano pero no otra cosa.






Objetos
--
Para tipar un objeto es necesario crear una interfaz
```typescript
interface Character {
name: string;
hp: number;
skills: (string|number)[];
hometown?: string;
}
```

Esta interfaz es simplemente para indicarle a typescript los atributos y el tipo de cada atributo que puede tener un objeto que sea de tipo Character.
> ==hometown?: string==;  El interrogante sirve para indicar que el atributo hometown no sea obligatorio en el objeto, es decir que no es relevante si el atributo existe o no existe en la variable
> ![[Pasted image 20240401221733.png]]
```typescript
interface Character {
name: string;
hp: number;
skills: (string|number)[];
hometown: string | undefined;
}
```

> hometown: string | undefined; Ahora indicamos que hometown puede ser de tipo string o puede no tener nada, pero es relevante, es decir que si o si debe existir en el objeto
> ![[Pasted image 20240401221836.png]]


Funciones
---
El tipado de una función se declara después de los parámetros
```typescript
const addNumber = (firstParam, secondParam): number => {
	return firstParam + secondParam;
}
```

Los parámetros también debes ser tipados
```typescript
const addNumber = (firstParam: number, secondParam: number = 2): number =>{
	return firstParam * secondParam;
}
```

En este caso secondParam no va ser obligatorio porque su valor va ser siempre 2 pero podemos cambiarle este valor si le especificamos un nuevo número en la llamada de la función,
ejemplo:
```typescript
const multiply = (first: number, second?: number, third: number = 2): number => {
	return first + third;
}
const result: number = myltiply(1,0,5);
console.log (result)
```
Esta función devolverá 6
```typescript
const multiply = (first: number, second?: number, third: number = 2): number => {
	return first + third;
}
const result: number = myltiply(1);
console.log (result)
```
Esta función devolverá 3


---
[[FUNCIONES CON OBJETOS COMO ARGUMENTOS]]
