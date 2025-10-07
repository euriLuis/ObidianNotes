# Programación asíncrona
## Asincronía
Un modelo de programación asíncrono permite que multiples cosas sucedan una a la vez. 
Permite que multiples cosas sucedan al mismo tiempo. 
En el siguiente diagrama, las líneas gruesas representan el tiempo que el programa pasa funcionando normalmente, y las líneas delgadas representan el tiempo gastado esperando a la red. 
En el modelo síncrono, el tiempo tomado por la red es parte de la línea de tiempo para un hilo de control dado. En el modelo asíncrono, iniciar una acción en la red permite que el programa continúe ejecutándose mientras la comunicación en la red sucede junto a él, notificando al programa cuando haya terminado.
![[Captura de pantalla 2025-05-28 221959.png]]
## Retrollamadas.
Un enfoque para la programación asíncrona es hacer que las funciones que necesitan esperar algo tomen un segundo argumento adicional, *una función de devolución de llamada* o callback function. 

Ejemplo la función `setTimeout` espera un numero dado de milisegundos y luego llama a una función.
```js
setTimeout(() => console.log("Tick"), 500);
```

Otro ejemplo de operacion asincrona comun es leer un archivo desde el almacenamiento de un dispositivo. 
```js
readTextFile("lista_de_compras.txt", contenido => {
	console.log(`Lista de Compras:\n${contenido}`); 
}); 
// → Lista de Compras: 
// → Mantequilla de cacahuate 
// → Plátanos
```

Realizar múltiples acciones asincrónicas en fila usando devoluciones de llamada significa que tienes que seguir pasando nuevas funciones para manejar la continuación de la computación después de las acciones. Así es como podría verse una función asincrónica que compara dos archivos y produce un booleano que indica si su contenido es el mismo.
```js
function compararArchivos(archivoA, archivoB, devolucionLlamada) { 
	readTextFile(archivoA, contenidoA => { 
		readTextFile(archivoB, contenidoB => { 
			devolucionLlamada(contenidoA == contenidoB); 
		}); 
	}); 
}
```

## Promesas
Una forma diferente de construir un programa asíncrono es ==hacer que las funciones asincrónicas devuelvan un objeto que represente su resultado== en lugar de pasar devoluciones de llamada por todas partes. 
Para esto sirve la clase estándar `Promise`.
Una *promesa*  es un recibo que representa un valor que aun puede no estar disponible.
Proporciona un método *`then`* que permite registrar una función que debe ser llamada cuando la acción por la que esta esperando finalice. 
Cuando la promesa se resuelve, estas funciones son llamadas con el valor del resultado.
La forma mas sencilla de crear una promesa es llamando a `Promise.resolve`. 
Esta función se asegura de que el valor que le proporcionas este envuelto en una promesa. Si ya es una promesa simplemente se devuelve; de lo contrario, se obtiene una nueva promesa que se resuelve inmediatamente con el valor del resultado.
```js
let quince = Promise.resolve(15); 
quince.then(valor => console.log(`Obtenido ${valor}`)); 
// → Obtenido 15
```

Para crear una promesa que no se resuelva inmediatamente se puede utilizar a `Promise` como constructor. 
El constructor espera una función como argumento, la cual llama inmediatamente, pasándole una función que puede utilizar para resolver la promesa.
```js
function textFile(nombreArchivo) { 
	return new Promise(resolve => { 
		readTextFile(nombreArchivo, texto => resolve(texto)); 
	}); 
} 

textFile("planes.txt").then(console.log);
```

Esta función asíncrona devuelve un valor significativo: una promesa para proporcionarte el contenido del archivo en algún momento futuro.
El método `then` devuelve otra promesa que se resuelve al valor retornado por la función de devolución de llamada, o si esa función devuelve una promesa, al valor al que esa promesa se resuelve.
De esa manera se pueden encadenar varias llamadas a `then` para configurar una secuencia de acciones asíncronas. 
```js
function randomFile(archivoLista) { 
	return textFile(archivoLista) 
		.then(contenido => contenido.trim().split("\n")) 
		.then(ls => ls[Math.floor(Math.random() * ls.length)]) 
		.then(nombreArchivo => textFile(nombreArchivo)); 
}
```

La función devuelve el resultado de esta cadena de llamadas a *then*. 

En general es util pensar en las promesas como un mecanismo que permite al código ignorar la pregunta de cuando va a llegar un valor. Un valor norm tiene que existir realmente antes de que podamos hacer referencia a el. Un valor prometido es un valor que puede estar allí o podría aparecer en algún momento en el futuro. 
Las operaciones definidas en términos de promesas, al conectarlas con llamadas then, se ejecutan de forma asíncrona a medida que sus entradas están disponibles.

