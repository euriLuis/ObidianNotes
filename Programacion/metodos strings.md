# Métodos comunes de Strings en JavaScript

Una referencia rápida de los métodos más importantes y usados para manipular strings en JavaScript, con ejemplos prácticos.

---

## Manipulación de strings

1. **`.length`**: Devuelve la longitud del string.
```js
"Hola".length; // 4
```

2. **`.charAt(index)`**: Devuelve el carácter en la posición indicada.
```js
"Hola".charAt(1); // "o"
```

3. **`.charCodeAt(index)`**: Devuelve el código Unicode del carácter en la posición dada.
```js
"Hola".charCodeAt(1); // 111
```

4. **`.slice(start, end)`**: Extrae una parte del string.
```js
"JavaScript".slice(0, 4); // "Java"
```

5. **`.substring(start, end)`**: Similar a `slice`, pero no admite índices negativos.
```js
"JavaScript".substring(4, 10); // "Script"
```

6. **`.replace(search, replacement)`**: Reemplaza la primera coincidencia.
```js
"Hola mundo".replace("mundo", "amigo"); // "Hola amigo"
```

7. **`.replaceAll(search, replacement)`**: Reemplaza **todas** las coincidencias.
```js
"aaa".replaceAll("a", "b"); // "bbb"
```

8. **`.toUpperCase()`**: Convierte el string a mayúsculas.
```js
"hola".toUpperCase(); // "HOLA"
```

9. **`.toLowerCase()`**: Convierte el string a minúsculas.
```js
"HOLA".toLowerCase(); // "hola"
```

10. **`.trim()`**: Elimina espacios al inicio y final.
```js
"  hola  ".trim(); // "hola"
```

11. **`.trimStart()` / `.trimEnd()`**: Elimina espacios solo al principio o final.
```js
"  hola  ".trimStart(); // "hola  "
"  hola  ".trimEnd();   // "  hola"
```

12. **`.padStart(length, padString)`**: Rellena desde el inicio hasta alcanzar longitud.
```js
"5".padStart(3, "0"); // "005"
```

13. **`.padEnd(length, padString)`**: Rellena desde el final.
```js
"5".padEnd(3, "0"); // "500"
```

14. **`.repeat(count)`**: Repite el string varias veces.
```js
"ha".repeat(3); // "hahaha"
```

---

##  Búsqueda y comparación

15. **`.includes(substring)`**: Verifica si contiene el texto dado.
```js
"JavaScript".includes("Script"); // true
```

16. **`.startsWith(substring)`**: Verifica si empieza con el texto dado.
```js
"Hola mundo".startsWith("Hola"); // true
```

17. **`.endsWith(substring)`**: Verifica si termina con el texto dado.
```js
"Hola mundo".endsWith("mundo"); // true
```

18. **`.indexOf(substring)`**: Devuelve la posición de la primera aparición.
```js
"banana".indexOf("a"); // 1
```

19. **`.lastIndexOf(substring)`**: Devuelve la posición de la última aparición.
```js
"banana".lastIndexOf("a"); // 5
```

20. **`.localeCompare(string)`**: Compara dos strings (útil para orden alfabético).
```js
"casa".localeCompare("carro"); // -1
```

---

##  División y unión

21. **`.split(separator)`**: Divide el string en un array.
```js
"uno,dos,tres".split(","); // ["uno", "dos", "tres"]
```

22. **`.concat(string2)`**: Une strings.
```js
"Hola".concat(" ", "mundo"); // "Hola mundo"
```

---

##  Expresiones regulares

23. **`.match(regex)`**: Busca coincidencias con una expresión regular.
```js
"abc123".match(/\d+/); // ["123"]
```

24. **`.matchAll(regex)`**: Devuelve un iterador con todas las coincidencias.
```js
[..."123abc456".matchAll(/\d+/g)]; // [["123"], ["456"]]
```

25. **`.search(regex)`**: Devuelve el índice de la primera coincidencia.
```js
"abc123".search(/\d/); // 3
```

26. **`.replace(regex, replacement)`**: Reemplaza coincidencia usando regex.
```js
"hola 123".replace(/\d+/, "###"); // "hola ###"
```

27. **`.replaceAll(regex, replacement)`**: Reemplaza todas las coincidencias.
```js
"123 456".replaceAll(/\d+/g, "X"); // "X X"
```
