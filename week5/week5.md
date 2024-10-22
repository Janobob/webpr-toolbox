# Woche 4

<span style="background-color: #e0e0e0; border-radius: 10px; padding: 5px 10px;">08.10.2024</span>

### Inhalt

Bearbeitet Dateien

// TODO

- [functionsTest.html](./functionsTest.html)

##### Javascript Goodies

const ary = [0,1,2,3,4];
ary

ary.push(5);
result ist länge

ary.pop();
result ist element welches gepopt wurde
rechtes / letzes element wurde entfernt und zurückgegeben

ary.shift();
result ist erstes element welches entfernt ist
also linkes element

ary.unshift(0);
neues element links anhängen
result ist länge

// array umdrehen variante range operator
[1,2,3].reduce( (acc, cur) => [cur, ...acc], []);
... range operator, rest operator

// array umdrehen variante unshift
[1,2,3].reduce( (acc, curr) => {acc.unshift(cur); return acc;}, [])

##### scripting

was ist scripting?

compiler ist versteckt, nicht sichtbar und nur teile

hauptmerkmal:
scripting = string nehmen also text und auswerten
sources: file, url, db, user input, ...

warum scripting?

command line, automation, build system, templating, code distrubition, formulae, business rules, smart configuration, product lines, dsl, self-modifying code, ...

characteristics

interpreted, non compolid
lenient type system - nachsichtig
"best effort" approach

##### progressive web app for testing

progressive web app

code that produces code gets interpred and thereby produces code, that ...

code nachladen kann sehr gefährlich sein.
code lädt weiterer schädlicher byte code

just like a virus - funktionsweise ist gleich

loading test suite dynamically

document.writeln('<script src="function/function.js"><\/script>');

##### general purpose function plotter

eval function gut für nur eine funktion und nicht für wenn der code mehrmals ausgeführt wird
// side effecting code

Function()
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

f ist eine funktion welche ein funktion body zurück gibt, so muss man nicht mehrmals f = Function setzen

##### excel in the browser

### Wissenwertes / Gelerntes

methode shift und unshift

array umdrehen mit reduce

js ist "best effort"
