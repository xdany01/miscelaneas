# Cheatsheet de Expresiones Regulares

#### Caracteres Básicos

- **`.`**: Coincide con cualquier carácter excepto un salto de línea.
- **`\d`**: Coincide con cualquier dígito (equivalente a `[0-9]`).
- **`\D`**: Coincide con cualquier carácter que no sea un dígito.
- **`\w`**: Coincide con cualquier carácter alfanumérico (letras, dígitos y guion bajo, equivalente a `[A-Za-z0-9_]`).
- **`\W`**: Coincide con cualquier carácter que no sea alfanumérico.
- **`\s`**: Coincide con cualquier carácter de espacio en blanco (espacio, tabulación, salto de línea).
- **`\S`**: Coincide con cualquier carácter que no sea espacio en blanco.
- **`\t`**: Coincide con la tabulación.
- **`\r`**: Coincide con el retorno de carro.
- **`\n`**: Coincide con el salto de linea.

#### Anclas

- **`^`**: Coincide con el inicio de una cadena.
- **`$`**: Coincide con el final de una cadena.
- **`\b`**: Coincide con un límite de palabra.
- **`\B`**: Coincide con un no-límite de palabra.

#### Cuantificadores

- **`*`**: Coincide con 0 o más repeticiones del patrón anterior.
- **`+`**: Coincide con 1 o más repeticiones del patrón anterior.
- **`?`**: Coincide con 0 o 1 repetición del patrón anterior.
- **`{n}`**: Coincide exactamente con `n` repeticiones del patrón anterior.
- **`{n,}`**: Coincide con `n` o más repeticiones del patrón anterior.
- **`{n,m}`**: Coincide con al menos `n` y como máximo `m` repeticiones del patrón anterior.

#### Grupos y Alternancia

- **`( )`**: Agrupa patrones.
- **`|`**: Alternancia (OR lógico), coincide con el patrón de la izquierda o el de la derecha.

#### Conjuntos de Caracteres

- **`[ ]`**: Define un conjunto de caracteres. Coincide con cualquier carácter dentro de los corchetes.
  - **`[aeiou]`**: Coincide con cualquier vocal.
  - **`[0-9]`**: Coincide con cualquier dígito.
  - **`[^aeiou]`**: Coincide con cualquier carácter que no sea una vocal.

#### Secuencias de Escape

