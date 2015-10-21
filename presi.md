class: center, middle
background-image: url(background-intro.png)

# Working with git and git-flow

---
class: middle
background-image: url(background.png)

# Ausgangssituation

- Es gibt 2 Rollen:
  - Entwickler: Die Person, die eine Anforderung entwickelt.
  - Reviewer: Die Person, die die Entwicklung prüft und Verbesserungsvorschläge auszeigt.
- Erster Entwickler legt den Feature-Branch an, veröffentlicht ihn auf dem Server und arbeitet darauf
- Zweiter Entwickler arbeitet auch an dem Feature.
- Nach Abschluss der Entwicklung prüft der Revier die Arbeit und schließt diese ab.
---
class: middle
background-image: url(background.png)

# Variablen (Block bindings)

- Bisher gibt es nur:
  - var  function scoped
- Neu:
  - let: block scoped
  - const: wie der Name sagt ;-)
- Daher ... nie mehr var!!

---
class: middle
background-image: url(background.png)

# Demo zu Variablen (block bindings):

```JavaScript
function f() {
  var y = 'outer';
  {
    let x;
    {
      // Okay, block scoped
      const x = 'bar';
      // Fehler, const
      x = 'foo';
      y = 'inner';
    }
    // Fehler, bereits deklariert
    let x = 'inner';
  }
  console.log(y); //y==='inner'
}
```

---
class: middle
background-image: url(background.png)

# Auflösen bzw. Zuweisen (Destructuring)
- Mehrfach Zuweisung in einer Zeile.
- Einfaches Tauschen von 2 (oder mehr) Variablen

---
class: middle
background-image: url(background.png)

# Demo zu Auflösen bzw. Zuweisen (Destructuring):
```JavaScript
let [a, b] = [1, 2];		

a = 'foo';
b = 'bar';

[a, b] = [b, a];

console.log(a); // a === 'bar'
console.log(b); // b === 'foo
```

---
class: middle
background-image: url(background.png)

# String und reguläre Ausdrücke

- Besseres Unicode
  - auch für Regexp (/u)
- Mehr Methoden für String
  - startsWith
  - endsWith
  - includes
- Template String

---
class: middle
background-image: url(background.png)

# Demo zu den neuen String-Funktionen:

```JavaScript
console.log("\u0061");      // "a"		
console.log("\u20BB7");     // "7"

let msg = 'Hello world!';
console.log(msg.startsWith('Hello'));  // true
console.log(msg.endsWith('!')); // true
console.log(msg.includes('o')); // true

let name = 'Martin';
console.log(`Hello ${name}`); // Hello Martin
```

---
class: middle
background-image: url(background.png)

# Funktionen

- Default-Parameter
- Rest-Parameter
- Spread-Parameter
- Name-Property
- Arrow-Funktions
  - keine arguments
  - this bleibt gültig

---
class: middle
background-image: url(background.png)

# Demo zu Funktionen

```JavaScript
function makeRequest(url, cb = function() {}) {
}
function pick(first, ...rest) {
  // first === 'a', rest === [1, 2, 3]
} 	
pick('a', 1, 2, 3);

let values = [25, 100];
// console.log(Math.max(25, 100));
console.log(Math.max(...values));

function doSomething() {
	// the function code
}
console.log(doSomething.name);  // doSomething
```

---
class: middle
background-image: url(background.png)

# Objekte

- Kurze Form der Methoden
- Prototype-Accessor

---
class: middle
background-image: url(background.png)

# Demo zu Objeten

```JavaScript
let person = {
  name: 'Martin',
  sayName() {
    console.log(this.name);
  }
};

let friend = {
  __proto__: person
};
```

---
class: middle
background-image: url(background.png)

# Symbole (Symbols)

- Neuer primitiver Datentype analog zu "string", "numbers" ...
- Definition von privaten Properties

---
class: middle
background-image: url(background.png)

# Demo zu Symbolen

```JavaScript
'use strict';
// only on node.js <= 4.0.0
//const Symbol = require('symbol');
const key = Symbol();

const obj = {};
obj[key] = 'foo';
console.log(obj[key]); // 'foo'
console.log(Object.keys(obj)); // []
```

