# Woche 4

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">08.10.2024</span>

### Inhalt

Slides

- [slides](WebProgramming_4_MapFilterReduce.pdf)

Bearbeitet Dateien

- [lambda.js](./lambda/lambda.js)
- [lambdaTest.js](./lambda/lambdaTest.js)

##### Javascript Goodies

Higher order functions

```javascript
// for loop
[0, 1, 2, 3].foreach((elem) => elem);

// boolean function für jedes Element in Liste / Array
[0, 1, 2, 3].every((elem) => elem > 1);
// Output: false
[0, 1, 2, 3].every((elem) => elem < 10);
// Output: true

// boolean function für ein Element in Liste / Array
[0, 1, 2, 3].some((elem) => elem < 10);
// Output: true
[0, 1, 2, 3, 4, 5, 6].some((elem) => {
  console.log(elem);
  return elem > 1;
});
// erwartet:
// Output:
// 0
// 1
// 2
// true
```

So könnte man einen max für eine unendliche Reihe machen.

```javascript
let max = Number.NEGATIVE_INFINITY;

// auch möglich mit .foreach();
[0, 1, 2, 3].some((elem) => {
  if (elem > max) {
    max = elem;
  }
  return false; // return false, damit some nicht früher aufhört
});

// Output: Max value found: 3
console.log(`Max ist: ${max}`);
```

##### Applied Map/Filter/Reduce

**(a, b) vs a => b =>**

```javascript
// multiple parameters
const times = (a, b) => a \* b;
// Fehler weil zweiter Paramter fehlt
times(2);
```

- _Nachteil:_ b = undefined ==> NaN
- _Vorteil(?):_ Viel verwendet von Funktionen und Libraries, direkte Fehlermeldung

```javascript
// parameter chain, "curried"
const times = a => b => a \* b;
// Kein Fehler, Rückgabewert ist eine Funktion
times(2)
```

- _Nachteil:_ b = undefined ==> NaN
- _Vorteil(?):_ Ermöglicht funktionale Programmierung, Kann spezifische Funktionen erstellen.

Funktionales Programmieren Beispiel:

```javascript
// timesByTwo ist eine Funktion, die eine Zahl mit 2 multipliziert
const timesByTwo = times(2);
// Output: 10
console.log(timesByTwo(5));
```

**"partial" application**

Bedeutet wenn noch nicht alle Parameter gebunden wurden. Wie Beispiel von oben.
Elegant mit higher-order functions wie `map`, `filter`, und `reduce`

Kleiner Hinweis: Google ist eigentlich nichts anders ein grosser map reduce 😀;

`map`:

Jedes element wird durch mitgegebene funktion gejagt und ersetzt (z.B. x => x \* 2)
Die Grösse bleibt dabei aber gleich.

```javascript
const times = a => b => a \* b;
const twoTimes = times(2);

[1,2,3].map(x => times(2)(x));
[1,2,3].map(times(2));
[1,2,3].map(twoTimes);
```

`filter`:

Alle element mit predicate == true werden behalten (z.B. x => x % 2 === 1)
Die Grösse kann kleiner werden (eigentlich was man möchte)

```javascript
// partial filter
const odd = (x) => x % 2 === 1;

[1, 2, 3].filter((x) => x % 2 === 1);
[1, 2, 3].filter((x) => odd(x));
[1, 2, 3].filter(odd);
```

`reduce`:
Die `reduce`-Funktion wird verwendet, um ein Array auf einen einzigen Wert zu reduzieren. Sie durchläuft das Array und wendet eine Funktion auf jedes Element an, wobei ein Akkumulator (`acc`) und das aktuelle Element (`cur`) verwendet werden. Die Funktion hat zwei Parameter:

- **Callback-Funktion:** Diese Funktion wird auf jedes Element des Arrays angewendet. Sie nimmt zwei Argumente:
  - acc (Akkumulator): Der akkumulierte Wert, der nach jedem Durchlauf aktualisiert wird.
  - cur (aktuelles Element): Das aktuelle Element des Arrays, das gerade verarbeitet wird.
- **Initialwert (optional):** Ein optionaler Startwert für den Akkumulator. Wenn kein Initialwert angegeben wird, wird das erste Element des Arrays als Initialwert verwendet und die Iteration beginnt beim zweiten Element.

```javascript
reduce((acc, cur) => acc + cur).
```

```javascript
// un-partial reduce
const plus = (acc, cur) => acc + cur;
[1, 2, 3].reduce((acc, cur) => acc + cur);
[1, 2, 3].reduce(plus);

// variant with initial accu value as 2nd argument
// then cur starts at first element
[1, 2, 3].reduce(plus, 0);
```

##### Snake and Tupeln(n)

### Wissenwertes / Gelerntes

JS Methode welche sehr cool und das C# Gegenstück.

`every(...)` ==> `All(...)`

`some(...)` ==> `Any(...)`

Verwenden von unpartial um filter und map leserlicher und wiederverwendbar zu machen.

```javascript
const isGreaterThan = (num, threshold) => num > threshold);
const multiplyBy = (num, factor) => num * factor);

const numbers = [1, 2, 3, 4, 5];

// Verwende isGreaterThan und multiplyBy mit filter und map
const filteredNumbers = numbers.filter(isGreaterThan(2)); // Alle Zahlen größer als 2
const mappedNumbers = numbers.map(multiplyBy(2)); // Alle Zahlen mal 2
```
