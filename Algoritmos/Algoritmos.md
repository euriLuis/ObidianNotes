 Búsqueda Binaria.

**Explicación:**
*El objetivo de este algoritmo es buscar en un array  ordenado si esta presente un elemento dado*
*Se divide el array a la mitad, y se compara el elemento que se esta buscando con el elemento se se encuentra en la mitad de este elemento,  si el elemento que se esta buscando es menor que el elemento que quedo en la mitad del array entonces se encuentra en la primera mitad, si es mayor se encuentra en la segunda.*
*Esto se sigue aplicando hasta que se encuentra el elemento que se esta buscando.*

**Complejidad**
$O(\log n)$

**Implementación**
*Se definen las variables que representaran el limite inferior y superior de cada array, se declara la variable que representara el medio, este se calculara en cada iteración del bucle.*
```js
function binSerch(elemento, arr) {
	let low = 0;
	let higth = arr.length - 1;
	let mid;
	while (low < higth) {
		mid = Math.round((higth + low) / 2);
		if (elemento < arr[mid]) {
			higth = mid -1;
		}else if (elemento > arr[mid]) {
			low = mid + 1;
		} else {
			return `Se encontro a ${elemento}`;
		}
	}
	return `El ${elemento} no se encuentra en el array`;
}
```