## Falla
Las computaciones regulares de JS pueden fallar al lanzar una excepción. 
Las computaciones asíncronas a menudo necesitan algo así.

El primer argumento de la devolución de llamada se utiliza para indicar que la acción falló, y el segundo contiene el valor producido por la acción cuando fue exitosa.
```js
unaFuncionAsincrona((error, valor) => { 
	if (error) manejarError(error); 
	else procesarValor(valor); 
});
```

Tales funciones de devolución de llamada siempre deben verificar si recibieron una excepción y asegurarse de que cualquier problema que causen, incluidas las excepciones lanzadas por las funciones que llaman, se capturen y se den a la función correcta.

Las promesas facilitan esto, pueden ser o bien resultas *==resolve==* o rechazadas *==reject==*. Los manejadores de resolución se llaman solo cuando la accion es exitosa y los rechazos se propagan a la nueva promesa que es devuelta por `then`. 
Cuando un manejador lanza una excepción esto causa automáticamente que la promesa producida por la llamada a su `then` sea rechazada.
Si en algún elemento de una cadena de acciones asíncronas falla, el resultado de toda la cadena se marca como rechazado, y no se llaman manejadores de éxito mas allá del punto donde fallo.

Cuando una excepción en una función manejadora causa el rechazo el valor de la excepción se usa como el motivo. 
Existe una función *`Promise.reject`* que crea una nueva promesa inmediatamente rechazada.
Para manejar explícitamente los rechazos las promesas tienen un método `catch` que registra un manejador para ser llamado cuando la promesa es rechazada, similar a como los manejadores de `then` manejan la resolución normal.
Como un atajo `then` también acepta un manejador de rechazo como segundo argumento. 
```js
function textFile(filename) { 
	return new Promise((resolve, reject) => { 
		readTextFile(filename, (text, error) => { 
			if (error) reject(error); 
			else resolve(text); 
		}); 
	}); 
}
```

Las cadenas de valores de promesa creadas por llamadas  `then` y `catch` forman así un pipeline a traves del cual se mueven los valores asíncronos o fallos.
Dado que dichas cadenas se crean registrando manejadores, cada eslabón tiene asociado un manejador de éxito o un manejador de rechazo (o ambos). Los manejadores que no coinciden con el tipo de resultado (éxito o fallo) son ignorados. 
Pero aquellos que coinciden son llamados, y su resultado determina qué tipo de valor viene a continuación: éxito cuando devuelve un valor que no es una promesa, rechazo cuando genera una excepción, y el resultado de la promesa cuando devuelve una promesa.
```js
new Promise((_, reject) => reject(new Error("Fail")))
	.then(value => console.log("Manejador 1:", value)) 
	.catch(reason => { 
		console.log("Error capturado " + reason); 
		return "nada"; 
	}) 
	.then(value => console.log("Manejador 2:", value)); 
	// → Error capturado Error: Fail 
	// → Handler 2: nothing
```

La primera función de manejador regular no es llamada porque en ese punto del pipeline la promesa contiene un rechazo. El manejador `catch`  maneja rechazo y devuelve un valor que se le da a la segunda función de manejador.
Cuando una excepción no controlada es manejada por el entorno, los entornos de JS pueden detectar cuando un rechazo de promesa no es manejado y lo reportarían como un error.

## Funciones asíncronas
Una función *async* es una función que implícitamente devuelve una promesa y que puede en su cuerpo `await` esperar otras promesas de una manera que parece sincrónica.

Podemos reescribir crackPasscode de la siguiente manera:
```js
async function crackPasscode(networkID) { 
	for (let code = "";;) { 
		for (let digit = 0;; digit++) { 
			let newCode = code + digit; 
			try { 
				await withTimeout(joinWifi(networkID, newCode), 50); 
				return newCode; 
			} catch (failure) { 
				if (failure == "Timed out") { 
					code = newCode; 
					break; 
				} else if (digit == 9) { 
					throw failure; 189 
				} 
			} 
		} 
	} 
}
```

Una función *async* está marcada con la palabra `async` antes de la palabra clave `function`. Los métodos también pueden ser marcados como *async* escribiendo `async` antes de su nombre. 
Cuando se llama a una función o método de esta manera, devuelve una promesa.
Tan pronto como la función devuelve algo, esa promesa se resuelve(resolve). Si el cuerpo genera una excepción, la promesa es rechazada(rejected).

