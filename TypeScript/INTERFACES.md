  
Una interfaz en `TypeScript` es una estructura que define la forma de un objeto, incluyendo sus propiedades y tipos de datos. Sirve como un contrato que especifica qué propiedades y métodos debe tener un objeto para cumplir con esa interfaz. Se utiliza para garantizar consistencia y claridad en la comunicación entre partes del código.

La creación de una interfaz es bien sencilla, simplemente declaramos los atributos que queramos que tengan los futuros objetos que hereden de la misma:
```typescript
interface AudioPlayer {
audioVolume: number;
songDuration: number;
song: string;
}
```

También podemos declarar atributos que no sean obligatorios en el objeto, por ejemplo:

``` typescript
interface AudioPlayer {
audioVolume: number;
songDuration?: number;
song?: string;
}
```

De esta manera, al heredar de la interfaz `AudioPlayer`, el único atributo obligatorio será `audioVolume`, mientras que los demás podrán ser incluidos o no según la elección del programador.

Cuando en una interfaz definimos un objeto como atributo lo correcto sería crear una nueva interfaz que declare las propiedades de ese objeto como se muestra en el siguiente ejemplo

```typescript
interface AudioPlayer {
audioVolume: number;
songDuration: number;
song: string;
details: Details;
}

  

interface Details {
author: string;
year: number;
}
```