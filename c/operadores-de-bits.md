---
description: Operando en binario
---

# Operadores de bits

Los operadores bit a bit realizan operaciones AND bit a bit (**`&`**), OR exclusivo bit a bit (**`^`**) y OR inclusivo bit a bit (**`|`**)

Los operandos de los operadores bit a bit deben tener tipos enteros, pero sus tipos pueden ser diferentes. Estos operadores realizan las conversiones aritméticas habituales; el tipo del resultado es el tipo de los operandos después de la conversión.

### And (&)

El operador AND bit a bit compara cada bit de su primer operando con el bit correspondiente de su segundo operando. **Si ambos bits son 1**, el bit del resultado correspondiente **se establece en 1**. De lo contrario, el bit del resultado correspondiente se establece en 0.

```
a AND b = c
0 and 0 = 0
0 and 1 = 0
1 and 0 = 0
1 and 1 = 1
```

Para que se entienda mejor lo que hace este operador:

```
int a, b, c;

c = a & b

0110-0011
1010-1001
---------
0010-0001
```

### OR ( | )

El operador OR exclusivo bit a bit compara cada bit de su primer operando con el bit correspondiente de su segundo operando. Si un bit es 0 y el otro bit es 1, el bit del resultado correspondiente se establece en 1. De lo contrario, el bit del resultado correspondiente se establece en 0.

```
a OR b = c
0 or 0 = 0
0 or 1 = 1
1 or 0 = 1
1 or 1 = 1
```

### XOR (^)

El operador OR exclusivo bit a bit compara cada bit de su primer operando con el bit correspondiente de su segundo operando. En el caso de que **solo uno de los dos bits sea 1**, el resultado sera 1. De no ser asi, sera 0

```
a XOR b = c
0 xor 0 = 0
0 xor 1 = 1
1 xor 0 = 1
1 xor 1 = 0
```

### NOT (\~)

El operador OR exclusivo bit a bit compara cada bit de su primer operando con el bit correspondiente de su segundo operando. Este operador especifica que el segundo operando tienes que ser distinto del primero.

```
NOT a = b
not 0 = 1
not 1 = 0
```

### Operadores de desplazamientos

Los operadores de desplazamiento se utiliza para mover los bits hacia la **izquierda `<<`** o hacia la **derecha** **`>>`**. Los bits  de las esquinas cuando son desplazados hacia su esquina, se pierden y el nuevo espacio se rellena con un 0. Es decir si desplazamos una serie de bits hacia la derecha, el bit de la derecha del todo se perdera y el primer bit empezando por la izquierda sera un 0.

A la hora de utilizar la estos operadores hay que especificar cuantos cuntos bits quieres deslazar.

```
int a, b, c;

c = a << x;    //Desplazar los bits x veces hacia la izquierda
c <<= a;      //Desplazara los bits de c un bit hacia la izquierda y los guarda en a
c <<= 1:     //Deslaza los bits de c hacia laa izquierda y lo garda en c
```

Bibliografia

* [https://learn.microsoft.com/es-es/cpp/c-language/c-bitwise-operators?view=msvc-170](https://learn.microsoft.com/es-es/cpp/c-language/c-bitwise-operators?view=msvc-170)
* [https://www.youtube.com/watch?v=jnpqz8EGOeE](https://www.youtube.com/watch?v=jnpqz8EGOeE)
