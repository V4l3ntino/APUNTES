La `desestructuración` es el método que se utiliza para poder sacar individualmente los atributos de un objeto y guardarlos en otra variable
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
const { song: cancion } audioPlayer;

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