- **`\`**: Escapa caracteres especiales.
  - **`\.`**: Coincide con un punto literal.
  - **`\\`**: Coincide con una barra invertida literal.

#### Otros

- **`(?: ... )`**: Grupo no capturador, agrupa patrones sin capturar coincidencias.
- **`(?= ... )`**: Lookahead positivo, coincide si el patrón dentro se encuentra a continuación.
- **`(?! ... )`**: Lookahead negativo, coincide si el patrón dentro no se encuentra a continuación.
- **`(?<= ... )`**: Lookbehind positivo, coincide si el patrón dentro se encuentra antes.
- **`(?<! ... )`**: Lookbehind negativo, coincide si el patrón dentro no se encuentra antes.

# Mas información:



### Banderas de Expresiones Regulares en JavaScript

1. **`g` (global)**
   
   - **Descripción**: Realiza una búsqueda global, encontrando todas las coincidencias en lugar de detenerse en la primera.
   - **Ejemplo**: 
     
     ```javascript
     let text = "Hello world! Hello universe!";
     let regex = /Hello/g;
     console.log(text.match(regex)); // ["Hello", "Hello"]
     ```

2. **`i` (insensitive)**
   
   - **Descripción**: Hace que la búsqueda sea insensible a mayúsculas y minúsculas.
   - **Ejemplo**: 
     
     ```javascript
     let text = "Hello world!";
     let regex = /hello/i;
     console.log(text.match(regex)); // ["Hello"]
     ```

3. **`m` (multiline)**
   
   - **Descripción**: Permite que las anclas `^` y `$` coincidan al inicio y al final de cada línea, no solo al inicio y al final de toda la cadena.
   - **Ejemplo**: 
     
     ```javascript
     let text = "Hello world!\nHello universe!";
     let regex = /^Hello/m;
     console.log(text.match(regex)); // ["Hello", "Hello"]
     ```

4. **`s` (dotAll)**
   
   - **Descripción**: Permite que el carácter `.` coincida con cualquier carácter, incluido el salto de línea `\n`.
   - **Ejemplo**: 
     
     ```javascript
     let text = "Hello\nworld!";
     let regex = /Hello.world/s;
     console.log(text.match(regex)); // ["Hello\nworld"]
     ```

5. **`u` (unicode)**
   
   - **Descripción**: Habilita el modo Unicode, permitiendo que la expresión regular trate correctamente los caracteres Unicode.
   - **Ejemplo**: 
     
     ```javascript
     let text = "𝟙𝟚𝟛";
     let regex = /\d/u;
     console.log(text.match(regex)); // ["𝟙"]
     ```

6. **`y` (sticky)**
   
   - **Descripción**: Realiza una búsqueda "pegajosa" que coincide solo desde la posición actual en la cadena y no reanuda desde el inicio.
   - **Ejemplo**: 
     
     ```javascript
     let text = "Hello world!";
     let regex = /world/y;
     regex.lastIndex = 6;
     console.log(regex.test(text)); // true
     console.log(regex.lastIndex); // 11
     ```

## Límite de Palabra (`\b`)

El límite de palabra `\b` es un tipo especial de ancla que se utiliza en expresiones regulares para indicar la posición entre un carácter de palabra (`\w`) y un carácter que no es de palabra (`\W`) o el inicio/final de una cadena. Un carácter de palabra incluye letras, dígitos y guiones bajos (equivalente a `[A-Za-z0-9_]`).

1. **Coincidir Palabras Exactas**
   
   ```javascript
   let text = "The quick brown fox jumps over the lazy dog.";
   let regex = /\bfox\b/;
   console.log(text.match(regex)); // ["fox"]
   ```
   
    Aquí, `\bfox\b` coincide con la palabra "fox" completa, no con subcadenas como "firefox".

2. **Buscar Palabras que Empiezan con una Letra Específica**
   
   ```javascript
   let text = "The quick brown fox jumps over the lazy dog.";
   let regex = /\b\w{3}\b/g;
   console.log(text.match(regex)); // ["The", "fox", "the", "dog"]
   ```
   
    Aquí, `\b\w{3}\b` busca todas las palabras de exactamente 3 caracteres.

3. **Eliminar Palabras Específicas**
   
   ```javascript
   let text = "The quick brown fox jumps over the lazy dog.";
   let regex = /\bthe\b/gi; // 'gi' para hacer la búsqueda insensible a mayúsculas
   let result = text.replace(regex, "");
   console.log(result); // " quick brown fox jumps over  lazy dog."
   ```
   
    Aquí, `\bthe\b` elimina la palabra "the" de manera insensible a mayúsculas y minúsculas.

## Límite No de Palabra (`\B`)

El límite no de palabra `\B` es el opuesto de `\b`. Coincide con cualquier posición que no esté en un límite de palabra.

1. **Coincidir Subcadenas Dentro de Palabras**
   
   ```javascript
   let text = "The quick brown fox jumps over the lazy dog.";
   let regex = /\Bfox\B/;
   console.log(text.match(regex)); // null
   ```
   
    Aquí, `\Bfox\B` no coincide con nada porque "fox" está en un límite de palabra.

2. **Añadir Caracteres Dentro de Palabras**
   
   ```javascript
   let text = "firefox";
   let regex = /\Bfire\B/;
   console.log(text.match(regex)); // null (fire no tiene caracteres antes y despues de palabra)
   
   let text2 = "firefox";
   let regex2 = /\Bfox\B/;
   console.log(text2.match(regex2)); // ["fox"]
   ```
   
    Aquí, `\Bfox\B` coincide con "fox" dentro de "firefox", porque "fox" no está en el límite de palabra.

# Lookahead y Lookbehind

*Las expresiones regulares utilizan **lookahead** y **lookbehind** para realizar búsquedas que dependen del contexto, sin incluir ese contexto en el resultado final.*

## Lookahead

El lookahead se utiliza para verificar que una secuencia de caracteres aparece después de la posición actual, sin incluir esa secuencia en la coincidencia final.

### Tipos de Lookahead

- **Lookahead Positivo (`(?= ...)`)**: Coincide si el patrón dentro del lookahead se encuentra a continuación del punto actual.
- **Lookahead Negativo (`(?! ...)`)**: Coincide si el patrón dentro del lookahead no se encuentra a continuación del punto actual.

#### Lookahead Positivo

```javascript
let text = "I have a cat and a dog.";
let regex = /\b\w+(?= and)/g;
console.log(text.match(regex)); // ["cat"]
```

Aquí, `\w+(?= and)` busca palabras que están seguidas por " and". En este caso, "cat" es la única palabra que cumple con esta condición.

#### Lookahead Negativo

```javascript
let text = "I have a cat and a dog.";
let regex = /\b\w+(?! and)/g;
console.log(text.match(regex)); // ["I", "have", "a", "dog"]
```

Aquí, `\w+(?! and)` busca palabras que **no** están seguidas por " and". En este caso, todas las palabras excepto "cat" cumplen con esta condición.

## Lookbehind

El lookbehind se utiliza para verificar que una secuencia de caracteres aparece antes de la posición actual, sin incluir esa secuencia en la coincidencia final.

### Tipos de Lookbehind

- **Lookbehind Positivo (`(?<= ...)`)**: Coincide si el patrón dentro del lookbehind se encuentra antes del punto actual.
- **Lookbehind Negativo (`(?<! ...)`)**: Coincide si el patrón dentro del lookbehind no se encuentra antes del punto actual.

#### Lookbehind Positivo

```javascript
let text = "I have a cat and a dog.";
let regex = /(?<=a )\w+/g;
console.log(text.match(regex)); // ["cat", "dog"]
```

Aquí, `(?<=a )\w+` busca palabras que están precedidas por "a ". En este caso, "cat" y "dog" son las palabras que cumplen con esta condición.

#### Lookbehind Negativo

```javascript
let text = "I have a cat and a dog.";
let regex = /\b(?!cat|dog)\w+/g;
console.log(text.match(regex)); // ["I", "have", "a", "and", "a"]
```

Aquí, `\b(?!cat|dog)\w+` busca palabras que **no** están precedidas por "cat" o "dog". En este caso, todas las palabras excepto "cat" y "dog" cumplen con esta condición.


# Grupo No Capturador

En las expresiones regulares, los paréntesis `(...)` se utilizan para agrupar partes de una expresión y capturar las coincidencias encontradas. Sin embargo, a veces solo necesitas agrupar partes de la expresión sin capturar las coincidencias. Aquí es donde los grupos no capturadores (`(?: ... )`) son útiles.

## Características de los Grupos No Capturadores

1. **Agrupación Sin Captura**: Permiten agrupar subexpresiones sin almacenarlas en los resultados de las coincidencias.
2. **Aplicación de Cuantificadores**: Facilitan la aplicación de cuantificadores a subexpresiones agrupadas sin capturar los resultados.

### Ejemplos en JavaScript

1. **Búsqueda Simple con Grupo No Capturador**
   
   ```javascript
   let text = "apple, orange, and banana";
   let regex = /(?:apple|banana)/g;
   console.log(text.match(regex)); // ["apple", "banana"]
   ```
   
    Aquí, `(?:apple|banana)` busca las palabras "apple" o "banana" en el texto, pero no captura las coincidencias en un grupo.

2. **Uso de Cuantificadores con Grupo No Capturador**
   
   ```javascript
   let text = "aaaabbbb";
   let regex = /(?:a{2,3}){2}/;
   console.log(text.match(regex)); // ["aaaa"]
   ```
   
    Aquí, `(?:a{2,3}){2}` busca dos repeticiones de "a" que aparezcan 2 o 3 veces consecutivamente. El grupo no capturador permite agrupar `a{2,3}` y aplicar `{2}` sin capturar el grupo.

3. **Comparación con Grupos Capturadores**
   
   ```javascript
   let text = "apple, orange, and banana";
   let regexCapturador = /(apple|banana)/g;
   let regexNoCapturador = /(?:apple|banana)/g;
   
   console.log(text.match(regexCapturador)); // ["apple", "banana"]
   console.log(text.match(regexNoCapturador)); // ["apple", "banana"]
   ```
   
    La salida es la misma en ambos casos porque `match` solo devuelve las coincidencias encontradas. Sin embargo, si utilizas `exec`, verás la diferencia en la captura de grupos:
   
   ```javascript
   let regexCapturador = /(apple|banana)/g;
   let result = regexCapturador.exec(text);
   console.log(result); // ["apple", "apple"]
   
   let regexNoCapturador = /(?:apple|banana)/g;
   let resultNoCapturador = regexNoCapturador.exec(text);
   console.log(resultNoCapturador); // ["apple"]
   ```
   
    Con el grupo capturador, `result[1]` contiene la coincidencia del grupo. Con el grupo no capturador, no hay `result[1]`.

4. **Uso en Reemplazos**
   
   ```javascript
   let text = "apple, orange, and banana";
   let regex = /(?:apple|banana)/g;
   let result = text.replace(regex, "fruit");
   console.log(result); // "fruit, orange, and fruit"
   ```
   
    Aquí, `(?:apple|banana)` permite reemplazar "apple" o "banana" por "fruit" sin capturar los grupos en el proceso.

### Ventajas de Usar Grupos No Capturadores

- **Rendimiento**: Reducen la carga de captura, lo que puede mejorar el rendimiento en expresiones regulares complejas.
- **Claridad**: Mejoran la legibilidad del código al indicar que ciertas partes de la expresión se agrupan solo por razones de lógica o cuantificación, no para captura.

# Grupos Capturadores por Índice

Los grupos capturadores por índice se crean utilizando paréntesis `(...)` en una expresión regular. Cada vez que utilizas paréntesis para agrupar parte de una expresión, creas un grupo capturador, y las coincidencias de estos grupos se pueden acceder mediante índices.

## Ejemplos en JavaScript

1. **Capturar Subcadenas**
   
   ```javascript
   let text = "My phone number is 123-456-7890.";
   let regex = /(\d{3})-(\d{3})-(\d{4})/;
   let match = text.match(regex);
   
   console.log(match[0]); // "123-456-7890" (la coincidencia completa)
   console.log(match[1]); // "123" (primer grupo capturador)
   console.log(match[2]); // "456" (segundo grupo capturador)
   console.log(match[3]); // "7890" (tercer grupo capturador)
   ```
   
    En este ejemplo, los paréntesis crean tres grupos capturadores, cada uno accesible por su índice.

2. **Reemplazar Usando Grupos Capturadores**
   
   ```javascript
   let text = "John Doe";
   let regex = /(\w+)\s(\w+)/;
   let result = text.replace(regex, "$2, $1");
   console.log(result); // "Doe, John"
   ```
   
    Aquí, `(\w+)\s(\w+)` captura dos palabras, y en la operación de reemplazo, usamos `$1` y `$2` para invertir el orden de las palabras.

# Grupos Capturadores Nombrados

Los grupos capturadores nombrados permiten asignar nombres a los grupos en lugar de solo índices. Esto puede hacer que las expresiones regulares sean más legibles y que el acceso a las coincidencias sea más claro.

### Sintaxis

- **Grupo Capturador Nombrado**: `(?<nombre> ...)`

## Ejemplos en JavaScript

1. **Capturar Subcadenas con Nombres**
   
   ```javascript
   let text = "My phone number is 123-456-7890.";
   let regex = /(?<areaCode>\d{3})-(?<exchangeCode>\d{3})-(?<lineNumber>\d{4})/;
   let match = text.match(regex);
   
   console.log(match.groups.areaCode); // "123"
   console.log(match.groups.exchangeCode); // "456"
   console.log(match.groups.lineNumber); // "7890"
   ```
   
    En este ejemplo, los grupos capturadores tienen nombres como `areaCode`, `exchangeCode`, y `lineNumber`, lo que hace que sea más fácil entender a qué se refiere cada grupo.

2. **Reemplazar Usando Grupos Capturadores Nombrados**
   
   ```javascript
   let text = "John Doe";
   let regex = /(?<firstName>\w+)\s(?<lastName>\w+)/;
   let result = text.replace(regex, "$<lastName>, $<firstName>");
   console.log(result); // "Doe, John"
   ```
   
    Aquí, los grupos capturadores nombrados `firstName` y `lastName` se utilizan en la operación de reemplazo.

### Comparación entre Grupos Capturadores por Índice y Nombrados

#### Ventajas de los Grupos Capturadores Nombrados

- **Legibilidad**: Los nombres de los grupos hacen que las expresiones regulares sean más fáciles de leer y entender.
- **Acceso Claro a Coincidencias**: En lugar de recordar índices, puedes acceder a las coincidencias mediante nombres descriptivos.

#### Ejemplo Comparativo

- **Grupos Capturadores por Índice**
  
  ```javascript
  let text = "John Doe";
  let regex = /(\w+)\s(\w+)/;
  let match = text.match(regex);
  console.log(match[1]); // "John"
  console.log(match[2]); // "Doe"
  ```
- **Grupos Capturadores Nombrados**
  
  ```javascript
  let text = "John Doe";
  let regex = /(?<firstName>\w+)\s(?<lastName>\w+)/;
  let match = text.match(regex);
  console.log(match.groups.firstName); // "John"
  console.log(match.groups.lastName); // "Doe"
  ```

# **Referencias en Expresiones Regulares**

### 1. **Introducción a las Expresiones Regulares**
- Las **expresiones regulares** (regex o regexp) son patrones utilizados para hacer coincidencias dentro de cadenas de texto.
- Pueden buscar, extraer o manipular texto de una manera eficiente.
- Una de las funcionalidades más poderosas es la **referencia a grupos capturados**.

### 2. **Grupos Capturados**
- Un **grupo capturado** se define usando paréntesis `( )` en una expresión regular.
- Sirven para encapsular parte del patrón y hacer referencia a ellos más tarde.
  
#### **Ejemplo de grupo capturado:**

```javascript
const regex = /(foo)bar/;
const match = "foobar".match(regex);
console.log(match[1]);  // "foo"
```
En este ejemplo, el grupo `(foo)` captura el texto `"foo"`. La referencia es accesible en `match[1]`.

### 3. **Referencia hacia Atrás (\1, \2, etc.)**
- Dentro de la misma expresión regular, las referencias a **grupos capturados** se hacen con **`\1`, `\2`, ...`**.
- **`\1`** se refiere al primer grupo capturado, **`\2`** al segundo, y así sucesivamente.

