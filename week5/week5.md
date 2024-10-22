# Woche 5

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">15.10.2024</span>

### Inhalt

Slides

- [slides](WebProgramming_5_Scripting.pdf)

Bearbeitet Dateien

- [AllTests.html](./AllTests.html)
- [plotter.js](./plotter/plotter.js)
- [plotterTests.js](./plotter/plotterTest.js)
- [View.html](./plotter/View.html)

Weitere Infos + Hausaufgaben

- [Excel](./excel)
- [Function](./function)

##### Javascript Goodies

```javascript
const ary = [0, 1, 2, 3, 4];
// Output: [0, 1, 2, 3, 4]

ary.push(5);
// Output: 6, Rückgabe ist neue Länge

ary.pop();
// Output; 5, Rückgabe ist element welches gepopt wurde
// rechtes / letzes element wurde entfernt und zurückgegeben

ary.shift();
// Output: 0, Rückgabe ist erstes element welches entfernt ist
// also linkes element bzw. an Index 0

ary.unshift(0);
// Output: 6, Rückgabe ist neue Länge
// neues element links anhängen

// array umdrehen variante range operator
// ... range operator, rest operator
[1, 2, 3].reduce((acc, cur) => [cur, ...acc], []);

// array umdrehen variante unshift
[1, 2, 3].reduce((acc, curr) => {
  acc.unshift(cur);
  return acc;
}, []);
```

##### Scripting

**Was ist scripting?**

- Compiler ist versteckt, nicht sichtbar und nur teile
- Hauptmerkmal ist einen String nehmen und diesen auswerten, Dieser kann aus verschiedenen sources kommen:
  - file
  - url
  - db
  - user input
  - ...

**Warum scripting?**

- command line
- automation
- build system
- templating
- code distrubition
- formulae
- business rules
- smart configuration
- product lines
- dsl
- self-modifying code
- ...

**Characteristics**

- Interpretiert und nicht kompiliert
- Das Ausführungssystem ist nachsichtig: lenient type system
  - "Best Effort" Approach

##### Scripting Caution

"architecture" of self modifiying code from unreliable sources:

AJAX, PWA, Mashup, "MicroFW", ...

Licenses often require dynamic loading (Google, Facebook, etc)

"Gives you enough rope to hang yourself."

##### progressive web app for testing

**progressive web app**

"Code that produces code gets interpred and thereby produces code, that ..."

- Code nachladen kann sehr gefährlich sein.
- Code lädt weiterer schädlicher byte code
- Just like a virus - funktionsweise ist gleich

loading test suite dynamically:
`document.writeln('<script src="function/function.js"><\/script>');`

##### general purpose function plotter

`eval`:

Gut für nur eine funktion und nicht für wenn der code mehrmals ausgeführt wird. Kann viele Nebeeffekte haben, einfach böswilligen Code einfügen.

```javascript
// side effecting code
eval("x = 2 * y");
```

`Function()`:

```javascript
const add = Function('x','y','return x + y');
add(1,2);
add(2,3); // no need to re-parse
// avoid side effects

// todo: how to display?
const f = (\_) => Function("x", "return " + userFunction.value);

display(canvas, f());
userFunction.onchange = (\_) => {
display(canvas, f());
};
```

f ist eine funktion welche ein funktion body zurück gibt, so muss man nicht mehrmals f = Function setzen

### Wissenwertes / Gelerntes

`shift()`:
Entfernt das erste Element eines Arrays und gibt dieses zurück. Das Array wird dabei verändert (d.h., das ursprüngliche Array wird kürzer).

```javascript
const array = [1, 2, 3];
const firstElement = array.shift();

console.log(firstElement); // Output: 1
console.log(array); // Output: [2, 3]
```

`unshift()`:
Fügt ein oder mehrere Elemente am Anfang des Arrays hinzu. Das Array wird dabei verändert (d.h., das ursprüngliche Array wird länger).

```javascript
const array = [2, 3];
const newLength = array.unshift(1);

console.log(newLength); // Output: 3
console.log(array); // Output: [1, 2, 3]
```

Array umdrehen mit reduce:

```javascript
[1, 2, 3].reduce((acc, cur) => [cur, ...acc], []);

[1, 2, 3].reduce((acc, curr) => {
  acc.unshift(cur);
  return acc;
}, []);
```

> Javascript ist **"Best Effort"**

> Scripting am besten mit `Function()`
