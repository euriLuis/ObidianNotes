# Capitulo 9: Expresiones regulares.
Las expresiones regulares son una forma de describir patrones en datos de cadena.
## Creando una expresión regular.
Puede ser construido con el constructor RegExp o escrito como un valor literal al encerrar un patrón entre caracteres de barra diagonal (/).

El constructor toma como primer argumento un string o una expresión regular como primer parámetro y un string como segundo parámetro opcional para las banderas [[#Flags]]
```js
let re1 = new RegExp("abc");
     //or
let re2 = /abc/;
     //or
let re3 = new RegExp(/abc/, "i");
```

Se debe poner una barra invertida \ antes de cualquier diagonal / que queremos sea parte de la expresión.
Tambien se deben de usar antes de algunos caracteres que tienen significado especial como el signo de interrogación y el signo de suma.
```js
let aPlus = /A\+/;
```

## Pruebas de coincidencias.
`RegExp.test()` - si se  le pasa una cadena este devolverá un booleano si coincide con el patron.
```js
console.log(/abc/.test("abcde"));
//true
console.log(/abc/.test("abxde")
```

## Conjunto de caracteres.
Poner parte de la expresión regular entre corchetes hace que esa parte de la expresión coincida con cualquiera de los caracteres entre los corchetes.

Ambas expresiones hacen coincidir todas las cadenas que contienen un digito.
```js
console.log(/[0123456789]/.test("in 1992"));
//true
console.log(/[0-9]/.test("in 1992"));
//true
```

Dentro de corchetes un guion (-) se puede utilizar para indicar un rango entre caracteres.

Para invertir un conjunto de caracteres o sea expresar que se desea hacer coincidir cualquier caracter excepto lo que están en el conjunto se utiliza el caracter circunflejo (^)
```js
let nonBinary = /[^01]/
console.log(nonBinary.test("1100100010100110"));
//false
console.log(nonBinary.test("0111010112101001")); 
// → true
```

## Repetir partes de un patron.
Cuando colocas un signo más (+) después de algo en una expresión regular, indica que el elemento puede repetirse más de una vez. Así, /\d+/ hace coincidir uno o más caracteres de dígitos.
El asterisco  (\*)  tiene un significado similar pero también permite que el patrón coincida cero veces
```js
console.log(/'\d+'/.test("'123'"));
// → true 
console.log(/'\d+'/.test("''")); 
// → false 
console.log(/'\d*'/.test("'123'"));
// → true
console.log(/'\d*'/.test("''")); 
// → true
```

Un signo de interrogación hace que una parte de un patrón sea opcional, lo que significa que puede ocurrir cero veces o una vez. 
En el siguiente ejemplo, se permite que el carácter /u/ ocurra, pero el patrón también coincide cuando falta.
```js
let neighbor = /neighbou?r/; 
console.log(neighbor.test("neighbour")); 
// → true 
console.log(neighbor.test("neighbor"));
// → true
```

Para indicar que un patrón debe ocurrir un número preciso de veces, utiliza llaves. Colocar {4} después de un elemento, por ejemplo, requiere que ocurra exactamente cuatro veces.
También es posible especificar un rango de esta manera: {2,4} significa que el elemento debe ocurrir al menos dos veces y como máximo cuatro veces.
También puedes especificar rangos abiertos al utilizar llaves omitiendo el número después de la coma. 
Así, {5,} significa cinco o más veces.

## Agrupación de sobrexpresiones.
Para utilizar operadores como * o + en mas de un elemento a la vez se deben utilizar paréntesis ()
```js
let cartoonCrying = /boo+(hoo+)+/i; console.log(cartoonCrying.test("Boohoooohoohooo")); // → true
```

La */i/* al final de la expresión en el ejemplo hace que esta expresión regular ignore mayúsculas y minúsculas

## Coincidencias y grupos.
`RegExp.exec()` este método devolverá null si no se encontró ninguna coincidencia y devolverá un array con información sobre la coincidencia en caso de que exista la coincidencia.
-[0] Retorna en el primer elemento del array todas las partes del string que cumplen con la expresión.
-[1], ...[n] retorna las subcadenas que han sido encontradas.
-index retorna el numero de cadenas que han coincidido
-input retorna la cadena original
```js
let coincidencia = /\d+/.exec("uno dos 100"); console.log(coincidencia); 
// → ["100"] 
console.log(coincidencia.index);
// → 8
```

##  La Clase Date
Clase estándar para representar fechas o mas bien puntos en el tiempo.
Al crear un objeto con esta clase se obtendrá la fecha y horas actuales.
```js
console.log(new Date()); 
// → Fri Feb 02 2024 18:03:06 GMT+0100 (CET)
```

Tambien se  puede crear un objeto para una fecha y hora específicos. 
```js
console.log(new Date(2009, 11, 9)); 
// → Mié Dec 09 2009 00:00:00 GMT+0100 (CET) 
console.log(new Date(2009, 11, 9, 12, 59, 59, 999)); 
// → Mié Dec 09 2009 12:59:59 GMT+0100 (CET)
```

>JavaScript utiliza una convención donde los números de mes empiezan en cero (por lo que diciembre es 11), pero los números de día comienzan en uno.
>Los últimos cuatro argumentos (horas, minutos, segundos y milisegundos) son opcionales y se consideran cero cuando no se proporcionan.

Si se proporciona un único argumento, este se tomara como un recuento de milisegundos.
Se puede obtener el recuento de milisegundos creando un nuevo objeto Date y llamando el método `getTime` o llamando la función `Date.now` 

Los objetos de fecha proporcionan métodos como `getFullYear`, `getMonth`, `getDate`, `getHours`, `getMinutes` y `getSeconds` para extraer sus componentes.
Poniendo paréntesis alrededor de las partes de la expresión que nos interesan, podemos crear un objeto de fecha a partir de una cadena.
```js
function getDate(string) {
	let [_, month, day, year] = 
		/(\d{1,2})-(\d{1,2})-(\d{4})/.exec(string);
	return new Date(year, month - 1, day);
} 
console.log(getDate("1-30-2003")); 
// → Jue Ene 30 2003 00:00:00 GMT+0100 (CET)
```
## Limites y anticipación.
`getTime` también extraerá una fecha de la cadena "100-1-30000" una coincidencia puede ocurrir en cualquier parte de la cadena.
Por lo que hay que agregar los marcadores ^ y $.
`/^\d +$/` coincide con una cadena que consiste completamente de uno o más dígitos,` /^!/` coincide con cualquier cadena que comience con un signo de exclamación.
La notación (?! ) expresa un mirar adelante negativo. Esto solo coincide si el patrón entre paréntesis no coincide, lo que hace que el segundo ejemplo solo coincida con caracteres “a” que no tienen un espacio después de ellos.
## Patrones de elección
El carácter de barra vertical (|) denota una elección entre el patrón a su izquierda y el patrón a su derecha, si el primer patron , los paréntesis se aplican para delimitar la parte del patron a la que se le va a aplicar el operador de barra
```js
let animalCount = /\d+ (pig|cow|chicken)s?/; console.log(animalCount.test("15 pigs")); 
// → true 
onsole.log(animalCount.test("15 pugs")); 
// → false
```

## La mecánica de la coincidencia.
El motor de expresiones regulares busca una coincidencia en tu cadena tratando de ajustar primero la expresión desde el comienzo de la cadena, luego desde el segundo carácter, y así sucesivamente, hasta que encuentra una coincidencia o llega al final de la cadena. 
Devolverá la primera coincidencia que encuentre o fracasará en encontrar cualquier coincidencia.

![[Captura de pantalla_26-5-2025_1244_.jpeg]]

## Retroceso
La expresión regular /^([01]+b|[\da-f]+h|\d+)$/ coincide ya sea con un número binario seguido de una b, un número hexadecimal (es decir, base 16, con las letras a a f representando los dígitos del 10 al 15) seguido de un h, o un número decimal regular sin un carácter de sufijo. 
Este es el diagrama correspondiente:
![[Captura de pantalla_26-5-2025_1642_.jpeg]]

Si varias ramas podrían coincidir potencialmente con una cadena, solo se usa la primera (ordenada por dónde aparecen las ramas en la expresión regular).
Al ingresar a una rama, recuera la posición actual para poder retroceder y probar otra rama si la actual no funciona.

## Método `replace`
Los valores de cadena tienen un método `replace` que se puede utilizar para reemplazar parte de la cadena con otra cadena.
El primer argumento también puede ser una expresión regular, en cuyo caso se reemplaza la primera coincidencia de la expresión regular.
Cuando se coloca /g después de la expresión regular todas las coincidencias serán remplazadas
```js
console.log("papa".replace("p", "m")); 
// → mapa
console.log("Borobudur".replace(/[ou]/, "a"));
// → Barobudur
console.log("Borobudur".replace(/[ou]/g, "a")); 
// → Barabadar
```

Esto se puede usar para invertir el orden de un patron. 
Los $1 y $2 en la cadena de reemplazo se refieren a los grupos entre paréntesis en el patrón.
Es posible llamar una funcion en lugar de una cadena como remplazo"segundo argumento"
```js
console.log( "Liskov, Barbara\nMcCarthy, John\nMilner, Robin" .replace(/(\p{L}+), (\p{L}+)/gu, "$2 $1"));
// → Barbara Liskov
// John McCarthy 
// Robin Milner

let stock = "1 limón, 2 repollos y 101 huevos"; 
function menosUno(match, cantidad, unidad) { 
	cantidad = Number(cantidad) - 1;
	if (cantidad == 1) { // solo queda uno, se elimina la 's'
		unidad = unidad.slice(0, unidad.length - 1);
	} else if (cantidad == 0) { 
		cantidad = "ningún"; 
	} 
	return cantidad + " " + unidad; 
} 

console.log(stock.replace(/(\d+) (\p{L}+)/gu, menosUno));
// → ningún limón, 1 repollo y 100 huevos
```

## Avaricia
Los operadores de repetición (+, \*, ?, y {}) son avariciosos coinciden con todo lo que pueden y retroceden desde allí,  un signo de interrogación después de ellos (+?, \*?, ??, {}?), se vuelven no avariciosos y comienzan coincidiendo con la menor cantidad posible, coincidiendo más solo cuando el patrón restante no encaja con la coincidencia más pequeña.

## Creación dinámica de objetos RegExp
Puedes construir una cadena y usar el constructor RegExp en ello
```js
let name = "harry";
let regexp = new RegExp("(^|\\s)" + name + "($|\\s)", "gi"); 
console.log(regexp.test("Harry es un personaje dudoso."));
// → true
```

En caso de que se quiera construir con caracteres especiales se puede agregar barras invertidas
```js
let name = "dea+hl[]rd";
let escaped = name.replace(/[\\[.+*?(){|^$]/g, "\\$&");
let regexp = new RegExp("(^|\\s)" + escaped + "($|\\s)", "gi"); 
let text = "Este chico dea+hl[]rd es súper molesto."; console.log(regexp.test(text)); 
// → true
```

## Método Search
Devuelve el primer índice en el que se encontró la expresión, o -1 cuando no se encontró.
```js
console.log(" palabra".search(/\S/)); // → 2 
console.log(" ".search(/\S/)); // → -1
```

## Propiedad lastIndex.
Controla en circunstancias limitadas a partir de donde comienza la coincidencia.
Estas circunstancias implican que la expresion regular debe tener la opcion global(g) o pegajosa (y) activada y la coincidencia debe ocurrir a traves del metodo exec.
```js
let pattern = /y/g; 
pattern.lastIndex = 3; 
let match = pattern.exec("xyzzy"); console.log(match.index); 
// → 4 
console.log(pattern.lastIndex); 
// → 5
```

La diferencia entre las opciones global y sticky es que, cuando se habilita sticky, la coincidencia solo se producirá si comienza directamente en lastIndex , mientras que con global se buscará una posición donde pueda comenzar una coincidencia.

Otro efecto interesante de la opción global es que cambia la forma en que funciona el método `match` en las cadenas. Cuando se llama con una expresión global, en lugar de devolver una matriz similar a la devuelta por exec, match encontrará todas las coincidencias del patrón en la cadena y devolverá una matriz que contiene las cadenas coincidentes
## Obteniendo todas las coincidencias.
Método `matchAll` encuentra todas las coincidencias, la expresión regular que se proporciona debe tener todas las coincidencias.
Este metodo devuelve un array de arrays 
```js
let input = "Una cadena con 3 números... 42 y 88.";
let matches = input.matchAll(/\d+/g);
for (let match of matches) {
	console.log("Encontrado", match[0], "en", match.index);
} 
// → Encontrado 3 en 14 
// Encontrado 42 en 33
// Encontrado 88 en 40
```

La expresión regular que se le proporciona debe tener `g` habilitado

## Unidades de código y caracteres
Los caracteres que están compuestos por dos unidades de código se comportan de manera extraña, por lo que debe agregarse al final la bandera u{Unicode}
## <span style="color:rgb(255, 0, 0)">Ejercicios</span>

Regexp golf
Para cada uno de los siguientes elementos, escribe una expresión regular para comprobar si el patrón dado ocurre en una cadena.

1. car y cat
```js
regex = /^ca[rt]$/;
```
2. pop y prop
```js
regex = /p(r?)op/;
```
3. ferret, ferry y ferrari
```js
regex = /ferr[et|y|ari]/;
```
4. Cualquier palabra que termine en ious
```js
regex = /(\p{L}+)ious/u | /(\w+)ious/;

```
5. Un carácter de espacio en blanco seguido de un punto, coma, dos puntos o punto y coma
```js
regex = /\s[.,:;]/; 
```
6. Una palabra con más de seis letras
```js
regex = /p{L}{7}/u
```

7. Una palabra sin la letra e (o E)
```js
regex = /[^e]/i
```

8. Estilo de comillas
Quieres reemplazar todas las comillas de diálogo con comillas dobles, manteniendo las comillas simples utilizadas en contracciones como aren’t
```js
str.replace(/(^|\P{L})'|'(\P{L}|$)/gu, '$1"$2');
```




----
## Recursos.
### Elementos
```js
/\d/     //Cualquier carácter dígito 
/\D/     //Un carácter que no es un dígito
/\w/     //Un carácter alfanumérico (“carácter de palabra”) 
/\W/     //Un carácter no alfanumérico 
/\s/     //Cualquier carácter de espacio en blanco   
/\S/     //Un carácter que no es de espacio en blanco
/./      //Cualquier carácter excepto saltos de línea
/x+/     //Una o más ocurrencias del patrón x
/x+?/    //Una o más ocurrencias, perezoso
/x*/     //Cero o más ocurrencias
/x{2,4}/ //Dos a cuatro ocurrencias, con solo un valor este seria el minimo
/x?/     //Cero o una ocurrencia
/[abc]/  //Cualquier carácter de un conjunto de caracteres
/[0-9]/  //Cualquier carácter en un rango de caracteres
/[^abc]/ //Cualquier carácter que no esté en un conjunto de caracteres
/[^]/    //Cualquier cracter que no este en un espacio vacio
i        //se coloca al final para ignorar mayusculas o minusculas
g        //la g despues de la regExp indica que deben ser remplazadas todas las coincidencias
/(abc)/  //Un grupo 
/abc/    //Una secuencia de caracteres
/a|b|c/  //Cualquiera de varias combinaciones de patrones
/\p{L}/u //Cualquier carácter de letra 
/^/      //Inicio de entrada 
/$/      //Fin de entrada
/(?=a)/  //Una prueba de vistazo hacia adelante
/|/      //denota una eleccion entre el patron de su izquierda y el de la derecha.
?        //convirte simbolos avariciosos en no avariciosos
```

### Flags

| Flag | Description                                                                                   | Corresponding property |
| ---- | --------------------------------------------------------------------------------------------- | ---------------------- |
| `d`  | Generate indices for substring matches.                                                       | `hasIndices`           |
| `g`  | Global search.                                                                                | `global`               |
| `i`  | Case-insensitive search.                                                                      | `ignoreCase`           |
| `m`  | Allows `^` and `$` to match next to newline characters.                                       | `multiline`            |
| `s`  | Allows `.` to match newline characters.                                                       | `dotAll`               |
| `u`  | "Unicode"; treat a pattern as a sequence of Unicode code points.                              | `unicode`              |
| `v`  | An upgrade to the `u` mode with more Unicode features.                                        | `unicodeSets`          |
| `y`  | Perform a "sticky" search that matches starting at the current position in the target string. | `sticky`               |

### Métodos
```js
RegExp.test("str");
//retorna true o false si coincide la cadena con la regExp
RegExp.exec("str");
//busca coincidencia entre la expresion y el sring y retorna null o un array, en este array el primer elemento corresponde
string.replace(regExp, remplazo);
//remplaza la coincidencia que se encuentre en el estring segun el primer argumento que se le de por el segundo argumento. El remplazo puede ser un string o una funcion llamada para cada coincidencia
string.search(regExp)
//primer index en que se encontro la coincidencia o -1 si no se encontro.
string.matchAll(regExp)
//encuentra todas las coincidencias de una expresion regular en una cadena y devuelve una matriz de matrices de coincidencias
```