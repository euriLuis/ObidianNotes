# Eloquent
## Caps 1, 2, 3 y 4.
## Capitulo 1: [[#Valores]], Tipos y Operadores
### *Valores*

> Algunos valores son números, otros son fragmentos de texto, otros son funciones, y así sucesivamente.

*Tipos de valores*
	-undefined: representa la ausencia de un valor asignado, variable que ha sido declarada pero no ha sido asignada.
	-null: representa la usencia intencional de un valor nulo.
	number: representa números enteros como de punto flotante.
	incluye valores especiales como Infinity, -infinity y NaN
	-string: Representa cadenas de texto. Se pueden definir con comillas simples, dobles o invertidas (template literals)
	-Boolean: Representa un valor lógico: `true` o `false`

### Operadores
#### Aritméticos/binarios

>`+`: suma/concatenación de cadenas
`-`: resta
`*`: multiplicación
`/`: division
`%`: residuo o resto
 `**` : exponenciación

#### Operadores de asignación

>`=`:  asignación simple
`+=`: suma y asignación
`-=`: resta y asignación
`*=`: Multiplicación y asignación
`/=`: División y asignación
`%`=: Módulo y asignación
`**=`: Exponenciación y asignación

#### Operadores de Comparación

>`==`: Igualdad (compara solo el valor)
`===`: Igualdad estricta (compara valor y tipo)
`!=`: Desigualdad
`!==`: Desigualdad estricta (compara valor y tipo)
`>`: Mayor que
`<`: Menor que
`>=`: Mayor o igual que
`<=`: Menor o igual que

#### Operadores Lógicos

>`&&` AND lógico (devuelve `true` si ambos operandos son
verdaderos)
`||`: OR lógico (devuelve `true` si al menos uno de los
operandos es verdadero)
`!`: NOT lógico (invierte el valor booleano)
`??`: Devuelve el operando de la derecha si el operando
de la izquierda es `null` o `undefined`

#### Operadores de Incremento y Decremento

>`++`: Incremento
`--`: Decremento

#### Operador ternario

>`a ? b : c`, el resultado será b cuando a es verdadero
y c de lo contrario

#### Unarios

>`typeof`: produce una cadena que indica el tipo de valor que se le proporciona
`instanceof`: Devuelve `true` si el objeto es una instancia del constructor especificado

Conversión automática de tipos
number `*` string = NaN
string `-` number = number

### Cortocircuito de operadores
Los operadores logicos && y || Convertiran el valor del lado izquierdo a tipo Booleano para decidir que hacer
>El operador ||, por ejemplo, devolverá el valor de su izquierda cuando ese valor pueda convertirse en true y devolverá el valor de su derecha de lo contrario.

==Podemos utilizar esta funcionalidad como una forma de utilizar un valor prede terminado==.

El operador ?? se asemeja a ||, pero devuelve el valor de la derecha solo si el de la izquierda es null o undefined, no si es algún otro valor que se pueda convertir en false.
El operador && funciona de manera similar pero en sentido contrario. Cuando el valor a su izquierda es algo que se convierte en false, devuelve ese valor, y de lo contrario devuelve el valor de su derecha. Otra propiedad importante de estos dos operadores es que la parte de su derecha se evalúa solo cuando es necesario.

## Capitulo 2: Estructura del Programa

### Expresiones y declaraciones
Un fragmento de código que produce un valor es una *expresión*.

Para atrapar y retener valores JS proporciona una cosa llamada enlace o variable.
`let caught = 5 * 5;`
Después de que se haya definido un enlace su nombre se puede usar como una expresión. El valor de esa expresión es el valor que el enlace mantiene actualmente.
```js
let ten = 10;
console.log(ten * ten);
//100
```

Cuando un enlace apunta a un valor eso no significa que este atado a ese valor para siempre. El operador = se puede usar en cualquier momento en enlaces existentes para desconectarlos de su valor actual y  hacer que apunten a uno nuevo.
```js
let mood = "light";
console.log(mood);
// → light
mood = "dark";
console.log(mood);
// → dark
```

Los dígitos pueden ser parte de nombres de enlaces pero no pueden estar al inicio de estos.

### El entorno 
La colección de enlaces y sus variables que existen en un momento dado se llama *entorno*.

### Funciones
Una función es un fragmento de programa envuelto en un valor. Estos valores pueden ser aplicados para ejecutar el programa envuelto.
Las funcione pueden tener valores de retorno o efectos secundarios.

### Control de Flujo
Las sentencias se ejecutan de arriba  hacia abajo.
Para ejecutar uno u otro código se puede utilizar la ejecución condicional.

### Ejecución condicional.

La ejecución condicional se crea con la palabra clave if en JavaScript. En el caso simple, queremos que cierto código se ejecute si, y solo si, una cierta condición es verdadera. Por ejemplo, podríamos querer mostrar el cuadrado de la entrada solo si la entrada es realmente un número:
![[Captura de pantalla 2025-06-08 042017.png]]
```js
let elNumero = Number(prompt("Elige un número")); 

if (!Number.isNaN(elNumero)) { 
	console.log("Tu número es " + elNumero * elNumero); 
}
```

### Bucles While y DO
Esta forma de control de flujo se llama bucle es una manera de ejecutar un fragmento de código múltiples veces,

Un statement que comienza con la palabra clave while crea un bucle. La pal abra while va seguida de una expresión entre paréntesis y luego un enunciado, similar a if. El bucle sigue ejecutando ese enunciado mientras la expresión produzca un valor que se convierta en true al convertirse a Booleano.
```js
let result = 1; 
let counter = 0; 
while (counter < 10) { 
	result = result * 2; 
	counter = counter + 1; 
} 
console.log(result); 
// → 1024
```

Un bucle do es una estructura de control similar a un bucle while. La única diferencia radica en que un bucle do siempre ejecuta su cuerpo al menos una vez, y comienza a probar si debe detenerse solo después de esa primera ejecución.
```js
let tuNombre; 
do { 
	tuNombre = prompt("¿Quién eres?"); 
} while (!tuNombre); 
console.log("Hola " + tuNombre);
```

### Bucles for
Es una forma mas corta de representar el bucle, donde primero se crea una variable contador, luego un expresión que verifica si el contador ha alcanzado el final y el actualizador del contador.
```js
for (let numero = 0; numero <= 12; numero = numero + 2) {
	console.log(numero); 
} 
// → 0 
// → 2 
// … etcétera
```

La instrucción `brake` tiene el efecto de salir inmediatamente de un bucle,
```js
for (let actual = 20; ; actual = actual + 1) { 
	if (actual % 7 == 0) { 
		console.log(actual); 
		break; 
	} 
} 
// → 21
```

La palabra clave `continue` es similar a break en que influye en el progreso de un bucle.
Cuando se encuentra `continue` en el cuerpo de un bucle, el control salta fuera del cuerpo y continúa con la siguiente iteración del bucle.

### Despachar un valor con switch
switch que está destinada a expresar dicho “despacho” de una manera más directa.
```JS
switch (prompt("¿Cómo está el clima?")) { 
	case "lluvioso": 
	console.log("Recuerda llevar un paraguas."); 
	break; 
	case "soleado": 
	console.log("Vístete ligero."); 
	case "nublado": console.log("Sal al exterior."); 
	break; 
	default: console.log("¡Tipo de clima desconocido!"); 
	break; 
}
```

## Capitulo 3: Funciones.
### Definir una función.
Una definición de función es una vinculación regular donde el valor de la vinculación es una función.
```js
const square = function(x) { 
	return x * x; 
}; 
console.log(square(12)); 
// → 144
```

