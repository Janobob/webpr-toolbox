# Woche 6

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">22.10.2024</span>

### Inhalt

Slides

- [slides](WebProgramming_6_Objects.pdf)

Bearbeitet Dateien

- [AllTests.html](./AllTests.html)
- [object.js](./object/object.js)
- [objectTests.js](./object/objectTest.js)

Weitere Infos + Hausaufgaben

- [Oopsie](./oopsie)

##### Javascript Goodies

Eine Methode ist eine Funktion, die als Eigenschaft eines Objekts aufgerufen wird, z.B. `obj.method()` (mit Zustand).
Eine Funktion hingegen ist ein eigenständiges, unabhängiges Code-Block, der ausgeführt wird, z.B. `functionName()` (ohne Zustand).

`slice`
Diese Methode erstellt ein neues Array, indem sie eine Kopie eines Teils eines bestehenden Arrays basierend auf den angegebenen
Start- und Endindizes (ohne das Endelement) zurückgibt. Sie verändert das ursprüngliche Array nicht undunterstützt auch negative Indizes, um von rechts zu zählen.

```javascript
[0, 1, 2, 3, 4].slice(2, 3);
// Output: [2]
[0, 1, 2, 3, 4].slice(2, 4);
// Output: [2,4]
[0, 1, 2, 3, 4].slice(2, 5);
// Output: [2,3,4]

// kein index out of bound
[0, 1, 2, 3, 4].slice(2, 50);
// Output: [2,3,4]

// ohne ende
[0, 1, 2, 3, 4].slice(2);
// Output: [2,3,4]

// ohne anfang und ende
[0, 1, 2, 3, 4].slice();
// Output: [0,1,2,3,4]

// bis zum letzen
// negative zahlen rechnen von rechts rückwärts
[0, 1, 2, 3, 4].slice(0, -1);
// Output: [0,1,2,3]
[0, 1, 2, 3, 4].slice(0, -2);
// Output: [0,1,2]
```

`splice`
Diese Methode ändert das ursprüngliche Array, indem sie Elemente entfernt, hinzufügt oder ersetzt, basierend auf den angegebenen
Startindex und der Anzahl der zu entfernenden Elemente. Sie gibt ein Array der entfernten Elemente zurück und kann auch neue Elemente an der Stelle einfügen.

Beispiel:
Analog zu einem Seil welches verbunden wird (spleiss)

```javascript
[0, 1, 2, 3, 4].splice(0, 1);
// Output: [0]

let ary = [0, 1, 2, 3, 4];
ary.splice(0, 1);
// Output: [0]
// ary: [1, 2, 3, 4]

ary.splice(0, 1);
// Output: [1]
// ary: [2, 3, 4]

// ary zurücksetzen
ary = [0, 1, 2, 3, 4];
ary.splice(1, 3);
// Output: [1,2,3]
// ary: [0, 4]

// neue einträge hinfügen
ary.splice(1, 0, 1, 2, 3);
// Output: [], nichts gelöscht
// ary: [0, 1, 2, 3, 4]
```

##### Objekten

**Was sind Objekte**

- Data Strukturen
- Methoden für zugriff und management
- Zugriff auf einen veränderbaren Zustand
- Abstrkationen und Polymorphismus

**3 unterschiedliche Möglichkeiten Objekte zu bilden**

**open, dynamic**

JS "Objects", Key Value pair
Funktionen werden auch als Werte gespeichert

```javascript
// literal object constructor
// no safety but super dynamic
// unobvious how to share structure
// beware of "this"!, am besten vermeiden in javascript
const good = {
  firstname: "Good",
  lastname: "Boy",
  getName: function () {
    return this.firstname + " " + this.lastname;
  },
  // getName() { return this.a }, syntactic sugar
};
```

> Bei `this` muss man hier aufpassen, weil es wie in java immer auf die "Instanz" zugreift.
> Kein `this` in lambda lokal gebunden

**closed, explizit**

```javascript
// eigentlich konstruktor
// best safety, easy to share structure, but no class
function Person(first, last) {
    return { getName: () => first + " " + last; }
}
```

> Kann z.B. nicht fragen ob type ist von einer bestimmten Klasse, hast du interface

**mixed, classified**

```javascript
const Person = (() => {
  // lexical scope
  function Person(first, last) {
    // ctor, binding
    this.firstname = first;
    this.lastname = last;
  }
  Person.prototype.getName = function () {
    return this.firstname + " " + this.lastname;
  };
  return Person;
})(); // IIFE
new Person("Good", "Boy") instanceof Person;
```

### Wissenwertes / Gelerntes

`slice`

```javascript
[0, 1, 2, 3, 4].slice(2, 3); // Output: [2]
[0, 1, 2, 3, 4].slice(0, -1); // Output: [0, 1, 2, 3]
```

`splice`

```javascript
let array = [0, 1, 2, 3, 4];

// Entfernt 2 Elemente ab Index 2
array.splice(2, 2);
// Output: [2, 3], array wird zu: [0, 1, 4]

// Fügt ab Index 1 ein neues Element hinzu
array.splice(1, 0, 10);
// Output: [], array wird zu: [0, 10, 1, 4]

// Entfernt ab Index 1 und fügt neue Elemente ein
array.splice(1, 2, 20, 30);
// Output: [10, 1], array wird zu: [0, 20, 30, 4]
```
