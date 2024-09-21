# Woche 1

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">17.19.2024</span>

### Inhalt

Bearbeitet Dateien

- [functionsTest.html](./functionsTest.html)

Diese Woche haben wir Javasript Funktionen und deren Signaturen angeschaut.

```javascript
// Normale Funktionsdeklaration
function add(a, b) {
  return a + b;
}

// Lambda-Funktion (Arrow Function)
const addLambda = (a, b) => a + b;
```

Man muss aber aufpassen, dass die Methoden immer etwas zurückgeben, ansonsten undefined.
Wichtig ist das `return` keyword.

```javascript
// Normale Funktionsdeklaration ohne return
function subtract(a, b) {
  a - b;
}

// Lambda-Funktion ohne return
const subtractLambda = (a, b) => {
  a - b;
};

// Beispielaufrufe
console.log(subtract(5, 3)); // Ausgabe: undefined
console.log(subtractLambda(5, 3)); // Ausgabe: undefined
```

Funktionen können in Variablen gespeichert.

```javascript
// Funktion in einer Variablen speichern
const multiply = function (a, b) {
  return a * b;
};

// Lambda-Funktion in einer Variablen speichern
const divide = (a, b) => a / b;

// Beispielaufrufe
console.log(multiply(4, 5)); // Ausgabe: 20
console.log(divide(20, 4)); // Ausgabe: 5
```

Funktionen können andere Funktionen als Parameter haben.

```javascript
// Funktion als Parameter.
function doit(whatToDo) {
  return function bla(arg) {
    return whatToDo(arg);
  };
}

// Beispielaufrufe
test(doit(fun1)(10) === 1);
test(doit(fun2)(10) === 10);

// Funktion als Parameter als Lambda.
const doit2 = (callme) => (arg) => callme(arg);

// Beispielaufrufe
test(doit2(fun1)(10) === 1);

// Funktion in Variable speichern
const doFun2 = doit2(fun1);

// Beispielaufrufe
test(doFun2(10) === 1);
test(doFun2() === 1);
```

### Wissenwertes / Gelerntes

Lambda Funktionen mit 2 Paramater können auch so geschrieben werden, werden dann mit `fun(x)(y)` aufgerufen

```javascript
// Lambda-Funktion mit zwei Parametern
const exampleFunction = (x) => (y) => {
  return x + y;
};

// Beispielaufruf
const addFive = exampleFunction(5);
console.log(addFive(3)); // Ausgabe: 8
```

Neuen String aus object erstellen, aber nicht alles wird schön angezeigt.

```javascript
// String ohne das 'new' Keyword erstellen
// String aus einem Objekt erstellen
const obj = { name: "John", age: 30 };
const str2 = String(obj);
console.log(str2); // Ausgabe: [object Object]
```