Dentro de una función *async*, la palabra await puede colocarse delante de una expresión para esperar a que una promesa se resuelva y luego continuar con la ejecución de la función. Si la promesa es rechazada, se genera una excepción en el punto `await`. 
Una función así ya no se ejecuta, como una función regular de JavaScript, de principio a fin de una sola vez. En su lugar, puede estar congelada en cualquier punto que tenga un await, y puede continuar más tarde.

Al encadenarlas, las funciones async suelen ser más agradables de escribir que encadenar llamadas `then`.

## Generadores
Esta capacidad de pausar y luego reanudar funciones no es exclusiva de las funcione `async`. JS también tiene una característica llamada generador functions. Son similares, pero sin las promesas.

Cuando defines una función con `function*` (colocando un asterisco después de la palabra function), se convierte en un generador. Al llamar a un generador, devuelve un iterador.

```js
function* powers(n) { 
	for (let current = n;; current *= n) { 
		yield current; 
	} 
} 
for (let power of powers(3)) { 
	if (power > 50) break; 
	console.log(power); 
} 
// → 3 
// → 9 
// → 27
```

Inicialmente al llamar a powers, la función se congela desde el principio. Cada vez que llamas a `next` en el iterador, la función se ejecuta hasta que encuentra una expresión `yield`, que la pausa y hace que el valor generado se convierta en el proximo valor producido por el iterador.

Escribir iteradores es mas fácil cuando se usan funciones generadoras.
```js
Group.prototype[Symbol.iterator] = function*() { 
	for (let i = 0; i < this.members.length; i++) { 
		yield this.members[i]; 
	} 
};
```

Ya no es necesario crear un objeto para mantener el estado de la iteración: los generadores guardan automáticamente su estado local cada vez que hacen un `yield`.

Tales expresiones `yield` solo pueden ocurrir directamente en la función generadora misma y no en una función interna que definas dentro de ella. El estado que un generador guarda, al hacer `yield`, es solo su entorno local y la posición donde hizo el `yield`.
Una función async es un tipo especial de generador. Produce una promesa al llamarla, la cual se resuelve cuando retorna (termina) y se rechaza cuando arroja una excepción.
Cada vez que hace un `yield `(awaits) una promesa, el resultado de esa promesa (valor o excepción generada) es el resultado de la expresión `await`.

Promise tiene un método estático `all` que se puede usar para convertir un ar ray de promesas en una sola promesa que se resuelve en un array de resultados.
Esto proporciona una forma conveniente de que algunas acciones asíncronas sucedan al lado unas de otras, esperar a que todas terminen y luego hacer algo con sus resultados (o al menos esperar a que terminen para asegurarse de que no fallen).
```js
function displayFrame(frame) { 
	return Promise.all(frame.map((data, i) => { 
		return request(screenAddresses[i], { 
			command: "display", 
			data 
		}); 
	})); 
}
```

Esto recorre las imágenes en frame (que es un array de arrays de datos de visualización) para crear un array de promesas de solicitud. Luego devuelve una promesa que combina todas esas promesas.
Para poder detener un video en reproducción, el proceso está envuelto en una clase.
Esta clase tiene un método asíncrono play que devuelve una promesa que solo se resuelve cuando la reproducción se detiene de nuevo a través del método stop.
```js
function wait(time) { 
	return new Promise(accept => setTimeout(accept, time)); 
} 

class VideoPlayer { 
	constructor(frames, frameTime) { 
		this.frames = frames; 
		this.frameTime = frameTime; 
		this.stopped = true; 
	} 
	
	async play() { 
		this.stopped = false; 
			for (let i = 0; !this.stopped; i++) { 
				let nextFrame = wait(this.frameTime); 
				await displayFrame(this.frames[i % this.frames.length]); 
				await nextFrame; 
			} 194 
		} 
		
	stop() { 
		this.stopped = true; 
	} 
}
```

La función wait envuelve `setTimeout` en una promesa que se resuelve después del número de milisegundos especificado. Esto es útil para controlar la velocidad de reproducción.
```js
let video = new VideoPlayer(clipImages, 100); 
video.play().catch(e => { 
	console.log("La reproducción falló: " + e); 
}); 
setTimeout(() => video.stop(), 15000);
```

