# Woche 4

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">08.10.2024</span>

### Inhalt

Bearbeitet Dateien

// TODO

- [functionsTest.html](./functionsTest.html)

##### Javascript Goodies

Higher order functions

[0,1,2,3].foreach(elem => elem);
[0,1,2,3].every(elem => elem > 1)
false
[0,1,2,3].every(elem => elem < 10)
true
[0,1,2,3].some(elem => elem < 10)
true
[0,1,2,3,4,5,6].some(elem => {console.log(elem);return elem > 1;})
erwartet
0
1
2
true

so könnte man einen max für eine unendliche Reihe machen.

##### Applied Map/Filter/Reduce

(a, b) vs a => b =>

// multiple parameters
const times = (a, b) => a \* b;
times(2) // ???
// error message?

Vorteil?
b = undefined ==> NaN
viel verwendet von funktionen und libraries

// parameter chain, "curried"
const times = a => b => a \* b;
times(2) // ???
// useful?

Gibt keine Fehlermeldung, rückgabewert ist eine Funktion

"partial" application

wenn noch nicht alle parameter gebunden wurden.

elegant mit higher-order functions(map, filter, und reduce)

Google = grosser map reduce :D

map:
jedes element wird durch mitgegebene funktion gejagt und ersetzt (z.B. x => x \* 2)
grösse bleibt gleich

const times = a => b => a \* b;
const twoTimes = times(2);

[1,2,3].map(x => times(2)(x));
[1,2,3].map(times(2));
[1,2,3].map(twoTimes);

filter:
alle element mit predicate == true werden behalten (z.B. x => x % 2 === 1)
kann kleiner werden

partial filter

const odd = x => x % 2 === 1;

[1,2,3].filter(x => x % 2 === 1);
[1,2,3].filter(x => odd(x));
[1,2,3].filter(odd);

reduce:
reduce((acc, cur) => acc + cur)

acc = accumulator
cur = current

1+2 3
3+3

un-partial reduce:
const plus = (acc, cur) => acc + cur;
[1,2,3].reduce((acc, cur) => acc + cur);
[1,2,3].reduce(plus);

// variant with initial accu value as 2nd argument
// then cur starts at first element

[1,2,3].reduce(plus, 0)

##### Snake and Tupeln(n)

### Wissenwertes / Gelerntes

methode every and some.