---
class: middle
background-image: url(background.png)

# Iterator und Generator

- Interator ist ein Interface-Pattern
  - spezielle Schnittstelle
- Generator in ein spezielles Pattern eines Iterators
  - \*functions
  - yield
- for x of y - loop

---
class: middle
background-image: url(background.png)

```JavaScript
// iterator		
function createIterator() {
  let i = 1;
  return {
    next: function() {
      let done = (i <= 2);
      i++;
      return {done: done, value: i};
    }
  };
}
// generator
function *gen() {
	yield 1;
	yield 2;
}
// for x of y - loop
let items = [1, 2];
for (let x of y) {}
```

---
class: middle
background-image: url(background.png)

# Klassen

- Klassen
  - nicht nur Prototypen
  - super()
  - constructor
  - properties
  - static Functions
- Ableitung
  - extends
  - instanceof
- (Leider) Keine Zugriffsbeschränkung

---
class: middle
background-image: url(background.png)

```JavaScript
class BaseClass {		
  sayName() { console.log('BaseClass'); }
}

class DerivedClass extends BaseClass {
  constructor() {
    this._name = 'no name';
  }
  sayName() { console.log('DerivedClass'); }		    	
  get name() {
    return this._name;
  }		    	
  set name(newName) {
    this._name = newName;
  }
  static helloWorld() {
  }
}
```

---
class: middle
background-image: url(background.png)

## Mengen und Aufzählungen (Arrays und Collections)

- Array
  - Erzeugen mit fester Länge ohne Werte
  - Array auf anderem Array mit Transformation
- Typisierte Arrays
  - Uint8Array ( Node.js Buffer)
  - Uint16Array
- Sets
  - Sortierte Liste
- Maps
  - Schlüssel: Werte Paare
  - eindeutiger Schlüssel
- WeakSet
  - GC kann Objekt aus Speicher entfernen
- WeakMap
  - Key muss ein Object sein
  - GC kann Key aus Speicher entfernen

---
class: middle
background-image: url(background.png)

# Demo zu Mengen und Aufzählungen (1)

```JavaScript
items = new Array(2);		
console.log(items.length); // 2
console.log(items[0]); // undefined
console.log(items[1]); // undefined

function translate() {
  return Array.from(arguments, (value) => value + 1);
}
let numbers = translate(1, 2, 3);
console.log(numbers); // [2, 3, 4]

```

---
class: middle
background-image: url(background.png)

# Demo zu Mengen und Aufzählungen (2)
```JavaScript
var items = new Set();		
items.add(5);
items.add("5");
items.add(5); // Doppelter Eintrag --> ignoriert
console.log(items.size);   // 2

var map = new Map();
map.set('name', 'Martin');
console.log(map.has('name'));   // true
console.log(map.get('name'));   // 'Martin'
console.log(map.size);
```

---
class: middle
background-image: url(background.png)

# Promises
- Asynchroner Programmfluss ohne Callback-Hölle
- Umgang mit Ausnahmen
  - nicht in jedem Callback separat

---
class: middle
background-image: url(background.png)

# Demo zu Promises

```JavaScript
'use strict';

let p1 = new Promise((resolve, reject) => {
  resolve(42);
});

p1.then(function(value) {
  console.log(value);
  let p2 = new Promise((resolve, reject) => {    
    resolve(value + 1);
  });
  return p2;
}).then(function(value) {
  console.log(value);     // 43
});  	
```

---
class: middle
background-image: url(background.png)

# Reflection
#### Neue Klasse Reflect (auch in Object enthalten)
- defineProperty()
- getOwnPropertyDescriptor()
- preventExtensions()
- isExtensible()
- apply()
- construct
- deleteProperty
- enumerate()
- get()
- getPrototypeOf()
- has()
- ownKeys()
- set()
- setPrototypeOf()

---
class: middle
background-image: url(background.png)

# Module
- Veröffentlichen von (export):
  - Klassen
  - Funktionen
  - Variablen
  - als Symbole
- Verwenden von Bereitgestellten (import):
  - Klassen
  - Funktionen
  - Variablen

---
class: middle
background-image: url(background.png)

