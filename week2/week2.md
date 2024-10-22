# Woche 1

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">24.19.2024</span>

### Inhalt

Slides

- [slides](WebProgramming_2_Lambda.pdf)

Bearbeitet Dateien

- [scopeTest.html](./scopeTest.html)

##### Javascript Goodies

2 Arten String zu erfassen, Iterale:

```javascript
"String mit Anführungszeichen";
"String mit einfachen Anführungszeichen";
```

Nutzen, Strings welche `"` oder `'` beinhalten kann man so trotzdem ohne escape zeichen schreiben

```javascript
// mit escape
"said \"hi!\" ";
// ohne escape
'said "hi"';

// genau das gleiche mit ''
"it's time";
```

String mit mehrere Zeichen oder Platzholden mit backtick `.

```javascript
// mehrere Zeilen
`erste Zeile
zweite Zeile`;

// platzhalter
`eins ist eine ${x}`;
```

Regex Strings mit `/`, damit spart man das Escapen der Spezialzeichen, Slashy Syntax.

```javascript
// Regex definieren
const regex = /\b/;
```

##### Snake Game

Was wir leider nicht letze Woche anschauen konnten, da uns die Zeit gefehlt hat. Man kann versuchen auf der Vorlage ein funktionieres Snake Game programmieren.

##### Ball Simulation

Auch hier kann man die Ball Simulation erweitern.

##### JavaScript Scopes

Klassisch gibt es eigentlich nur 2 Scopes:

- global: "window (im Browser)"
- function: "lokal zur eingezenden Funktion (lambda)"

In JavaScript gibt es vier Hauptmöglichkeiten, um Variablen zu deklarieren. Jede hat unterschiedliche Eigenschaften hinsichtlich ihrer Gültigkeit, ihres Speicherortes und ihrer Veränderlichkeit.

| Deklaration     | Gültigkeit                                    | Veränderlichkeit                                                                                  |
| --------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `x = ...`       | global, nach erstem Gebrauch                  | veränderbar, **nicht gebrauchen**                                                                 |
| `var x = ...`   | global oder lokal (je nach Kontext), hoisting | veränderbar, **nicht gebrauchen**                                                                 |
| `let x = ...`   | Block-scope, lokal                            | veränderbar                                                                                       |
| `const x = ...` | Block-scope, lokal                            | unveränderbar (der Wert selbst kann jedoch, wenn es sich um ein Objekt handelt, verändert werden) |

<span style="color: red; font-weight: bold;">&#9888; Achtung!</span>: hier im Unterricht <span style="color: red; font-weight: bold;">nie</span> `var` gebrauchen

```javascript
// Globale Variable (implizit deklariert)
x = 5;
console.log(x); // 5

// "var" Beispiel (hoisting)
console.log(y); // undefined (weil y durch hoisting nach oben verschoben wird)
var y = 10;

// "let" Beispiel (lokale Variable)
{
  let z = 15;
  console.log(z); // 15
}
console.log(z); // ReferenceError: z is not defined

// "const" Beispiel (unveränderbare Variable)
const a = 20;
console.log(a); // 20
a = 25; // TypeError: Assignment to constant variable.
```

Hier ein Beispiel, was beschreibt wo let überall gültig ist. Wenn 2 Variablen den gleichen Namen haben gewinnt das "Innere".

```javascript
let x = 0;
function foo() {
  let x = 1;
  document.writeln(String(x)); // Ausgabe: 1 (lokale Variable x innerhalb der Funktion)
}
foo();
document.writeln(String(x)); // Ausgabe: 0 (globale Variable x bleibt unverändert)
```

Das gleiche Beispiel aber mit `var`. Hier gibt es sogar 2 Sachen aus: undefined und 0. Das liegt daran, dass x nicht definiert war und das obige x nicht in der Funktion gültig und das x welches nachher deklariert wurde sich nachträglich noch meldet. Liegt daran das JavaScript einen Interpreter hat.

```javascript
var x = 0;
function foo() {
  document.writeln(String(x)); // Ausgabe: undefined 0
  var x = 1; // hoisting
}
foo();
```

Der Code wird also so interpretiert:

```javascript
var x = 0;
function foo() {
  var x; // Deklaration wird an den Anfang der Funktion verschoben
  document.writeln(String(x)); // Ausgabe: undefined (x ist deklariert, aber noch nicht zugewiesen)
  x = 1; // Zuweisung
}
foo();
```

##### IIFE, immediately invoked function expression

Anonyme Blöcke können so deklariert werden

```javascript
(() => {
  let x = 1;
  document.writeln(String(x));
})();
```

was auch geht ist:

```javascript
{
  let x = 1;
  document.writeln(String(x));
}
```

##### Lambda Calculus

Mit 3 Regeln kann man alles berechnen. <br>
Programmcode wird zu Algebra.

JavaScript Interpreter ist im Kern ein Lambda Calculus. (Evaluator)

**Alpha translation:**

```javascript
const id = (x) => x; // suche x auf der linke Seite gib x auf der rechten Seite
const id = (y) => y;
```

**Beta Reduktion I:**

```javascript
((x) => x)(1);
((x) => 1)(1);
1; // Alle x wurden durch 1 ersetzt
```

Würde man das rückgängig machen, würde dies eine _Beta Expansion_ heissen.

**Beta Reduktion II:**

```javascript
(
  (f) => (x) =>
    f(x)
)(id)(1);

((x) => id(x))(1);
id(1);
((x) => x)(1);
1; // Alle x wurden durch 1 ersetzt
```

**Eta Reduktion I:**

```javascript
(x) => foo(x);
foo; // funktion welche x nimmt und foo macht, ist foo
```

**Eta Reduktion II:**

```javascript
(x) => (y) => both(x)(y);
(x) => both(x);
both; //rightmost argument with rightmost parameter
```

### Wissenwertes / Gelerntes

Hoisting, deklaration von var wird nach oben verschoben aber nicht initialisiert, gibt undefined statt reference error.

```javascript
console.log(x); // undefined (wegen Hoisting)
var x = 5;
console.log(x); // 5
```

In JavaScript können Regex (reguläre Ausdrücke) mit Schrägstrichen (`/`) definiert werden. Dies spart das Escapen der Spezialzeichen.

```javascript
// Regex definieren
const regex = /\bword\b/;
const testString = "A word in a sentence.";
console.log(regex.test(testString)); // true
```
