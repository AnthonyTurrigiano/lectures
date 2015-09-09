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

:attention: `NaN` can't be tested against itself:

```javascript
Math.sqrt(-2) !== NaN; // true
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
"one, two , three".split(/\s*,\s*/); // [ 'one', 'two', 'three' ]
String.fromCharCode(74, 83) // "JS"
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

literals, names, operators and other expressions.

### Operators Precedence

| operators                 | comment                                         |
|---------------------------|-------------------------------------------------|
| `. [] ()`                 | Refinement and invocation                       |
| `delete new typeof - + !` | Unary operators                                 |
| `* / %`                   | Multiplication, division, modulo                |
| `+ -`                     | Addition (or string concatenation), subtraction |
| `<= < >= >`               | Inequalities                                    |
| `=== !==`                 | Equality                                        |
| `&&`                      | Logical AND                                     |
| \`                        |                                                 |
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

Objects
-------

Functions
---------

Inheritance
-----------

Arrays
------

Regexp
------

JSON
----