# Demo zu Modulen (export)

```JavaScript
export var color = "red";		

export let name = "Nicholas";

export const magicNumber = 7;

export function sum(num1, num2) {
  return num1 + num1;
}

export default class MyClass {
  constructor() {
  }
}

export {color as RedColor};
```

---
class: middle
background-image: url(background.png)

# Demo zu Modulen (import)

```JavaScript
import {sum, multiply, magicNumber} from 'example';		
import * as example from 'example';

import {sum} from 'example';

import {sum as mySum } from 'example';

import {default as OtherClass} from 'example';
```
---
class: center, middle
background-image: url(background.png)

# Weitere Änderungen in ES6
### (Math, Integer-Klasse + Safe-Integers)

---
class: center, middle
background-image: url(background.png)

# ES7
### oder Ausblick auf die nächste Generation von JavaScript

---
class: middle
background-image: url(background.png)

# Asynchrone Funktionen
### (aka: async and await)

- Einfacher Umgang mit asynchronen Funktionsaufrufen
  - async
  - await

---
class: middle
background-image: url(background.png)

# Demo zu Asynchrone Funktionen

```JavaScript
async function doAsync(query) {

  let httpClient = new HttppClient()

  let result = await httpClient.get(query);

  return result;
}
```

---
class: middle
background-image: url(background.png)

# Decorator bzw. Annotation
- Attribute an:
  - Klassen
  - Funktionen
- Meta-Daten
- Reflextion-/Meta-Programmierung
- Grundlage für Dependency Injection
  - Angular 2.0

---
class: middle
background-image: url(background.png)

# Demo zu Decorator bzw. Annotation

```JavaScript
// --annotations		
import {Anno} from './resources/setup.js';

@Anno
function Simple() {}

assertArrayEquals([new Anno], Simple.annotations);
```

---
class: middle
background-image: url(background.png)

# Object – Rest and Spread Operator

- Rest:
  - Rest einer Variable zuweisen
- Spread:
  - Array/Collection EINER Variable zuweisen

---
class: middle
background-image: url(background.png)

# Demo zu Object - Rest and Spread Operator

```JavaScript
// Rest		
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(z) // { a: 3, b: 4 }


// Spread
let n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 }
```

---
class: middle
background-image: url(background.png)

# Bindung bei Funktionen
#### (function binding or ::)
- Neuer Operator ::
- Native Umsetzung für:
  - f.bind(self)
- Gebundene Funktionen einer Variable zuweisen
  - callback‘s mit Instanzmethoden

---
class: middle
background-image: url(background.png)

# Demo zu Bindung bei Funktionen
#### (function binding or ::)

```JavaScript
// BISHER:
let fkt = (msg) => console.log(msg);
Promise.resolve(12).then(fkt);
// oder
Promise.resolve(12).then(console.log.bind(console));

// NEU: Gebundene Funktion als Callback mitliefern
Promise.resolve(12).then(::console.log);
```

---
class: middle
background-image: url(background.png)

# Klassen Properties
- Instanzen Properties
  - get <prop-name>() {}
  - set <prop-name>() {}
- Statisch!
- Singleton-Pattern

---
class: middle
background-image: url(background.png)

# Demo zu Klassen Properties

```JavaScript
class MyClass {
  instance = null;

   static createInstance() {
     if (instance === null) {
       instance = new MyClass();
     }
     return instance;
   }
}
```

---
class: middle
background-image: url(background.png)

# Array Comprehensions
- Funktionale Programmierung
- Erzeugen eines Array‘s durch einen Expr.
- Unterscheidungen:
  - Array direkt
  - Generator lazy

---
class: middle
background-image: url(background.png)

# Demo zu Array Comprehensions

```JavaScript
// Array comprehensions
var results = [
  for (c of customers)
    if (c.city == "Seattle")
      { name: c.name, age: c.age }
]

// Generator comprehensions
var results = (
  for (c of customers)
    if (c.city == "Seattle")
      { name: c.name, age: c.age }
)
```

---
class: center, middle
background-image: url(background.png)

# TypeScript

---
class: center, middle
background-image: url(background.png)

## TypeScript --> Voraussichtlich am 21.10.2015
