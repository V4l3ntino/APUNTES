----
- Tags: #Linux #Comandos #Hacking 
------

### Convertir un número a binario

```bash
echo "obase=2; 192" | bc
```

obase=2 => Indicamos que queremos hacer una canversión en base 2. 
bc => Indicamos que queremos que se aplique el cálculo

De la misma manera podemos utilizar el **bc** para realizar otros cálculos como elevar una potencia
```bash
echo "2^32" | bc
```

> Con el bc simplemente estamos indicando que queremos realizar un cálculo matemático de un elemento.

