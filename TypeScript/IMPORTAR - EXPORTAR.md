
### Exportación

La exportación en TypeScript se utiliza para hacer disponibles variables, funciones, clases o cualquier otra construcción fuera del módulo actual para que puedan ser utilizadas en otros módulos.

Ejemplo:

```typescript
// En el archivo example.ts

// Exportar una variable
export const myVariable: number = 42;

// Exportar una función
export function myFunction(): void {
    console.log("Hola, mundo!");
}

// Exportar una clase
export class MyClass {
    constructor(public name: string) {}
}

```

### Importación

La importación en TypeScript se utiliza para acceder a las variables, funciones, clases u otros elementos que han sido exportados desde otro módulo.

Ejemplo:

```typescript
// En otro archivo

// Importar todo desde example.ts
import * as example from './example';

// Utilizar la variable exportada
console.log(example.myVariable);

// Llamar a la función exportada
example.myFunction();

// Crear una instancia de la clase exportada
const instance = new example.MyClass("Ejemplo");
console.log(instance.name);

```

### Uso

Las exportaciones e importaciones permiten utilizar código de un archivo en otro, lo que facilita la creación de aplicaciones más grandes y mantenibles.

- **Exportación**: Se coloca la palabra clave `export` antes de la declaración de la variable, función o clase que se desea exportar.
- **Importación**: Se utiliza la palabra clave `import` seguida del nombre de la variable o elemento que se quiere importar, junto con la ruta del archivo en el que se encuentra.

En resumen, la exportación e importación en TypeScript son herramientas fundamentales para organizar y estructurar un proyecto, permitiendo la creación de módulos reutilizables y facilitando el mantenimiento del código.