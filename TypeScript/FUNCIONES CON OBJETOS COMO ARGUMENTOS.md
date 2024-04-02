Si queremos pasarle un objeto que tenga unas características específicas a una función como parámetro debemos primero crear una interfaz
```typescript
interface Character {
name: string;
hp: number;
showHp: () => void;
}
```

Esto se hace para que los tipos de los atributos de un objeto que se pasen como parámetro a una función sean de una manera específica.
```typescript
const healCharacter = { character: Character, amount: number} => {
character.hp += amount;
}
```

Si creamos un objeto de tipo Character podremos acceder a la función healCharacter y poder curar a nuestro personaje.

```typescript
const stridder: Character = {
name: "Stridder",
hp: 50,
showHp: function () {
	console.log(`El personaje tiene ${this.hp} de vida`)
	}
}

healCharacter(stridder, 49)
```
---
[[METODOS TIPADO]]