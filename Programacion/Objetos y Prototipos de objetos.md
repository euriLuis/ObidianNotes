# Conceptos básicos de los objetos JavaScript y prototipos

## Objetos
>Un objeto es una colección de datos relacionados y/o funcionalidad[denominados propiedades y métodos]

Se puede crear con `objeto.create`

Para acceder a las propiedades de un objeto se puede usar la notación de punto o con notación de corchetes.
Las propiedades de un objeto deben estar separadas por coma.
```js 
let person = {
	name: "Pepe Suarez",
	age: 33,
	intereses: ["musica", "esqui"],
	saludo: function (){
		console.log("Hola, soy " + this.name + ".");
	}
}
```

```js
console.log(person.name); //->notacion de punto.
//Pepe Suarez
console.log(person[age]); //notacion de corchetes
//33
```

Para acceder a propiedades de objetos anidados en otro  objeto solo se debe agregar un paso mas
```js
nombre : {
	pila: 'Bob',
	apellido: 'Smith'
}

person.nombre.pila;
person[nombre][pila];
```

Los objetos a veces se nombran arreglos asociativos.
Para establecer el valor de las propiedades de un objeto solo hay que declarar el valor de esta lo cual sirve para crear propiedades nuevas.
```js
persona.edad = 45;
persona["nombre"]["apellido"] = "Cratchit";
```

Una utilidad de la notación de corchetes es que se puede utilizar para establecer los nombres de las propiedades
```js
var nombrePerzonalizado = entradaNombre.value;
var valorPerzonalizado = entradaValor.value;

persona[nombrePerzonalizado] = valorPerzonalizado;
```

La palabra clave `this` se refiere al objeto actual en el que se esta escribiendo el código.

## Prototipos de objetos
>Los prototipos son mecanismo mediante el cual los objetos en JS heredan características entre si.

Los objetos pueden tener un objeto prototipo, el cual actúa como un objeto plantilla que hereda métodos y propiedades.

```js
function Persona(nombre, apellido, edad, genero, intereses) {
  // definiendo de propiedades y métodos
  this.first = first;
  this.last = last;
  //...
}

//creando una instancia
var person1 = new Persona("Bob", "Smith", 32, "hombre", ["music", "skiing"]);
```

>Los métodos y propiedades no se copian de un objeto a otro en la cadena del prototipo. Ellos son accedidos subiendo por la cadena como se ha descrito anteriormente.

