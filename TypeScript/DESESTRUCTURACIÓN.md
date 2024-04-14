La `desestructuración` es el método que se utiliza para poder sacar individualmente los atributos de un objeto y guardarlos en otra variable

Objetos
--


```typescript
const audioPlayer: AudioPlayer = {
	audioVolume: 90,
	songDuration: 36,
	song: "Mess",
	details: {
		author: "Ed Sheeran",
		year: 2015
	}
}

const { song, songDuration, details } = audioPlayer;
const { author } = details;

console.log(song); //RESULTADO 'Mess'
console.log(songDuration); // RESULTADO '36'
console.log(author); // RESULTADO 'Ed Sheeran'
```

La lógica en la sintaxis es que cuando pones el mismo nombre que en el atributo se creará una nueva variable con los datos de ese mismo atributo, si por el contrario quisiéramos cambiarle el nombre a la variable pero que contenga los mismos datos del atributo se especificaría de la siguiente manera:

```typescript
const { song: cancion } = audioPlayer;

console.log(cancion); // RESULTADO 'Mess'
```

También para `desestructurar` un objeto dentro de otro objeto se puede hacer como en el primer ejemplo (que sería la manera más legible de hacer) o de la siguiente manera:

```typescript
const { details: { author } } = audioPlayer
```


Esta forma de `desestructurar` es lo mismo que si hiciéramos lo siguiente:

```typescript
const song = audioPlayer.song;
const cancion = audioPlayer.song;
const author = audioPlayer.details.author
```

Pero para evitar esto y ahorrar más tiempo se hace de la primera forma



Arrays
--

Según la posición en la que nombremos la variable obtendrá un valor u otro, ejemplo:
```typescript
const dbz: string[] = ['Goku', 'Vegeta', 'Trunk'];
const [ p1, p2, p3] = dbz

console.log(p1); // MUESTRA 'Goku'
console.log(p2); // MUESTRA 'Vegeta'
console.log(p3); // MUESTRA 'Trunks'
```

También si no necesitamos las dos primeras variables podemos saltar de posición poniendo simplemente una coma:

```typescript
const [ , , trunks] = dbz

console.log(trunks) // MUESTRA 'Trunks'
```

La otra forma menos eficiente sería con el método tradicional, creamos una variable y la igualamos al índice del array:

```typescript
const trunks = dbz[2]
```

Podemos definir una condición de tipo `or` indicando que si el índice no existe muestre un mensaje distinto

```typescript
const trunks = dbz[5] || 'No existe el personaje'

const [ , , , , , trunks] = dbz || 'No existe el personaje'
```

