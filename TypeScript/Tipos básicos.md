
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