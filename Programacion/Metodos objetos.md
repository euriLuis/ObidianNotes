# 🧱 Métodos comunes para trabajar con Objetos en JavaScript

Una guía con los métodos más usados y útiles para manipular objetos en JavaScript.

---

  

## 🔍 Inspección y propiedades

  

1. **`Object.keys(obj)`**: Devuelve un array con las claves del objeto.

```js

const persona = { nombre: "Ana", edad: 30 };

Object.keys(persona); // ["nombre", "edad"]

```

  

2. **`Object.values(obj)`**: Devuelve un array con los valores del objeto.

```js

const persona = { nombre: "Ana", edad: 30 };

Object.values(persona); // ["Ana", 30]

```

  

3. **`Object.entries(obj)`**: Devuelve un array de pares clave-valor.

```js

const persona = { nombre: "Ana", edad: 30 };

Object.entries(persona); // [["nombre", "Ana"], ["edad", 30]]

```

  

4. **`Object.hasOwn(obj, prop)`**: Verifica si el objeto tiene la propiedad (mejor que `hasOwnProperty`).

```js

const persona = { nombre: "Ana" };

Object.hasOwn(persona, "nombre"); // true

```

  

---

  

## 🧪 Comparación y asignación

  

5. **`Object.is(val1, val2)`**: Compara dos valores de forma estricta (más preciso que `===`).

```js

Object.is(NaN, NaN); // true

Object.is(+0, -0);   // false

```

  

6. **`Object.assign(dest, ...sources)`**: Copia propiedades de uno o más objetos fuente a un objeto destino.

```js

const destino = { a: 1 };

const fuente = { b: 2 };

Object.assign(destino, fuente); // { a: 1, b: 2 }

```

  

---

  

## 🧱 Creación y prototipos

  

7. **`Object.create(proto)`**: Crea un nuevo objeto con el prototipo indicado.

```js

const proto = { saludar() { return "Hola"; } };

const obj = Object.create(proto);

obj.saludar(); // "Hola"

```

  

8. **`Object.defineProperty(obj, prop, descriptor)`**: Define o modifica una propiedad directamente.

```js

const persona = {};

Object.defineProperty(persona, "edad", {

  value: 30,

  writable: false

});

```

  

9. **`Object.defineProperties(obj, props)`**: Define varias propiedades a la vez.

```js

const persona = {};

Object.defineProperties(persona, {

  nombre: { value: "Ana" },

  edad: { value: 30 }

});

```

  

---

  

## 🔒 Inmutabilidad y estado

  

10. **`Object.freeze(obj)`**: Congela un objeto (no se puede modificar ni extender).

```js

const config = { modo: "estricto" };

Object.freeze(config);

config.modo = "normal"; // No tiene efecto

```

  

11. **`Object.seal(obj)`**: Sella un objeto (no se pueden agregar/eliminar propiedades).

```js

const config = { modo: "estricto" };

Object.seal(config);

delete config.modo; // No tiene efecto

```

  

12. **`Object.isFrozen(obj)`**: Verifica si un objeto está congelado.

```js

Object.isFrozen(config); // true o false

```

  

13. **`Object.isSealed(obj)`**: Verifica si un objeto está sellado.

```js

Object.isSealed(config); // true o false

```

  

---

  

## 🧠 Otros útiles

  

14. **`Object.fromEntries(entries)`**: Crea un objeto a partir de un array de pares clave-valor.

```js

const entradas = [["nombre", "Ana"], ["edad", 30]];

Object.fromEntries(entradas); // { nombre: "Ana", edad: 30 }

```

  

15. **`Object.getOwnPropertyDescriptors(obj)`**: Devuelve todos los descriptores de propiedades del objeto.

```js

const obj = { x: 10 };

Object.getOwnPropertyDescriptors(obj);

// { x: { value: 10, writable: true, enumerable: true, configurable: true } }

```