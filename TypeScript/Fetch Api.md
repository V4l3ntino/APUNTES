A continuación se va a mostrar un caso de prueba de petición a una api proporcionando una key.

```typescript
const apiKey = '...'

fetch(`https://laurl=${apiKey}`)
	.then((resp) => {
		return resp.json()
	})
	//OBTENGO EL CUERPO COMPLETO
	.then( (body) => console.log(body))
	//DESESTRUCTURACIÓN
	.then( ({data}) => console.log({ data }))
	.catch((err) => console.log( err ))
```

