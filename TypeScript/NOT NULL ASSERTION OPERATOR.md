
En TypeScript, el operador de aserción no nula (`!`) se utiliza para indicar al compilador que estás seguro de que un valor no es nulo o indefinido, incluso cuando el compilador no puede deducirlo por sí mismo. Esto puede ser útil cuando estás trabajando con tipos que podrían ser nulos o indefinidos, como variables que provienen de fuentes externas o de bibliotecas que no están tipadas.

Por ejemplo, considera este código:

```typescript
let x: string | null = null; // Al intentar acceder a una propiedad de x, TypeScript mostrará un error de compilación: // Error: Object is possibly 'null'. console.log(x.length);
```

Puedes usar el operador de aserción no nula para indicarle a TypeScript que estás seguro de que `x` no es nulo:

``` typescript
let x: string | null = null;
console.log(x!.length); // Ahora TypeScript no mostrará ningún error
```


Cuando utilizas el símbolo `?` después de un nombre de propiedad en la definición de una interfaz o tipo, estás indicando que esa propiedad es opcional. Esto significa que puede estar presente o ausente en un objeto que cumple con esa interfaz o tipo.

Por ejemplo:

```typescript
interface Persona {
  nombre: string;
  edad?: number; // La propiedad "edad" es opcional
}

const persona1: Persona = { nombre: "Juan" }; // OK
const persona2: Persona = { nombre: "María", edad: 25 }; // OK

```

En este ejemplo, `edad` es una propiedad opcional en la interfaz `Persona`, lo que significa que un objeto puede tener o no tener esa propiedad y aún así cumplir con la interfaz `Persona`. Si intentas acceder a una propiedad opcional que no está presente en un objeto, TypeScript no mostrará un error de compilación.

Entonces, simplemente se le llama una "propiedad opcional".


----
[[INTERFACES]]