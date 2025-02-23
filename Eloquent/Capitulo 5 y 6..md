# Eloquent
## Cap [[#Capitulo 5 Funciones de Orden Superior|5]] y [[#Capitulo 6 La Vida Secreta de los Objetos.|6]].
## Capitulo 5: Funciones de Orden Superior
#### Abstracción
- Las abstracciones nos brindan la capacidad de hablar sobre prob-
lemas a un nivel superior (o más abstracto), sin distraernos con detalles no
interesantes.
>  Las funciones que operan en otras funciones, ya sea tomandolas como argumentos o devolviéndolas, se llaman **funciones de orden superior.**


**forEach**
*itera sobre cada elemento de un array y realza una accion sobre este*
```js
["A", "B"].forEach(l => console.log(l));
// → A
// → B
```
****
**Filter**
*Filtra los elementos de una matriz que no pasan una prueba*
```js
function filter(array, test) {
    let passed = [];
    for (let element of array) {
        if (test(element)) {
	        passed.push(element);
		}
	}
	return passed;
}

console.log(filter(SCRIPTS, script => script.living));
// → [{name: "Adlam", …}, …]
```
****
**map**
*El método map transforma una matriz aplicando una función a todos sus elementos y construyendo una nueva matriz a partir de los valores devueltos.*
```js
function map(array, transform) {
	let mapped = [];
	for (let element of array) {
		mapped.push(transform(element));
	}
	return mapped;
}

let rtlScripts = SCRIPTS.filter(s => s.direction == "rtl");

console.log(map(rtlScripts, s => s.name));
// → ["Adlam", "Arabic", "Imperial Aramaic", …]
```
****
**reduce**
*Construye un valor tomando repetidamente un único elemento del array y combinándolo con el valor actual.*
*Los parámetros de reduce son, además del array, una función de combinación y un valor inicial*
```js
function reduce(array, combine, start) {
	let current = start;
	for (let element of array) {
		current = combine(current, element);
	}
	return current;
}

console.log(reduce([1, 2, 3, 4], (a, b) => a + b, 0));
// → 10
```
**Uso normal**
```js
let arr = [1, 2, 3, 4];
console.log(arr.reduce((a, b) => a + b)); //10
```
****

*Las abstracciones proporcionadas por estas funciones brillan realmente cuando necesitas componer operaciones.* 
****

**some**
*El método some comprueba si algún elemento coincide con una función de predicado dada.*
```js
const numeros = [3, 7, 15, 2];
const hayMayoresA10 = numeros.some(num => num > 10); console.log(hayMayoresA10); // true (porque 15 es mayor a 10)
```
****

**find** 
*recorre los elementos en el array y devuelve el primero para el cual una función devuelve true. Devuelve undefined cuando no se encuentra dicho elemento.*
```js
const numeros = [3, 7, 15, 2, 20];
const primerMayorA10 = numeros.find(num => num > 10); console.log(primerMayorA10); // 15 (porque es el primer número mayor a 10)
```
****
#### Ejercicios
**1 Aplanamiento**
> Utiliza el método reduce en combinación con el método concat para “aplanar” un array de arrays en un único array que contenga todos los elementos de los arrays originales.
```js
let arr = [[4, 5, 8], [9, 8, 0], [7, 8, 6]];

let aplanadora = (arr) => arr.reduce((a, b) => a.concat(b));

console.log(aplanadora(arr)); // [4, 5, 8, 9, 8, 0, 7, 8, 6]
```

**3 Everything**
> Implementa every como una función que recibe un array y una función de predicado como parámetros. Escribe dos versiones, una usando un bucle y otra usando el método some.
```js
//bucle
function every(arr, func){
	for(let element of arr) {
		if(func(!element)){
			return false;
		}
	}
	return true;
}

//some
function everY(arr, func){
	if (arr.some(a => func(a))) {
		return false;
	} else {
		return true;
	}
}
```

****

## Capitulo 6: La Vida Secreta de los Objetos.

>La idea principal en la programación orientada a objetos es utilizar objetos, o más bien tipos de objetos, como la unidad de organización del programa. Configurar un programa como una serie de tipos de objetos estrictamente separados proporciona una forma de pensar en su estructura y, por lo tanto, de imponer algún tipo de disciplina para evitar que todo se entrelace.

#### Métodos
*En JavaScript, los métodos no son más que propiedades que contienen valores de función. Este es un método simple:*
```js
function speak(line) { 
	console.log(`El conejo ${this.type} dice '${line}'`); 
} 
let conejoBlanco = {type: "blanco", speak}; 
let conejoHambriento = {type: "hambriento", speak}; conejoBlanco.speak("Oh, mi pelaje y mis bigotes"); // → El conejo blanco dice 'Oh, mi pelaje y mis bigotes'
conejoHambriento.speak("¿Tienes zanahorias?"); // → El conejo hambriento dice '¿Tienes zanahorias?'
```

>Cuando una función es llamada como método—buscada como propiedad y llamada inmediatamente, como en objeto.método()—la vinculación llamada this en su cuerpo apunta automáticamente al objeto en el que fue llamada.
>No puedes hacer referencia al this del ámbito.
>Las funciones flecha son diferentes—no vinculan su propio this pero pueden ver la vinculación this del ámbito que las rodea.

```js
let buscador = {
	find(array) { 
		return array.some(v => v == this.value);
	}, 
	value: 5 
}; 
console.log(buscador.find([4, 5])); // → true
```

#### Prototipos


