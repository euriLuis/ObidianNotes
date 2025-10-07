## Arrays
### Métodos de modificación de arrays

1. **`push()`**: Añade elementos al final del array.
```js
let arr = [1, 2, 3]; 
arr.push(4); // [1, 2, 3, 4]
```

2. **`pop()`**: Elimina el último elemento del array.
```js
let arr = [1, 2, 3];
arr.pop(); // 3 console.log(arr); // [1, 2]
```

3. **`shift()`**: Elimina el primer elemento del array.
```js
let arr = [1, 2, 3]; 
arr.shift(); // 1 console.log(arr); // [2, 3]
```

4. **`unshift()`**: Añade elementos al inicio del array.
```js
let arr = [1, 2, 3]; 
arr.unshift(0); // [0, 1, 2, 3]
```

5. **`splice()`**: Añade, elimina o reemplaza elementos en cualquier posición.
```js
let arr = [1, 2, 3, 4];
arr.splice(1, 2, 'a', 'b'); // [2, 3] eliminados, 'a', 'b' añadidos 
console.log(arr); // [1, 'a', 'b', 4]
```

6. **`fill()`**: Rellena los elementos de un array con un valor.
```js
let arr = [1, 2, 3];
arr.fill(0); // [0, 0, 0]
```

7. **`reverse()`**: Invierte el orden de los elementos en el array.
```js
let arr = [1, 2, 3]; 
arr.reverse(); // [3, 2, 1]
```

8. **`sort()`**: Ordena los elementos del array.
```js
let arr = [3, 1, 2]; 
arr.sort(); // [1, 2, 3]
```

9. **`copyWithin()`**: Copia una sección del array a otra posición dentro del mismo array.
```js
let arr = [1, 2, 3, 4]; 
arr.copyWithin(2, 0, 2); 
// [1, 2, 1, 2]
```
---

### Métodos de búsqueda y acceso

1. **`indexOf()`**: Encuentra el primer índice de un elemento en el array.
```js
let arr = [10, 20, 30];
console.log(arr.indexOf(20)); // 1
```

2. **`lastIndexOf()`**: Encuentra el último índice de un elemento en el array.
```js
let arr = [10, 20, 10, 30]; 
console.log(arr.lastIndexOf(10)); // 2
```

3. **`includes()`**: Verifica si el array contiene un elemento.
```js
let arr = [10, 20, 30]; console.log(arr.includes(20)); // true
```

4. **`find()`**: Encuentra el primer elemento que cumpla con la condición.
```js
let arr = [5, 10, 15]; 
let result = arr.find(x => x > 8); // 10
```

5. **`findIndex()`**: Encuentra el índice del primer elemento que cumpla con la condición.
```js
let arr = [5, 10, 15];
let result = arr.findIndex(x => x > 8); // 1
```

6. **`at()`**: Obtiene el elemento en un índice específico, soporta índices negativos.
```js
let arr = [10, 20, 30]; 
console.log(arr.at(1)); // 20 
console.log(arr.at(-1)); // 30
```

---

### Métodos de transformación y filtrado
1. **`map()`**: Crea un nuevo array con los resultados de la función aplicada a cada elemento.
```js
let arr = [1, 2, 3];
let newArr = arr.map(x => x * 2); 
// [2, 4, 6]
```

2. **`filter()`**: Crea un nuevo array con los elementos que cumplen la condición.
```js
let arr = [1, 2, 3, 4]; 
let newArr = arr.filter(x => x > 2); 
// [3, 4]
```

3. **`reduce()`**: Aplica una función contra un acumulador y cada elemento.
```js
let arr = [1, 2, 3, 4];
let sum = arr.reduce((acc, val) => acc + val, 0); 
// 10
```

4. **`reduceRight()`**: Aplica una función contra un acumulador y cada elemento de derecha a izquierda.
```js
let arr = [1, 2, 3, 4]; 
let sum = arr.reduceRight((acc, val) => acc + val, 0); 
// 10
```

5. **`flat()`**: Aplana un array multidimensional.
```js
let arr = [1, [2, 3], [4, 5]]; 
let flatArr = arr.flat(); 
// [1, 2, 3, 4, 5]
```

6. **`flatMap()`**: Primero mapea cada elemento y luego aplana el resultado.
```js
let arr = [1, 2, 3]; 
let newArr = arr.flatMap(x => [x, x * 2]); 
// [1, 2, 2, 4, 3, 6]
```
---

### Métodos de iteración

1. **`forEach()`**: Ejecuta una función para cada elemento del array.
```js
let arr = [1, 2, 3];
arr.forEach(x => console.log(x)); // 1 2 3
```

2. **`some()`**: Verifica si al menos un elemento cumple la condición.
```js
let arr = [1, 2, 3]; 
console.log(arr.some(x => x > 2)); // true
```

3. **`every()`**: Verifica si todos los elementos cumplen la condición.
```js
let arr = [1, 2, 3]; console.log(arr.every(x => x > 0)); // true
```

4. **`keys()`**: Devuelve un objeto Array Iterator con las claves (índices) del array.
```js
let arr = [10, 20, 30]; 
let iterator = arr.keys(); 
for (let key of iterator) { 
	console.log(key); // 0 1 2 
}
```

5. **`values()`**: Devuelve un objeto Array Iterator con los valores del array.
```js
 let arr = [10, 20, 30]; 
 let iterator = arr.values();
 for (let value of iterator) { 
	 console.log(value); // 10 20 30
 }
```

6. **`entries()`**: Devuelve un objeto Array Iterator con pares clave/valor del array.
```js
let arr = [10, 20, 30]; 
let iterator = arr.entries(); for (let entry of iterator) { 
	console.log(entry); // [0, 10] [1, 20] [2, 30]
}
```

---

### Métodos de combinación y conversión

1. **`concat()`**: Combina dos o más arrays.
```js
let arr1 = [1, 2];
let arr2 = [3, 4]; 
let combined = arr1.concat(arr2); 
// [1, 2, 3, 4]
```

2. **`join()`**: Convierte todos los elementos del array en una cadena.
```js
let arr = [1, 2, 3]; 
let str = arr.join('-'); 
// '1-2-3'
```

3. **`slice()`**: Crea una copia superficial de una porción del array.
```js
let arr = [1, 2, 3, 4]; let newArr = arr.slice(1, 3); 
// [2, 3]
```

4. **`from()`**: Crea un nuevo array a partir de un objeto iterable.
```js
let arr = Array.from('hello'); 
// ['h', 'e', 'l', 'l', 'o']
```

5. **`isArray()`**: Verifica si el valor es un array.
```js
let arr = [1, 2, 3]; console.log(Array.isArray(arr)); 
// true
```

6. **`toString()`**: Convierte el array a una cadena.
```js
let arr = [1, 2, 3]; console.log(arr.toString()); 
// '1,2,3'
```

7. **`toLocaleString()`**: Convierte el array a una cadena con formato local.
```js
let arr = [1, 2, 3]; 
console.log(arr.toLocaleString()); 
// '1,2,3'
```
