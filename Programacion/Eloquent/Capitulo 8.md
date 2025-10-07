# Bugs y Errores
Las fallas en los programas se llaman bugs
## Modo Estricto
JS puedes ser un poco mas estricto al habilitar el modo estricto, esto se hace con el string *"use strict"* en el archivo o la función.
```js
function canYouSpotTheProblem() {
	"use strict"; 
	for (counter = 0; counter < 10; counter++) { 
		console.log("Happy happy"); 
	} 
} 
canYouSpotTheProblem();
// → ReferenceError: counter is not defined
```

Sin el modo estricto al crear un loop for sin declarar con let la variable esta se escribirá en el ámbito global, en caso de ya estar declarada se ira sobrescribiendo, lo que no sucederá en el modo estricto.
Al igual que al llamar a una función constructora sin new delante esto no arrojara error pero en el modo estricto si.
## Tipos 
Saber el tipo de valor que entra a un enlace y expresiones suele ser util, JS solo considera los tipos al ejecutar el programa y en muchas ocasiones intenta convertir al tipo que espera.
Cuando los tipos de un programa son conocidos, es posible que la computadora los verifique por ti, señalando errores antes de que se ejecute el programa.
Hay varios dialectos de JavaScript que añaden tipos al lenguaje y los verifican. El más popular se llama *TypeScript.*
## <span style="color:rgb(116, 146, 205)">Pruebas</span>
Las pruebas automatizadas son el proceso de escribir un programa que prueba otro programa.
Las pruebas suelen tomar la forma de pequeños programas etiquetados que verifican algún aspecto de tu código.
```js
function test(label, body) { 
	if (!body()) console.log(`Fallo: ${label}`);
} 

test("convertir texto latino a mayúsculas", () => { 
	return "hello".toUpperCase() == "HELLO"; 
});
test("convertir texto griego a mayúsculas", () => {
	return "Χαίρετε".toUpperCase() == "ΧΑΊΡΕΤΕ";
}); 
test("no convertir caracteres sin caso", () => {
	return "ڑغ׍৹৫".toUpperCase() == "ڑغ׍৹৫"; 
});
```
Existe software que ayuda a construir y ejecutar colecciones de pruebas *Suites de pruebas* al proporcionar un lenguaje en forma de funciones y métodos adecuado para expresar pruebas y al producir información informativa cuando una prueba falla.

## <span style="color:rgb(116, 146, 205)">Depuración</span>
Debes resistir la tentación de empezar a hacer cambios aleatorios en el código para ver si eso lo mejora. En cambio, piensa. Analiza lo que está sucediendo y elabora una teoría sobre por qué podría estar ocurriendo.

> Colocar algunas llamadas `console.log()` estratégicas en el programa es una buena manera de obtener información adicional sobre lo que está haciendo el programa.

Los navegadores vienen con la capacidad de establecer un punto de interrupción en una línea específica de tu código. Cuando la ejecución del programa llega a una línea con un punto de interrupción, se pausa y puedes inspeccionar los valores de las asignaciones en ese punto.

## <span style="color:rgb(116, 146, 205)">Excepciones</span>
Cuando una función no puede proceder normalmente a menudo queremos detener lo que estábamos haciendo e ir directamente a un lugar que sepa como manejar el problema. Es lo que hace el manejo de excepciones.

La palabra clave *throw* se utiliza para lanzar una excepción.
La captura de una excepción se realiza envolviendo un trozo de código en un bloque *try*, seguido de la palabra clave *catch*.
```js
function promptDirection(question) { 
	let result = prompt(question);
	if (result.toLowerCase() == "left") return "L"; 
	if (result.toLowerCase() == "right") return "R"; 
	throw new Error("Dirección inválida: " + result); 
} 

function look() {
	if (promptDirection("¿Hacia dónde?") == "L") { 
		return "una casa"; 
	} else { 
		return "dos osos enojados"; 
	} 
} 

try { 
	console.log("Ves", look()); 
} catch (error) { 
	console.log("Algo salió mal: " + error);   
}
```

Cuando el código en el bloque *try* provoca que se lance una excepción, se evalúa el bloque *catch*, con el nombre entre paréntesis vinculado al valor de la excepción. Después de que el bloque catch finalice, o si el bloque *try* finaliza sin problemas, el programa continúa debajo de toda la instrucción *try/catch*.

