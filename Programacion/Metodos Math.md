# 🧮 Métodos principales del objeto Math en JavaScript

Una guía con los métodos más usados y útiles del objeto Math para operaciones matemáticas en JavaScript.

---

## 🔢 Operaciones básicas

1. **`Math.abs(x)`**: Devuelve el valor absoluto de un número.
```js
Math.abs(-5);    // 5
Math.abs(3.14);  // 3.14
Math.abs(-0);    // 0
```

2. **`Math.round(x)`**: Redondea al entero más cercano.
```js
Math.round(4.7);  // 5
Math.round(4.4);  // 4
Math.round(-4.6); // -5
```

1. **`Math.floor(x)`**: Redondea hacia abajo al entero más cercano.
```js
Math.floor(4.9);  // 4
Math.floor(-4.1); // -5
```

2. **`Math.ceil(x)`**: Redondea hacia arriba al entero más cercano.
```js
Math.ceil(4.1);   // 5
Math.ceil(-4.9);  // -4
```

3. **`Math.trunc(x)`**: Elimina la parte decimal (truncar).
```js
Math.trunc(4.9);  // 4
Math.trunc(-4.9); // -4
```

---

## 📊 Comparaciones y extremos

4. **`Math.max(...values)`**: Devuelve el mayor de los números dados.
```js
Math.max(1, 5, 3);     // 5
Math.max(...[2, 8, 1]); // 8
```

5. **`Math.min(...values)`**: Devuelve el menor de los números dados.
```js
Math.min(1, 5, 3);     // 1
Math.min(...[2, 8, 1]); // 1
```

6. **`Math.sign(x)`**: Devuelve el signo de un número (-1, 0, 1).
```js
Math.sign(5);   // 1
Math.sign(-5);  // -1
Math.sign(0);   // 0
```

---

## 🎲 Números aleatorios

7. **`Math.random()`**: Genera un número aleatorio entre 0 (incluido) y 1 (excluido).
```js
Math.random(); // 0.7834592847
// Número entre 1 y 10:
Math.floor(Math.random() * 10) + 1;
```

---

## 📐 Potencias y raíces

8. **`Math.pow(base, exp)`**: Eleva un número a una potencia.
```js
Math.pow(2, 3);  // 8
Math.pow(4, 0.5); // 2
```

9. **`Math.sqrt(x)`**: Devuelve la raíz cuadrada.
```js
Math.sqrt(16); // 4
Math.sqrt(2);  // 1.4142135623730951
```

10. **`Math.cbrt(x)`**: Devuelve la raíz cúbica.
```js
Math.cbrt(8);   // 2
Math.cbrt(27);  // 3
```

11. **`Math.exp(x)`**: Devuelve e^x (exponencial).
```js
Math.exp(1); // 2.718281828459045 (e)
Math.exp(0); // 1
```

---

## 📏 Logaritmos

12. **`Math.log(x)`**: Logaritmo natural (base e).
```js
Math.log(Math.E); // 1
Math.log(10);     // 2.302585092994046
```

13. **`Math.log10(x)`**: Logaritmo base 10.
```js
Math.log10(100); // 2
Math.log10(1000); // 3
```

14. **`Math.log2(x)`**: Logaritmo base 2.
```js
Math.log2(8);  // 3
Math.log2(16); // 4
```

---

## 🌊 Funciones trigonométricas

15. **`Math.sin(x)`**: Seno (x en radianes).
```js
Math.sin(Math.PI / 2); // 1
Math.sin(0);           // 0
```

16. **`Math.cos(x)`**: Coseno (x en radianes).
```js
Math.cos(0);       // 1
Math.cos(Math.PI); // -1
```

17. **`Math.tan(x)`**: Tangente (x en radianes).
```js
Math.tan(Math.PI / 4); // 1
Math.tan(0);           // 0
```

18. **`Math.asin(x)`**: Arco seno (resultado en radianes).
```js
Math.asin(1); // 1.5707963267948966 (π/2)
Math.asin(0); // 0
```

19. **`Math.acos(x)`**: Arco coseno (resultado en radianes).
```js
Math.acos(1); // 0
Math.acos(0); // 1.5707963267948966 (π/2)
```

20. **`Math.atan(x)`**: Arco tangente (resultado en radianes).
```js
Math.atan(1); // 0.7853981633974483 (π/4)
Math.atan(0); // 0
```

---

## 🎯 Constantes útiles

21. **`Math.PI`**: El valor de π (pi).
```js
Math.PI; // 3.141592653589793
```

22. **`Math.E`**: El número de Euler.
```js
Math.E; // 2.718281828459045
```

23. **`Math.LN2`**: Logaritmo natural de 2.
```js
Math.LN2; // 0.6931471805599453
```

24. **`Math.SQRT2`**: Raíz cuadrada de 2.
```js
Math.SQRT2; // 1.4142135623730951
```

---

## 💡 Ejemplos prácticos

```js
// Generar número aleatorio en un rango
function randomRange(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Calcular distancia entre dos puntos
function distancia(x1, y1, x2, y2) {
  return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
}

// Convertir grados a radianes
function gradosARadianes(grados) {
  return grados * (Math.PI / 180);
}
```