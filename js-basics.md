# JavaSript Basics


In a nutshell:

-	Created by Brendan Eich at Netscape, in 1995.
-	The name comes from a cooperation with Sun Microsystems but it has nothing to do with Java.
-	Standardized by ECMA (ECMAScript Language Specification).
-	Interpreted language.
-	Dynamic typing.
-	Object Oriented language based on Prototypes.
-	Functional language with nested functions and closures.

Below is a detailed overview of the basis of the language. This presentation is heavily based on <cite><a href='http://www.maritimejournal.com/__data/assets/pdf_file/0020/1033940/Javascript-The-Good-Parts.pdf'>JavaScript: The Good Parts</a></cite> by Douglas Crockford. This more or less correspond to the fift version of the ECMAScript standard (ES5). The sixth version ES6 or ES2015 has many new features (classes, modules, arrow functions, etc.) that are not described here.


<!-- TOC depth:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [JavaSript Basics](#javasript-basics)
	- [Syntax](#syntax)
		- [Variables](#variables)
		- [Comments](#comments)
		- [Names](#names)
		- [Reserved Words](#reserved-words)
	- [Numbers](#numbers)
		- [Numbers Encoding Format](#numbers-encoding-format)
		- [NaN](#nan)
		- [Infinity](#infinity)
		- [Utility functions](#utility-functions)
		- [Parse Strings to Numbers](#parse-strings-to-numbers)
	- [Strings](#strings)
		- [String Literals](#string-literals)
		- [Escaped Characters](#escaped-characters)
		- [unicode](#unicode)
		- [Concatenation](#concatenation)
		- [Length](#length)
		- [String Methods](#string-methods)
	- [Control Flow](#control-flow)
		- [if/else](#ifelse)
		- [for](#for)
		- [while](#while)
		- [switch](#switch)
	- [Expressions](#expressions)
		- [Operators Precedence](#operators-precedence)
		- [Refinement](#refinement)
		- [Invocation](#invocation)
		- [Objects](#objects)
		- [Arrays](#arrays)
		- [Regexp (borrowed from perl)](#regexp-borrowed-from-perl)
		- [Functions](#functions)
		- [Anonymous functions](#anonymous-functions)
	- [Scope](#scope)
	- [Strict Mode](#strict-mode)
	- [Objects](#objects)
		- [Object Literal](#object-literal)
		- [Access to properties](#access-to-properties)
		- [Objects are passed by reference](#objects-are-passed-by-reference)
	- [Prototype](#prototype)
		- [Constructor Functions](#constructor-functions)
		- [The `new` operator](#the-new-operator)
		- [Dealing  with properties of an object](#dealing-with-properties-of-an-object)
		- [Augmenting Default Types](#augmenting-default-types)
	- [Functions](#functions)
		- [Functions Arguments](#functions-arguments)
		- [Functions used as _methods_](#functions-used-as-methods)
		- [Functions used as _functions_](#functions-used-as-functions)
		- [Functions used as constructors](#functions-used-as-constructors)
		- [Functions invoked with a different context](#functions-invoked-with-a-different-context)
		- [IIFE Immediately Invoked Function Expressions](#iife-immediately-invoked-function-expressions)
	- [Exceptions](#exceptions)
	- [Recursion](#recursion)
	- [Closure](#closure)
		- [Closure to Hide Singletons](#closure-to-hide-singletons)
		- [Closure to Make Safe Objects](#closure-to-make-safe-objects)
		- [Closure to Make Modules](#closure-to-make-modules)
	- [Objects & Inheritance](#objects-inheritance)
		- [Classical Pattern](#classical-pattern)
		- [The ECMASript 5 Pattern](#the-ecmasript-5-pattern)
		- [The Differential Pattern](#the-differential-pattern)
		- [The Functional Pattern](#the-functional-pattern)
	- [Arrays](#arrays)
	- [Regexp](#regexp)
	- [JSON](#json)
<!-- /TOC -->


## Syntax


JavaSript has a c-based syntax with lots of idioms borrowed from Java.

### Variables

Variables are dynamically typed but need to be declared with the `var` keyword:

```javascript
var i;
var j = 0;
var k = 1, l = j+k;
```

### Comments

```javascript
/*
    C-Style multiline comment
 */

// C-Style single line comment
```

### Names

One letter or underscore optionally followed by one or more letters, digits, underscores.

### Reserved Words

Most of them are not used.

`abstract boolean break byte case catch char class const continue debugger default delete do double else enum export extends false final finally float for function goto if implements import in instanceof int interface long native new null package private protected public return short static super switch synchronized this throw throws  transient true try typeof var volatile void while with`

## Numbers

`Number` is the single type for all numerical values. No integers, float, double, etc. Only numbers. A number is composed of :

-	an integer part, e.g. `123`,
-	followed by an optional fraction part, e.g. `123.456`
-	followed by an optional exponent part, e.g. `123.456e+7`

### Numbers Encoding Format

-	64 bits floats (Java doubles)
-	No integers, 1 is the same value as 1.0.
-	Arithmetic is not exact, ( 0.1 + 0.2 !== 0.3) as in all programming languages...

### NaN

`NaN` is a value that results from an operation producing abnormal arithmetic result.

:warning: `NaN` can't be tested against itself:

```javascript
Math.sqrt(-2) === NaN; // false
```

isNaN(number) is used to spot NaNs.

```javascript
isNaN(Math.sqrt(-2)); // true
```

### Infinity

```javascript
Infinity > 1.79769313486231570e+308 // true
```

### Utility functions

Utility functions and constants are available through the Math object.

```javascript
Math.floor(3.45); // 3
Math.random();  // 0.22312605078332126
Math.PI; // 3.141592653589793
Math.sin(Math.PI/2); // 1
```

### Parse Strings to Numbers

```javascript
parseInt(string, base);
parseInt('345€', 10); // 345
parseInt('$345', 10); // 'undefined'
parseInt('8'); // 8
parseInt('08'); // 0 -> leading 0 is understood as octal base
parseInt('08', 10); // 8 -> always give the base!!!
```

## Strings


Strings are immutable objects.

### String Literals

Written between single or double quotes ( 'this string', "that string").

-	The empty string '' is allowed (0 characters).
-	No char type. We use one-character strings ( 'a').

### Escaped Characters

-	`\`(backslash) escapes characters.
-	`\\ \' \' \n \/ \t \b \f \r \u0065`

### unicode

-	Strings are 16 bits unicode characters.
-	`'\u004A \u0053 \u062D \u0F1C \u3FEF \u0DF4' === 'J S ح ༜ 㿯 ෴'`
-	Characters above '\uFFFF' need 2 JS characters.

### Concatenation

The `+` operator has 2 functions:

-	concatenation of strings
-	and addition of numbers.

```javascript
'J' + 'S' === 'JS' // true
```

The concatenation has the priority over the addition. Addition will occure only if the two operators are numbers. In any other case, concatenation will occure.

```javascript
'HTML' + 10 / 2 === 'HTML5' // true
```

### Length

String objects have a `length` property that represents the number of 16-bits unicode characters in that string.

```javascript
 '€\u5555ñ'.length === 3 // true

'€\u5555ñ' === '€啕ñ' // true
```

### String Methods

The String **pseudo-class** has methods.

Since strings are immutable, methods are static and only return new objects (no modification).

```javascript
var s = 'ok/ko';
var s1 = s;
s += '/ok'; // 'ok/ko/ok' but strings are immutable, so s is a new object.
s1; // 'ok/ko' The original object remains unchanged.

s1.toUpperCase(); // 'OK/KO'
s1.split('/'); // [ 'ok', 'ko' ]
s1.replace('/', ' ≠ '); // 'ok ≠ ko'
'one, two , three'.split(/\s*,\s*/); // [ 'one', 'two', 'three' ]
String.fromCharCode(74, 83) // 'JS'
```

## Control Flow


Classical C-Style Block statements.

### if/else

```javascript
if (expression) {
    // statements;
} else if (expression) {
    // statements;
}
```

### for

```javascript
var i; // at beginning of function
// ...
for (i = 0; i < 10; i += 1) {
    // statements;
}
for (i in obj) {
    // statements;
}
```

### while

```javascript
var i; // at beginning of function
// ...
i = 0;
while (i < 10) {
    // statements;
}
```

### switch

```javascript
switch (expression) {
    case expression:
        // statements;
        break;
    default:
        // statements;
}
```

## Expressions


Literals, names, operators and other expressions.

### Operators Precedence

| Operator                  | comment                                         |
|---------------------------|-------------------------------------------------|
| `. [] ()`                 | Refinement and invocation                       |
| `delete new typeof - + !` | Unary operators                                 |
| `* / %`                   | Multiplication, division, modulo                |
| `+ -`                     | Addition (or string concatenation), subtraction |
| `<= < >= >`               | Inequalities                                    |
| `=== !==`                 | Equality                                        |
| `&&`                      | Logical AND                                     |
| `||`                      | Logical OR                                      |
| `?:`                      | Ternary operator                                |

### Refinement

```javascript
object.property;
object['property'];
```

### Invocation

```javascript
my_function(param1, param2);
```

Literals
--------

### Objects

```javascript
{
    property1: 'value1',
    my_property: true,
    '% of value': 23
}
```

### Arrays

```javascript
['a', 'b', 'c', 3, true, my_obj]
```

### Regexp (borrowed from perl)

```javascript
/^[a-zA-Z_][a-zA-Z_0-9]*$/ // recognizes javascript 'names'
```

### Functions

```javascript
function my_function(p1, p2) {
    // var statements;
    // statements;
}
```

### Anonymous functions

```javascript
some_function(p1, p2, function(){
    // var statements;
    // statements;
});
```



## Scope
Although being a block-based syntax language, JavaSript does not have block scope. Javascript has **function scope**.

Functions get access to the context (surrounding variables) they are defined within.

```javascript
function f () {
    var a = 10, b = 2;
    function f2() {
        var b = 20, c = 2;
        // a : 10,  b : 20,  c : 2
    }
    f2();
    // a : 10,  b : 2,  'c' exists but is undefined
    if (a > 0) {
        var c = 34;
        b = 25;
        // a : 10, b : 25, c : 34
    }
    // a : 10, b : 25, c : 34
}
f();
```
[A function scope extended example.](http://codepen.io/pigne/pen/LhHEo)

## Strict Mode


Strict Mode is a restricted variant of Javascript defined in EcmaScript 5. It is activated per-function adding the string `'strict mode';` in the body of the function.

It is adviced not to use strict mode on the global scope in order to avoid imported non-strict dependencies and other files to be treated as strict mode.

```javascript
function myFunction(){
    'use strict';
    // instructions...
}
```

-	Some silent errors become throw errors

	```javascript
	forgotTheVar = 17; // throws a ReferenceError
	delete Object.prototype; // throws a TypeError
	var o = { p: 1, p: 2 }; // !!! syntax error
	function sum(a, a, c){ /* ... */ }// !!! syntax error
	var sum = 015; // !!! syntax error
	```

-	Some dangerous or slow structures are forbidden

	```javascript
	function f() {
	    'use strict';
	    var o = { x:17 };
	    with (o) { console.log(x); } // !!! syntax error
	}
	var x = 17;
	var evalX = eval(''use strict'; var x = 42; x');
	x === 17;  // true
	evalX === 42; // true
	```

-	Use of restricted words raises errors (class, enum, export, extends, import, super)

## Objects


-	Numbers, strings, booleans, `null` and `undefined` are simple and immutable types.
-	All other values are **objects**.
-	Objects are **mutable** dictionaries (Java's hashtables, Python's dicts).
-	An object is a container for **properties**.
-	A property has a **name** and a **value**. A name of a property can be any string (quotes are optional if name matches `/^[a-zA-Z_][a-zA-Z_0-9]*$/`).
-	A value of a property can be any JS value except for `undefined`.

### Object Literal

```javascript
var w = {
    '°C': 27,
    humidity: '80%',
    place: 'Le Havre'
}
```

### Access to properties

```javascript
w['°C']; // 27
w.humidity; // '80%'
w.pressure; // undefined
w.pressure = 1030;
w.place = 'Nice';
```

### Objects are passed by reference

```javascript
var w2 = w;
w['°C']=34;
w2['°C']; // 34
```

## Prototype


-	Every object inherits properties from a *prototype object*.
-	Object literals are linked to `Object.prototype`.
-	New objects can have any object as a prototype.
-	Accessing an object's property is a recursive search into the prototype chain.
-	Recursively, all objects inherit from `Object.prototype`.

-	object

	-	properties
	-	prototype
		-	properties
		-	prototype
			-	...
			-	...

Example:

```javascript
var o = {
    'a': 0,
    'b': false
};
Object.prototype.ok = function() {
    return 'That\'s OK!';
};
Object.prototype.not_ok = 'Not OK.';
o.ok(); // 'That's OK!'
o.not_ok; // 'Not OK.'
```

Searching the prototype chain: - object `o` - properties `{'a':0, 'b':false}` - prototype `Object.prototype` - properties `{ ok: [Function], not_ok: 'Not OK.'}` - prototype `undefined`

Creation of new Objects
-----------------------

Several technics allow the creation of new objects. The most common uses *Constructor Functions* and the `new` operator.

### Constructor Functions

Like an ordinary function, with a capital first Letter name (convention) The function body can be described as the constructor of the new object. The new object's properties can be accessed/defined in the constructor with the `this` special value.

```javascript
function Point() {
    this.x = 0;
    this.y = 0;
    this.toString = function() {
        return '('+ this.x + ', ' + this.y + ')';
    };
}
```

### The `new` operator

The `new` creates new objects using a *Constructor Function*.

It gives newly created objects properties referred to by `this` in the body of the *Constructor Function*.

```javascript
var p1 = new Point();
p1; // { x: 0, y: 0, toString: [Function] }
```

:warning: The `new`operator uses the *Constructor Function*'s `prototype` property to initialise the new object's *prototype*.

A *Constructor Function* is an object like an other JS object. It has *properties* an a *prototype*.

| Object     | `Point`              |
|------------|----------------------|
| Properties | `prototype: {}`      |
| Prototype  | `Function.prototype` |

| Object     | `p1`                                   |
|------------|----------------------------------------|
| Properties | `x: 0, y: 0, toString: [Function] `    |
| Prototype  | `Point.prototype`                      |

-	The special class method `Object.getPrototypeOf(object)` retrieves an object's prototype.
    ```javascript
	Object.getPrototypeOf(p1) === Point.prototype
	```

-	Changing an object's properties does not change its prototype object.
    ```javascript
	p1.z = 0;
	Point.prototype.z; // undefined
	```

-	:warning: Changing an object's prototype will change all the objects that use this prototype!
    ```javascript
    var p2 = new Point();
    p2.z; // undefined
    var proto = Object.getPrototypeOf(p1); // {}
    proto.z = -1;
    p1.z; // -1
    p2.z; // -1
    Point.prototype; // { z: -1 }
    ```

### Dealing  with properties of an object

The `for in` statement iterates through the properties of an object.

```javascript
var prop;
for (prop in p1){
    console.log(prop+' : '+p1[prop]);
}
```


The for `in loop` might bring properties inherited from the prototype chain. `hasOwnProperty` filters only properties (not function) belonging to that object.

```javascript
for(var prop in options) {
    if(options.hasOwnProperty(prop) && this.hasOwnProperty(prop)) {
        this[prop] = options[prop];
    }
}
```

Delete a property from an object. Cannot affect properties from the prototype.
```javascript
delete p1.x; // true
p1.x; // undefined
```



### Augmenting Default Types

Preexisting objects also have a prototype link that can be accessed.

The String `pseudo-class` can be augmented. We call it a pseudo-class because it does not create real mutable objects. Indeed strings are immutable.

```javascript
 String.prototype.trim = function() {
    return this.replace(/^\s*|\s*$/, '');
};

' Ok then     '.trim(); // 'Ok then'

Number.prototype.integer = function() {
    return Math[this >= 0 ? 'floor' : 'ceil'](this);
};

(2.34).integer(); // 2
(-Math.PI).integer(); // -3
```



## Functions


- Functions are objects.
- Functions are linked to `Function.prototype` (which is itself linked to `Object.prototype`).
- Functions have a `prototype` property, different from the *prototype link*.
- Used by Constructor Functions to define newly created objects' prototype.
- Nothing differentiates CF from non-CF so all functions have it.
- Functions have a link to the object which invokes them: `this`.


###  Functions Arguments

In JavaSript, matching functions' declared argument during a call is not mandatory. No error is raised when parameters are omitted. The hidden object `arguments` holds the given parameters.

```javascript
function f(a) {
    for (var i = 0; i < arguments.length; i++) {
        console.log(i + '=>' + arguments[i]);
    }
}
f('ok',false) //  0=>ok
//  1=>false
```


Arguments list order can be tricky to handle. _Option objects_ should be used to identify parameters.

```javascript
var obj1 = new Object1( w, h, c, o, s);
var obj2 = new Object2({
    width : w,
    height : h,
    color: c,
    opacity: o,
    shadow: s
});
```

### Functions used as _methods_

When belonging to an object _and_ being invoked by that object, functions are _methods_.
the parameter `this` refers to the object that owns the method.
```javascript
 var p1 = {
    x: 10,
    y: 10,
    toString: function() { /* definition of a method */
        return '(' + this.x + ', ' + this.y + ')';
    }
};
// invocation of 'toString' as a method
p1.toString(); // '(10, 10)'
```

### Functions used as _functions_

If not bounded to an object, functions are bounded to the _global scope_. In that case, `this` refers to the global scope and not to the calling context.

```javascript
var my_name_is = 'This is global!';
function f() {
    var my_name_is = 'This is local to f()';
    function print_name() {
        console.log(this.my_name_is); // don't do that!
    }
    print_name();
}
f(); // 'This is global!'

```


###Functions used as constructors



When used as a constructor, a function is called  a _Constructor Function_. By convention a CF has an upper cased first letter. _Constructor Functions_ are used in conjunction with the `new` operator. The `new` operator creates a fresh object and apply the CF to that object. The  `this` pointer refers to that new object. is meant to refer to the new object.

:warning: This function's `prototype` property is used to initialize the new object's _prototype link_.

If no return statement or if the function doesn't return an object, then this is automatically returned.

```javascript
 function Point(x, y) {
    this.x = x || 0;
    this.y = y || 0;
}
Point.prototype.toString = function() {
    return '('+ this.x + ', ' + this.y + ')';
};
var p = new Point();
```



### Functions invoked with a different context

Functions are objects, and objects can have functions (methods).  Then Functions have methods.

Their exists a `Function` function. has it has a capital 'F' you can guess it is a _Constructor Function_. The `Function.prototype` property is used as a _prototype link_ to any function.

 The `apply` method belongs to  `Function.prototype`. Following the prototype chain, any function can call  the `apply`  method.

`apply` invokes the function with a given context (`this`) as a parameter.

```javascript
var weirdo = {
    x: '\u03B1',
    y: '\u03B2'
}

Point.prototype.toString.apply(weirdo); // '(α, β)'
p.toString.apply(weirdo); // '(α, β)'
```


### IIFE Immediately Invoked Function Expressions

Use immediately invoked function expressions to prevent polluting the global scope.

```javascript
var a = 1;
(function(){
    var a = 0
    console.log(a); // 0
})();
console.log(a); // 1
```




## Exceptions

 Exceptions are meant to interrupt abnormally behaving programs.

- Thrown with the `throw` statement.
- Caught with the `try` / `catch` statements.

```javascript
 function Point(x, y) {
    if ((typeof x !== 'undefined' && typeof x !== 'number')
    || (typeof y !== 'undefined'  && typeof y !== 'number')) {
        throw { name: 'TypeError', message: ''Point' needs numbers' };
    }
    // ...
}
(function() {
    try {
        var weird = new Point('\u03B1', 0);
    } catch (e) {
        console.log(e.name + ': ' + e.message);
    }
})(); // TypeError: 'Point' needs numbers
```


## Recursion

Possible but slow. No tail optimization for self calling functions.
```javascript
 function fib(n) {
    if (n <= 2) {
        return 1;
    }
    return fib(n - 1) + fib(n - 2);
}
```
[Recursion demo on CodePen.](http://codepen.io/pigne/pen/edLBE)


## Closure

Functions have access to the variables and parameters of the function that defined them. They have access to the scope that was available during their creation.

A function can be exported to another context (another scope) and still have access to its original scope.


An inner function may live longer than its outer function.
```javascript
function f_outer() {
    function f_inner() {
        return 'Inner function';
    }
    return f_inner;
}
var f = f_outer(); // f_inner
f(); // 'Inner function'
```

Inner functions encapsulate states of outer functions for a latter invocation.

```javascript
function increment() {
    var counter = 0;
    return function() {
        counter = counter + 1;
        return counter;
    };
}
var my_increment = increment();
my_increment(); // 1
my_increment(); // 2
my_increment(); // 3
my_increment(); // 4
counter; // undefined
```

### Closure to Hide Singletons

```javascript
function html_to_md() {
    var tokens = {
        'p': '\n',
        '/p': '\n',
        'h1': '# ',
        '/h1': '\n',
        // ...
    };
    return function(html) {
        return html.replace(/<([^<>]+)>/g, function(a, b) {
            var t = tokens[b];
            return typeof t === 'string' ? t : a;
        });
    };
}
var parse = html_to_md();
parse('<h1>My Title</h1><h2>Subtitle<...'); // # My Title\n ## Subtitle\n...
```
An extended example of [hidden singletons and utilities](http://codepen.io/pigne/pen/HtqjF).

### Closure to Make Safe Objects

By default, objects properties are always visible and writable. Inner Functions and closure can create objects with 'private' members.

```javascript
 function createPoint() {
    var x = 0;
    var y = 0;
    // ...
    return {
        getX: function() {
            return x;
        },
        setX: function(new_x) {
            check_number(new_x);
            x = new_x;
        },
        // ...
    };
}
var p = createPoint(); // { getX: [Function], setX: [Function], ... }
```
`p` is a new object created without the 'new' operator.

```javascript
p.x; // undefined
```
`x` is not part of `p`'s inheritance chain but is accessible from `p`'s functions scope.

```javascript
p.getX(); // 0
p.setY(-12);
p.toString(); // '(0, -12)'
```

A complete example of [safe objects create with closure](http://codepen.io/pigne/pen/DsEnA).

###Closure to Make Modules
```javascript
var prop;
(function(global) {
    global.MY_MODULE = global.MY_MODULE || {};
    // private API
    function hidden_function() {
        console.log('You called a hidden function.');
    }
    // public API
    global.MY_MODULE.publicFunction = function() {
        console.log('Public function calling a hidden one...');
        hidden_function();
    };
})(this);

for (prop in MY_MODULE) {
    console.log(prop);
}
MY_MODULE.publicFunction(); // Public function calling a hidden one...
// You called an hidden function.
```

## Objects & Inheritance

### Classical Pattern

**Pros**:
- It's the classical way to do. Easy to read and understand. Any JS developer knows it.
**Cons**:
- Manipulating _Constructor Functions_ and the `new` operator is risky.
- All members are public.
- Parameters and inheritance are problematic.

```javascript
 var p,
    Point3D = function() {
        this.z = 0;
    };
Point3D.prototype = new Point();
Point3D.prototype.toString = function() {
    return '(' + this.x + ', ' + this.y + ', ' + this.z + ')';
};
p = new Point3D();
p.x = p.y = p.z = -3;
p.toString(); // '(-1, -2, -3)';
```
A complete example of [Objects Inheritance with the Classical Pattern](http://codepen.io/pigne/pen/fkczG).


### The ECMASript 5 Pattern

[TODO]

### The Differential Pattern

Create new objects from existing ones.

Specify differences from a base object in ordrer to specify (specialise) another one.

**Pros**:

- can hide Constructor Functions and new operators.

**Cons**:

- objects are linked (if base object changes, then inherited objects change too).

```javascript
function createObject(base) {      // Utility function to
    function F() {};               // create objects with
    F.prototype = base;            // 'base' as a prototype.
    return new F();
}
var point = { x: 0, y: 0 },        // A 'base' object.
p3d = createObject(point);         // New object with 'point' as its prototype.
p3d.z = 0;                         // Differences from 'point'.
p3d.toString = function() {
    return '(' + this.x + ', ' + this.y + ', ' + this.z + ')';
};
p3d.toString(); // '(0, 0, 0)'
```

An example of [Object Inheritance with the differential pattern](http://codepen.io/pigne/pen/tLHFA).


### The Functional Pattern

Some classical function returns new objects with public methods in it.

Public methods access hidden attributes thanks to closure.

That function is called as a regular function (no `new` operator).

```javascript
var createPoint = function(attributes) {
    attributes = attributes || {};
    attributes.x = attributes.x || 0; // Hidden attributes, given as parameters.
    attributes.y = attributes.y || 0;
    // ...
    var point = {}; // The new object to be returned.

    point.toString = function() { // public methods accessing hidden parameters.
        return '(' + attributes.x + ', ' + attributes.y + ')';
    };
    // ...
    return point; // return the newly created object.
};
var p1 = createPoint({ x: -1, y: -4 });
```



Inheritance is simply done by:

- using a create function into another,
- sharing the attributes to initialize to new object.

```javascript
var createPoint3D = function(attributes) {
    attributes = attributes || {};
    attributes.z = attributes.z || 0;
    var point3D = createPoint(attributes); // create a new object from upper hierarchy

    point3D.toString = function() {
        return '(' + attributes.x + ', ' + attributes.y + ', ' + attributes.z + ')';
    };
    // ...
    return point3D;
};
var p3d = createPoint3D({ x: -3, y: -3, z: -4 });
```

An example of [Object Inheritance with the functionnal pattern](http://codepen.io/pigne/pen/EajDd).

Code reuse or access to super members can be done with the apply invocation pattern.
```javascript
var createAugmentedPoint3D = function(attributes) {
    attributes = attributes || {};
    attributes.width = attributes.width || '1px';
    attributes.color = attributes.color || '#00FF00';
    var augmentedPoint3D = createPoint3D(attributes);
    var superToString = augmentedPoint3D.toString;  /* Store the super toString
                                                       method locally.*/

    augmentedPoint3D.toString = function() {        /* Shadow super toString
                                                       and call it with 'apply' */
    return '{' + superToString.apply(augmentedPoint3D) + ', width:' +
        attributes.width + ', color:' + attributes.color + '}';
    };
    return augmentedPoint3D;
};
var ap3d = createAugmentedPoint3D({ color: '#b3e4a2' });
ap3d.toString(); // '{(0, 0, 0), width:1px, color:#b3e4a2}'
```



## Arrays


## Regexp


## JSON