## <span style="color:rgb(116, 146, 205)">Limpiando después de excepciones</span>
El efecto de una excepción es otro tipo de flujo de control. Cada acción que pueda causar una excepción  puede hacer que el control salga repetidamente de tu código. 
Por eso existe otra característica que tienen las instrucciones *try*. Pueden estar seguidas de un bloque *finally* en lugar o además de un bloque *catch*. Un bloque *finally* dice “sin importar qué suceda, ejecuta este código después de intentar ejecutar el código en el bloque *try.*”
```js
const accounts = { 
	a: 100, 
	b: 0, 
	c: 20 
};

function getAccount() { 
	let accountName = prompt("Ingresa el nombre de una cuenta"); 
	if (!Object.hasOwn(accounts, accountName)) { 
		throw new Error(`No existe esa cuenta: ${accountName}`); 
	} 
	return accountName; 
}

function transfer(from, amount) { 
	if (accounts[from] < amount) return;
	let progress = 0; 
	try { 
		accounts[from] -= amount; 
		progress = 1; 
		accounts[getAccount()] += amount; 
		progress = 2; 
	} finally { 
		if (progress == 1) { 
			accounts[from] += amount; 
		}
	} 
}
```

## <SPAN style="color:rgb(116, 146, 205)">Captura selectiva
</SPAN>
Cuando una excepción llega hasta el final sin ser capturada, es manejada por el entorno. 
Para problemas que se espera que ocurran durante el uso rutinario, fallar con una excepción no manejada es una estrategia terrible. 
Cuando se entra en un cuerpo catch todo lo que sabemos es que algo en nuestro cuerpo try causo una excepción. Pero no sabemos que lo hizo ni que excepción causo. 
```js
for (;;) { 
	try { 
		let dir = promptDirection("¿Dónde?"); // ← ¡Error de tipeo! 
		console.log("Elegiste ", dir); 
		break;
	} catch (e) { 
		console.log("Dirección no válida. Inténtalo de nuevo."); 
	}
}
```

Como regla general, no captures excepciones de manera general a menos que sea con el propósito de “enviarlas” a algún lugar, por ejemplo, a través de la red para informar a otro sistema que nuestro programa se bloqueó.

Podemos capturar un tipo específico de excepción verificando en el bloque catch si la excepción que recibimos es la que nos interesa y relanzándola en caso contrario.
Podemos definir un nuevo tipo de error y usando instanceof para identificarlo.
```js
class InputError extends Error {}; 

function promptDirection(question) { 
	let result = prompt(question); 
	if (result.toLowerCase() == "izquierda") return "I"; 
	if (result.toLowerCase() == "derecha") return "D"; 
	throw new InputError("Dirección no válida: " + result); 
}
```

Los objetos InputError se comportan como objetos Error, excepto que tienen una clase diferente mediante la cual podemos reconocerlos.
```js
for (;;) { 
	try { 
		let dir = promptDirection("¿Dónde?");
		console.log("Elegiste ", dir); 
		break; 
	} catch (e) { 
		if (e instanceof InputError) { 
			console.log("Dirección no válida. Inténtalo de nuevo."); 
		} else { 
			throw e; 
		} 
	} 
}
```
Esto capturará solo instancias de InputError y permitirá que pasen excepciones no relacionadas.

## Afirmaciones.
Son verificaciones dentro de un programa que aseguran que algo es como se supone que debe ser. Se utilizan no para manejar situaciones que pueden surgir en a operación normal si no para encontrar errores de programación.
```js
function primerElemento(array) { 
	if (array.length == 0) { 
		throw new Error("primerElemento llamado con []"); 
	} 
	return array[0]; 
}
```

En lugar de devolver silenciosamente undefined, esto hará que tu programa falle ruidosamente tan pronto como lo uses incorrectamente.
## <span style="color:rgb(116, 146, 205)">Ejercicios</span>
Tienes una función primitiveMultiply que en el 20 por ciento de los casos multiplica dos números y en el otro 80 por ciento arroja una excepción del tipo MultiplicatorUnitFailure.
Escribe una función que envuelva esta función problemática y siga intentando hasta que una llamada tenga éxito, momento en el que devuelva el resultado. Asegúrate de manejar solo las excepciones que estás intentando manejar.
```js
class MultiplyError extends Error {};

function primitiveMultiply(a, b){
	for(;;){
		try{
			if(Math.random() < 0.20){
				return a * b;
			}else{
				throw new MultiplyError("error de multiplicacion");
			}
		} catch(e) {
			if (e instanceof MultiplyError) { 
				console.log("error"); 
			} else { 
				throw e; 
			}
		}
	}
}
```

La caja cerrada con llave
Hay un array en la caja, pero solo puedes acceder a él cuando la caja está desbloqueada. Escribe una función llamada withBoxUnlocked que reciba como argumento un valor de función, desbloquee la caja, ejecute la función y luego asegure que la caja esté cerrada de nuevo antes de devolverla, independientemente de si la función de argumento devolvió normalmente o lanzó una excepción.
```js
const box = new class { 
	locked = true; 
	#content = []; 
	unlock() { this.locked = false; } 
	lock() { this.locked = true; } 
	get content() { 
		if (this.locked) throw new Error("¡Cerrado con llave!"); 
		return this.#content;
	} 
};

function withBoxUnlocked(funct){
	
	let status = box.locked;
	if(status){
		box.unlock();
	};
	
	try{
		return funct();
	}finally{
		if(status){
			box.lock();
		}
	}
}
```