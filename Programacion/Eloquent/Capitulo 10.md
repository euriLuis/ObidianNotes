# Módulos
Los módulos son un  mecanismo para empaquetar y *namespacing* código.
Namepacing es una via para evitar colisión de nombres
## Programas modulares
Un modulo es una parte de un programa que especifica en que otras piezas se basa y que funcionalidad proporciona para que otros módulos la utilicen.
Un buen sistema de módulos requiere que los módulos especifiquen que código ellos utilizan de otros módulos. Estas relaciones se llaman *dependencias*
## Módulos ES
Desde 2015 con ECMAScript 6 JS admite el uso de las palabras clave *import* y *export*. Este sistema se suele llamar sistemas de módulos ES.

Este sistema convierte entre nombres de días y números 
```js
const names = ["Domingo", "Lunes", "Martes", "Miércoles", "Jueves", "Viernes", "Sábado"]; 

export function dayName(number) { 
return names[number];
} 
export function dayNumber(name) { 
return names.indexOf(name); 
}
```

La palabra clave *export* se puede colocar delante de una función, clase o definición de vinculación para indicar que esa vinculación es parte de la interfaz del módulo. 
Esto permite que otros módulos la utilicen.
```js
import {dayName} from "./dayname.js";
let ahora = new Date(); 
console.log(`Hoy es ${dayName(ahora.getDay())}`); 
// → Hoy es Lunes
```

La palabra clave *import* seguida de una lista de nombres de vinculación entre llaves hace que las vinculaciones de otro modulo estén disponibles en el modulo actual.
Las declaraciones de importación y exportación no pueden aparecer dentro de funciones, bucles u otros bloques.

-Las vinculaciones importadas se pueden renombrar para darles un nuevo nombre local utilizando *as* después de su nombre.
```js
import {dayName as nomDeJour} from "./dayname.js";
console.log(nomDeJour(3));
// → Miércoles
```

Es posible que un modulo tenga una exportación *default* que a menudo se usa para módulos que solo exportan un único enlace.

Para definir una exportación predeterminada se escribe *export default* antes de una expresion, una declaracion de funcion o una declaracion de clase.
```js
export default ["Invierno", "Primavera", "Verano", "Otoño"];
```

Este enlace se importa omitiendo las llaves alrededor del nombre de la importación.
```js
import nombresEstaciones from "./nombrsestaciones.js";
```


## Paquetes
Un paquete es un fragmento de código que se puede distribuir. 
Puede contener uno o mas módulos y tiene información sobre de que otros paquetes depende. Un paquete también suele venir con documentación que explica que hace para que las persons que no lo escriben aun puedan usarlo.

NPM es dos cosas: un servicio en línea donde puedes descargar (y subir) paquetes y un programa (incluido con Node.js) que te ayuda a instalar y gestionarlo.

## Módulos CommonJS
Un modulo CommonJS se ve como un script regular, pero tiene acceso a dos enlaces que utiliza para interactuar con otros módulos. 
El primero es una función llamada require. Cuando llamas a esto con el nombre del modulo de tu dependencia, se asegura de que e modulo este cargado y devuelve su interfaz. 
El segundo es un objeto llamado exports, que es el objeto de interfaz para el modulo. Comienza vació y agregas propiedades para definir los valores exportados
```js
exports.formatDate = function(date, format) { 
	return format.replace(/YYYY|M(MMM)?|Do?|dddd/g, tag => {
		if (tag == "YYYY") return date.getFullYear(); 
		if (tag == "M") return date.getMonth(); 
		if (tag == "MMMM") return months[date.getMonth()]; 
		if (tag == "D") return date.getDate(); 
		if (tag == "Do") return ordinal(date.getDate()); 
		if (tag == "dddd") return days[date.getDay()]; 
	}); 
};
```

La técnica de desestructuración es muy conveniente al crear enlaces para las interfaces importadas.
El modulo añade su función de interfaz a exports para que los módulos que dependen de e tengan acceso a ella.
```js
const {formatDate} = require("./format-date.js");
console.log(formatDate(new Date(2017, 9, 13),
						"dddd the Do")); 
// → Viernes 13º
```

CommonJS se implementa con un cargador de módulos, que al cargar un modulo, envuelve su código en una función dándole su propio ámbito local y pasan los enlaces require y exports a esa función como argumentos.
```js
function require(name) { 
	if (!(name in require.cache)) { 
		let code = readFile(name); 
		let exports = require.cache[name] = {}; 
		let wrapper = Function("require, exports", code); 
		wrapper(require, exports); 
	} 
	return require.cache[name]; 
} 
require.cache = Object.create(null);
```

Para evitar cargar el mismo modulo multiples veces, require mantiene un cache de módulos ya cargados, Cuando se llama, primero comprueba si el modulo solicitado ha sido cargado y si no lo carga. Esto implica leerlo código del modulo, envolverlo en una función y llamarlo

A diferencia de las declaraciones *import*, las llamadas a *require* pueden aparecer dentro de funciones, y el nombre de la dependencia puede ser cualquier expresión que se evalúe a una cadena, mientras que *import* solo permite cadenas simples entre comillas.

Node.js permite que los módulos ES importen desde módulos CommonJS. Por lo tanto, si bien el código CommonJS es algo con lo que te encontrarás, ya no hay una razón real para escribir nuevos programas en este estilo.

## Compilación y empaquetado.
No es raro que el código que se encuentre en un paquete de NPM  haya pasado por multiples etapas de transformación, convirtiéndose de JS moderno a JS histórico, luego combinando los módulos en un solo archivo y minimizando el código. 

## Diseño de módulos.
Un aspecto del diseño de módulos es la facilidad de uso. Si estas diseñado algo que se supone sera utilizado por varias personas es útil que la interfaz sea simple y predecible.

Otro aspecto importante es la facilidad con la que algo puede ser compuesto con otro código.
Los módulos enfocados en calcular valores son aplicables en una gama mas amplia de programas que los módulos mas grandes que realizan acciones complicadas con efectos secundarios. 

Si deseas diseñar para la composabilidad, averigua qué estructuras de datos están utilizando otras personas y, cuando sea posible, sigue su ejemplo.
Una vez que tengas algo que se sienta sólido, es un buen momento para dar un paso atrás y organizarlo.


----

Los módulos proporcionan estructura a programas mas grandes al separar el código en piezas con interfaces claras y dependencias. La interfaz es la parte del modulo que es visible para otros módulos y las dependencias son los otros módulos que se utilizan.
Un paquete es un fragmento de código que se puede distribuir por si solo. 





| Hola | Tooll |
| ---- | ----- |
