# Clases predefinidas

Las clases predefinidas en Java son clases que ya están definidas en el lenguaje Java y se pueden utilizar sin necesidad de definirlas de nuevo. Estas clases son parte de la biblioteca estándar de Java, también conocida como Java Class Library o Java API.

### Math

La clase predefinida `Math` en Java es una biblioteca de funciones matemáticas que proporciona una amplia variedad de operaciones matemáticas comunes y avanzadas. La clase `Math` es parte de la biblioteca estándar de Java y se encuentra en el paquete `java.lang`.

A continuación, se describen algunos de los métodos más utilizados en la clase predefinida `Math`:

1. `abs()`: Este método devuelve el valor absoluto de un número. Por ejemplo, `Math.abs(-5)` devuelve `5`.
2. `ceil()`: Este método devuelve el número entero más pequeño que es mayor o igual que un número decimal. Por ejemplo, `Math.ceil(4.2)` devuelve `5.0`.
3. `floor()`: Este método devuelve el número entero más grande que es menor o igual que un número decimal. Por ejemplo, `Math.floor(4.9)` devuelve `4.0`.
4. `round()`: Este método devuelve el valor redondeado de un número decimal a la unidad más cercana. Por ejemplo, `Math.round(4.5)` devuelve `5`.
5. `max()`: Este método devuelve el valor más grande entre dos valores. Por ejemplo, `Math.max(10, 20)` devuelve `20`.
6. `min()`: Este método devuelve el valor más pequeño entre dos valores. Por ejemplo, `Math.min(10, 20)` devuelve `10`.
7. `sqrt()`: Este método devuelve la raíz cuadrada de un número. Por ejemplo, `Math.sqrt(16)` devuelve `4`.
8. `pow()`: Este método devuelve el valor de un número elevado a una potencia específica. Por ejemplo, `Math.pow(2, 3)` devuelve `8`.
9. `random()`: Este método devuelve un número aleatorio entre 0 y 1. Por ejemplo, `Math.random()` devuelve un número aleatorio como `0.384785426`.

Estos son solo algunos de los métodos más utilizados de la clase predefinida `Math`. La mayoría de los métodos de la clase `Math` **son estáticos**, lo que significa que se pueden llamar sin tener que crear una instancia de la clase `Math`. Para utilizar los métodos de la clase `Math`, simplemente se llama al método y se proporcionan los parámetros necesarios.

### Strings

La clase predefinida `String` en Java es una clase que se utiliza para representar cadenas de caracteres. La clase `String` es parte de la biblioteca estándar de Java y se encuentra en el paquete `java.lang`.

A continuación, se describen algunos de los métodos más utilizados en la clase predefinida `String`: &#x20;

1. `length()`: Este método devuelve la longitud de la cadena de caracteres. Por ejemplo, `String s = "Hola"; s.length()` devuelve `4`.
2. `charAt()`: Este método devuelve el carácter en el índice especificado en la cadena de caracteres. Por ejemplo, `String s = "Hola"; s.charAt(0)` devuelve `H`.
3. `substring()`: Este método devuelve una subcadena de la cadena de caracteres. El primer parámetro especifica el índice inicial de la subcadena, y el segundo parámetro especifica el índice final. Por ejemplo, `String s = "Hola"; s.substring(1, 3)` devuelve `ol`.
4. `indexOf()`: Este método devuelve el índice de la primera aparición de un carácter o una subcadena en la cadena de caracteres. Si el carácter o la subcadena no se encuentra en la cadena de caracteres, el método devuelve `-1`. Por ejemplo, `String s = "Hola mundo"; s.indexOf("mundo")` devuelve `5`.
5. `toLowerCase()`: Este método convierte todos los caracteres de la cadena de caracteres en minúsculas. Por ejemplo, `String s = "HOLA"; s.toLowerCase()` devuelve `hola`.
6. `toUpperCase()`: Este método convierte todos los caracteres de la cadena de caracteres en mayúsculas. Por ejemplo, `String s = "hola"; s.toUpperCase()` devuelve `HOLA`.
7. `replace()`: Este método reemplaza todas las apariciones de un carácter o una subcadena en la cadena de caracteres con otra cadena de caracteres. Por ejemplo, `String s = "Hola mundo"; s.replace("mundo", "amigo")` devuelve `Hola amigo`.
8. `trim()`: Este método elimina todos los espacios en blanco del principio y el final de la cadena de caracteres. Por ejemplo, `String s = " Hola "; s.trim()` devuelve `Hola`.

Estos son solo algunos de los métodos más utilizados de la clase predefinida `String`. La mayoría de los métodos de la clase `String` son inmutables, lo que significa que no modifican la cadena de caracteres original, sino que devuelven una nueva cadena de caracteres que contiene el resultado de la operación. Para utilizar los métodos de la clase `String`, simplemente se llama al método en una instancia de la clase `String`.

\
