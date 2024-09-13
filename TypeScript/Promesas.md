  Una **promesa** en TypeScript (al igual que en JavaScript) es un objeto que representa la eventual finalización (o fallo) de una operación asíncrona y su valor resultante. Es una forma de trabajar con código asíncrono sin necesidad de usar **callbacks** (funciones de retroceso), lo que facilita la lectura y mantenimiento del código.
### Estados de una Promesa:

Una promesa puede encontrarse en uno de estos tres estados:

1. **Pendiente** (`pending`): La operación asíncrona está en progreso y aún no ha completado ni ha fallado.
2. **Resuelta** (`fulfilled`): La operación asíncrona ha sido completada con éxito y devuelve un valor.
3. **Rechazada** (`rejected`): La operación asíncrona ha fallado y devuelve una razón o error.


Estructura:

``` typescript
//PROMESA CUMPLIDA
new Promise (( resolve, reject ) => {
	resolve('Mi amigo cumplió');
}).then((message) => console.log(message))

//PROMESA INCUMPLIDA
new Promise ((resolve, reject) => {
	reject('Mi amigo no cumplió');
})
	.then((message) => console.log(message));
	.catch(errorMessage => console.log(errorMessage));
	.finally(() => console.log('Fin de la promesa'));
```

* .then() : captura el resultado de la promesa cuando es cumplida.
* .catch() : captura la excepción cuando la promesa no se cumple por algún error.
* .finally() : se ejecuta si o si independientemente del resultado de la promesa.