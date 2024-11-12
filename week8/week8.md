# Woche 8

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">05.11.2024</span>

### Inhalt

Slides

- [slides](WebProgramming_8_Optional_Typing.pdf)

Bearbeitet Dateien

TODO

- [AllTests.html](./AllTests.html)
- [lambda.js](./lambda/lambda.js)
- [lambdaTest.js](./lambda/lambdaTest.js)
- [util.js](./util/util.js)
- [utilTest.js](./util/utilTest.js)
- [TryTypeSystem.html](TryTypeSystem.html)

##### Javascript Goodies
```javascript

// object mit key value.
let x = 1;
{x:x}

// Shorthand für die Zuweisung
{x}

// Hier ein Beispiel um ein solches Objekt zu erstellen
const obj = {a:1,b:2,c:3}
let foo = obj;
foo.a

// Dekonstruktor
let {c} = obj
let {vc} = obj
let {b,c} = obj

// nur b und c verwenden
const myFun ({b,c}) => b + c;

// geht mit beiden, entweder direkt Objekt oder Werte angeben.
myfun(obj);
myfun({a:1,b:2,c:4})
```
##### Typen in JavaScript

Da es `leider` keine wirklichen Typen gibt in Javascript und diese man via denn Compiler (ja, JavaScript hat ja eigentliche gar keinen Compiler wie wir ihn kennen), sind wir auf die Unterstützung der IDE (VS Code, Intellij IDEA) angewiesen.

Es gibt allerdings bei Web Frameworks wie Angular, React, Vue and ... die Möglichkeit auf `Typescript` zu setzen, welche wie der Name verlauten lässt es ermöglicht durch den Compiler auf die richtigen Typisierung des Codes zu prüfen. Ausser man erstellt alles mit `any` :D.

**JsDoc**
JsDoc wird ähnlich wie das JavaDocs genutzt um weitere Informationen wie Typen Informationen, Parameter, Return values und Beschreibungne für Funktionen genutzt. Diese helfen dann andere Entwickler den Code zu verstehen. Insbesonder durch die IDE mit Funktionen wie Autocompletion und Typen Checking.

Da JsDoc optional ist, bedeutet das in der Hinsicht auch das die Typen optional sind. Es ist immer dem Entwickler überlassen solche Docs zu schreiben und pflegen.


`Intellij Setup`: Einstellungen -> Editor -> Inspection -> JavaScript and TypeScript
`VS Code Extension`: Gibt viele welche das unterstützen. Auch von Haus aus aber gibt Language Support: JavaScript Gruppe mit vielen nützlichen Erweiterungen.

Beispiel eines JsDoc:

```javascript
/**
 * This is a basic description of a function.
 * @param { String } name - The name of the person.
 * @param { Number } age - The age of the person.
 * @returns { String } A greeting message.
 */
function greet(name) {
  return `Hello, ${name}! You are going to be ${age + 1} next year.`;
}
```

JavaScript hat einige built-in Typen:

- Boolean
- Number
- String
- Object
- BigInt
- Symbol
- Null
- Undefined
- Function (`typeof`)

Diese verfügen über einen literalen Konstruktor und auch Operatoren.

Aber auch Objekt Klassen:

- Array
- Date
- RegExp
- Error
- Map
- Set
- JSON

**Tags in JavaDocs**

Funktionen mit `@type`:

1. **Simple Function Type**

```javascript
/**
 * @type { (A) => B }
 */
const exampleFunction = (a) => {
    // function implementation
};
```

2. **Curried Function Type**

```javascript
/**
 * @type { (A) => (B) => C }
 */
const curriedFunction = (a) => (b) => {
    // function implementation
};
```

3. **Function with Parameter Types**

```javascript
/**
 * @type { (a: A) => (b: B) => C }
 */
const parameterizedFunction = (a) => (b) => {
    // function implementation
};
```

4. **Generic Function Type**

```javascript
/**
 * @type { <T>(a: T) => (b: B) => T }
 */
const genericFunction = (a) => (b) => {
    // function implementation
};
```

Daten Typen mit `@property`

```javascript
/**
 * @property {Number} age - The age of the object.
 * 
 * @typedef {Array<Number>} NumberArray - An array of numbers.
 * @typedef {Number[]} NumberList - Another way to define an array of numbers.
 */

/**
 * Represents a person.
 * @typedef {Object} Person
 * @property {String} name - The name of the person.
 * @property {Number} age - The age of the person.
 */

/**
 * An array of persons.
 * @typedef {Person[]} PersonArray
 */
```

Union type:

```javascript
/**
 * Processes the input value which can be either a string or a number.
 * 
 * @param {(string|number)} input - The input value to be processed.
 * @returns {string} - The processed result as a string.
 */
```

Intersection type:

```javascript
/**
 * Log how cool a person is
 * @param { Person & Cool } person - A cool person.
 */
function cool(person) {
  console.log(`Hey, ${person.name} is really cool!`)
}
```

String literal type:

```javascript
/**
 * Get a string to describe the greating of me or you
 * @param { "me" | "you" }  - arg Me or you
 * @returns { String } A greeting message.
 */
function age(arg) {
  return `Hello, you are ${arg}!`;
}
```

Capability:

```javascript
/**
 * Processes an object with properties `a` and `b`.
 * @param {{a: string, b: Function}} obj - The object to process.
 * @returns {void} 
 */
function processObject(obj) {
  console.log(`Value of a: ${obj.a}`); // We know a must be a string
  obj.b(); // Invoke the function
}
```

Interfaces mit `@typedef`: 

```javascript
/**
 * @typedef {Object} Person
 * @property {string} name - The name of the person.
 * @property {number} age - The age of the person.
 * @property {Function} greet - A method that returns a greeting message.
 */
```

Callback mit `@callback`:

```javascript
/**
 * A callback function that processes a result.
 *
 * @callback resultCallback
 * @param {Error} error - An error object if an error occurred, otherwise null.
 * @param {Object} result - The result object if the operation was successful.
 */
```

Type Casts mit `@type`:

```javascript
/**
 * @type {string}
 * @description This variable holds a string value.
 */
```

### Wissenwertes / Gelerntes

- Funktionen mit Dekonstruktor deklarieren um nur die Properties welche man braucht angeben (Etwas ähnliches gibt es bei dem Function Mapping bei Haskell):

```javascript
/**
 * Berechnet die Summe der Eigenschaften eines Objekts.
 * @param {Object} obj - Das Objekt mit den Eigenschaften a und b.
 * @param {number} obj.a - Die erste Zahl.
 * @param {number} obj.b - Die zweite Zahl.
 * @returns {number} - Die Summe der beiden Zahlen.
 */
function sum({a, b}) {
    return a + b;
}

// Beispielaufruf
const result = sum({a: 5, b: 10});
console.log(result); // Ausgabe: 15
```

- jsDoc sind eine mächtige Art Code Dokumentation zu erfassen.