#### **Uso de referencias hacia atrás:**

```javascript
const regex = /(\w+)\s\1/;  // El grupo \1 debe repetirse
const testString = "hello hello";
console.log(regex.test(testString));  // true
```

Aquí, la expresión busca dos palabras iguales seguidas (referencia hacia atrás). `"hello hello"` coincide porque la segunda palabra repite lo capturado por el primer grupo.

#### **Otro ejemplo:**
```javascript
const regex = /(\d{2})-(\d{2})-\1/;  // \1 referencia al primer grupo
const date = "12-34-12";  // Repite el primer grupo
console.log(regex.test(date));  // true
```
En este caso, `\1` hace referencia al primer grupo capturado, por lo que el formato debe ser `XX-XX-XX` donde las primeras y últimas dos cifras son iguales.

### 4. **Referencia en Reemplazo ($1, $2, etc.)**
- En la cadena de reemplazo, las referencias a grupos capturados se hacen con **`$1`, `$2`, ...`**.
- Sirven para reutilizar el texto capturado en el patrón dentro de la **nueva cadena** que generas con `replace()`.

#### **Ejemplo de referencia en reemplazo:**

```javascript
const input = "John Doe";
const result = input.replace(/(\w+) (\w+)/, '$2, $1');
console.log(result);  // "Doe, John"
```
Aquí, `$1` captura el primer nombre y `$2` el apellido. La referencia permite intercambiar el orden del nombre y apellido.

#### **Otro ejemplo:**
```javascript
const input = "123-456-7890";
const result = input.replace(/(\d{3})-(\d{3})-(\d{4})/, '($1) $2-$3');
console.log(result);  // "(123) 456-7890"
```
En este caso, los números capturados por los grupos son reutilizados para dar formato a un número de teléfono.

### 5. **Ejemplo Completo:**
Vamos a combinar ambas formas, referencias hacia atrás y en reemplazo, en un solo caso:

#### **Problema:**
Tienes un texto que contiene números duplicados y quieres reemplazarlos con un símbolo de repetición.

```javascript
const input = "La clave es 123-123 o 456-456";
const result = input.replace(/(\d{3})-\1/g, '$1 (repetido)');
console.log(result);  // "La clave es 123 (repetido) o 456 (repetido)"
```

1. **Patrón de búsqueda**: `(\d{3})-\1` busca tres dígitos (`\d{3}`) seguidos de un guion y los mismos tres dígitos (referencia hacia atrás `\1`).
2. **Reemplazo**: En la cadena de reemplazo, `$1` usa los tres dígitos capturados y añade "(repetido)" para indicar que se repiten.

### 6. **Resumen de Referencias**
- **`\1`, `\2`, etc.**: Se usan **dentro de la expresión regular** para hacer referencia a grupos capturados previamente (referencias hacia atrás).
- **`$1`, `$2`, etc.**: Se usan en **cadenas de reemplazo** con `replace()` para reutilizar las coincidencias de los grupos capturados.

### 7. **Conclusión**
Las referencias en expresiones regulares te permiten trabajar con coincidencias previas dentro del mismo patrón o en reemplazos, lo que las convierte en una herramienta poderosa para manipular texto.