## El bucle de eventos
El comportamiento asincrónico ocurre en su propia función vacía pila de llamadas. Esta es una de las razones por las que, sin promesas, gestionar excepciones en código asincrónico es tan difícil. 
Dado que cada devolución de llamada comienza con una pila de llamadas en su mayoría vacía, sus manejadores de catch no estarán en la pila cuando lancen una excepción.
```js
try { 
	setTimeout(() => { 
		throw new Error("¡Zoom!"); 
	}, 20); 
} catch (e) { 
	// Esto no se ejecutará 
	console.log("Atrapado", e); 
}
```

Este ejemplo establece el tiempo de espera pero luego demora hasta después del momento previsto para el tiempo de espera, provocando que el tiempo de espera sea tardío. 
```js
let start = Date.now(); 
setTimeout(() => { 
	console.log("El tiempo de espera se ejecutó en", Date.now() start); 
}, 20); 
while (Date.now() < start + 50) {} 
console.log("Tiempo perdido hasta", Date.now()- start); 
// → Tiempo perdido hasta 50 
// → El tiempo de espera se ejecutó en 55
```

Las promesas siempre se resuelven o se rechazan como un nuevo evento. Incluso si una promesa ya esta resuelta, esperarla hara que su devolución de llamada se ejecute después de que termine el script actual.
```js
Promise.resolve("Hecho").then(console.log); 
console.log("¡Yo primero!"); 
// → ¡Yo primero! 
// → Hecho
```

## Errores asincrónicos.
Cuando tu programa se ejecuta de forma síncrona, de una sola vez, no hay cambios de estado ocurriendo excepto aquellos que el programa mismo real iza. Para programas asíncronos esto es diferente, pueden tener *brechas* en su ejecución durante las cuales otro código puede correr.

Esta es una función que intenta reportar el tamaño de cada archivo en un arreglo de archivos, asegurándose de leerlos todos al mismo tiempo en lugar de en secuencia.
```js
async function fileSizes(files) { 
	let lista = ""; 
	await Promise.all(files.map(async fileName => { 
		lista += fileName + ": " + 
			(await textFile(fileName)).length + "\n";
	})); 
	return lista; 
}
```

`async fileName =>` muestra cómo también se pueden hacer `arrow functions async` colocando la palabra `async` delante de ellas.

El problema radica en el operador +=, que toma el valor actual de lista en el momento en que comienza a ejecutarse la instrucción y luego, cuando el await termina, establece el enlace lista como ese valor más la cadena agregada. Pero entre el momento en que comienza a ejecutarse la instrucción y el momento en que termina, hay una brecha asincrónica. La expresión map se ejecuta antes de que se agregue cualquier cosa a la lista, por lo que cada uno de los operadores += comienza desde una cadena vacía y termina, cuando termina su recuperación de almacenamiento, estableciendo lista en el resultado de agregar su línea a la cadena vacía.

Esto podría haberse evitado fácilmente devolviendo las líneas de las prome sas mapeadas y llamando a join en el resultado de Promise.all, en lugar de construir la lista cambiando un enlace. Como suele ser, calcular nuevos valores es menos propenso a errores que cambiar valores existentes.
```js
async function fileSizes(files) { 
	let líneas = files.map(async fileName => { 
		return fileName + ": " + 
			(await textFile(fileName)).length; 
	}); 
		return (await Promise.all(líneas)).join("\n"); 
	}
```


## Ejercicios.
### Momentos de tranquilidad
Escribe una función asíncrona `activityTable(día)` que, para un día de la semana dado, devuelva un array de 24 números, uno para cada hora del día, que contenga la cantidad de observaciones de tráfico de red de la cámara vista en esa hora del día. Los días se identifican por número utilizando el sistema utilizado por Date.getDay, donde el domingo es 0 y el sábado es 6. 
La función activityGraph, proporcionada por el sandbox, resume dicha tabla en una cadena. Utiliza la función textFile definida anteriormente, que al recibir un nombre de archivo devuelve una promesa que se resuelve en el contenido del archivo. 
Recuerda que new Date(marcaDeTiempo) crea un objeto Date para ese momento, que tiene métodos getDay y getHours que devuelven el día de la semana y la hora del día. Ambos tipos de archivos, la lista de archivos de registro y los propios archivos de registro, tienen cada dato en su propia línea, separados por caracteres de nueva línea ("\n")
```js
function textFile(filename) { 
	return new Promise((resolve, reject) => { 
		readTextFile(filename, (text, error) => { 
			if (error) reject(error); 
			else resolve(text); 
		}); 
	}); 
}

async function activityTable(dia){
	//string de direcciones
	let contFile = await textFile("camera_logs.txt");
}

activityTable(1).them(table => console.log)
```

