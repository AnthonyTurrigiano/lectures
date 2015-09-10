JavaSript Basics
================

In a nutshell:

-	Created by Brendan Eich at Netscape, in 1995.
-	The name comes from a cooperation with Sun Microsystems but it has nothing to do with Java.
-	Standardized by ECMA (ECMAScript Language Specification).
-	Interpreted language.
-	Dynamic typing.
-	Object Oriented language based on Prototypes.
-	Functional language with nested functions and closures.

Below is a detailed overview of the basis of the language. This presentation is heavily based on <cite><a href='http://www.maritimejournal.com/__data/assets/pdf_file/0020/1033940/Javascript-The-Good-Parts.pdf'>JavaScript: The Good Parts</a></cite> by Douglas Crockford. This more or less correspond to the fift version of the ECMAScript standard (ES5). The sixth version ES6 or ES2015 has many new features (classes, modules, arrow functions, etc.) that are not described here.

Syntax
------

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

Numbers
-------

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

Strings
-------

Strings are immutable objects.

### String Literals

Written between single or double quotes ( 'this string', 'that string').

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

Control Flow
------------

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

Expressions
-----------

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

Strict Mode
-----------

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

Objects
-------

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

Prototype
---------

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

Functions
---------

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
        console.log(i + "=>" + arguments[i]);
    }
}
f("ok",false) //  0=>ok
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
        return "(" + this.x + ", " + this.y + ")";
    }
};
// invocation of 'toString' as a method
p1.toString(); // "(10, 10)"
```

### Functions used as _functions_

If not bounded to an object, functions are bounded to the _global scope_. In that case, `this` refers to the global scope and not to the calling context.

```javascript
var my_name_is = "This is global!";
function f() {
    var my_name_is = "This is local to f()";
    function print_name() {
        console.log(this.my_name_is); // don't do that!
    }
    print_name();
}
f(); // 'This is global!'

```


###Functions used as constructors



When used as a constructor, a function is called  a _Constructor Function_. By convention a CF has an upper cased first letter. _Constructor Functions_ are used in conjuction with the `new` operator. The `new` operator creates a fresh object and apply the CF to that object. The  `this` pointer refers to that new object. is meant to refer to the new object.

:warning: This function's `prototype` property is used to initialize the new object's _prototype link_.

If no return statement or if the function doesn't return an object, then this is automatically returned.

```javascript
 function Point(x, y) {
    this.x = x || 0;
    this.y = y || 0;
}
Point.prototype.toString = function() {
    return "("+ this.x + ", " + this.y + ")";
};
var p = new Point();
```



### Functions invoked with a different context

Functions are objects, and objects can have functions (methods).  Then Functions have methods.

Their exists a `Function` function. has it has a capital "F" you can guess it is a _Constructor Function_. The `Function.prototype` property is used as a _prototype link_ to any function.

 The `apply` method belongs to  `Function.prototype`. Following the prototype chain, any function can call  the `apply`  method.

`apply` invokes the function with a given context (`this`) as a parameter.

```javascript
var weirdo = {
    x: "\u03B1",
    y: "\u03B2"
}

Point.prototype.toString.apply(weirdo); // '(α, β)'
p.toString.apply(weirdo); // '(α, β)'
```



Inheritance
-----------

Arrays
------

Regexp
------

JSON
----
