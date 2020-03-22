# code guidelines
<!-- TOC -->autoauto- [code guidelines](#code-guidelines)auto    - [Variables](#variables)auto        - [Use meaningful and readable variable names](#use-meaningful-and-readable-variable-names)auto        - [Avoid using unary increments and decrements (++, --)](#avoid-using-unary-increments-and-decrements----)auto    - [References](#references)auto        - [Use const for all of your references; avoid using var](#use-const-for-all-of-your-references-avoid-using-var)auto        - [If you must reassign references, use let instead of var](#if-you-must-reassign-references-use-let-instead-of-var)auto    - [Object](#object)auto        - [Use object method shorthand](#use-object-method-shorthand)auto        - [Use property value shorthand](#use-property-value-shorthand)auto        - [Only quote properties that are invalid identifiers](#only-quote-properties-that-are-invalid-identifiers)auto        - [Prefer the object spread operator over Object.assign to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted(展开操作符和剩余操作符)](#prefer-the-object-spread-operator-over-objectassign-to-shallow-copy-objects-use-the-object-rest-operator-to-get-a-new-object-with-certain-properties-omitted展开操作符和剩余操作符)auto    - [Array](#array)auto        - [Use array spreads ... to copy arrays](#use-array-spreads--to-copy-arrays)auto        - [To convert an iterable object to an array, use spreads ... instead of Array.from.](#to-convert-an-iterable-object-to-an-array-use-spreads--instead-of-arrayfrom)auto        - [Use Array.from for converting an array-like object to an array](#use-arrayfrom-for-converting-an-array-like-object-to-an-array)auto        - [Use Array.from instead of spread ... for mapping over iterables, because it avoids creating an intermediate array.](#use-arrayfrom-instead-of-spread--for-mapping-over-iterables-because-it-avoids-creating-an-intermediate-array)auto    - [Destructuring(解构赋值)](#destructuring解构赋值)auto        - [Use object destructuring when accessing and using multiple properties of an object（避免创建临时引用）](#use-object-destructuring-when-accessing-and-using-multiple-properties-of-an-object避免创建临时引用)auto        - [Use array destructuring](#use-array-destructuring)auto    - [strings](#strings)auto        - [Use single quotes '' for strings](#use-single-quotes--for-strings)auto        - [When programmatically building up strings, use template strings instead of concatenation.(模板字符串)](#when-programmatically-building-up-strings-use-template-strings-instead-of-concatenation模板字符串)auto    - [Functions](#functions)auto        - [Never use arguments, opt to use rest syntax ... instead](#never-use-arguments-opt-to-use-rest-syntax--instead)auto        - [Use default parameter syntax rather than mutating function arguments](#use-default-parameter-syntax-rather-than-mutating-function-arguments)auto        - [Never reassign parameters](#never-reassign-parameters)auto    - [Arrow Functions](#arrow-functions)auto        - [When you must use an anonymous function (as when passing an inline callback), use arrow function notation(匿名函数)](#when-you-must-use-an-anonymous-function-as-when-passing-an-inline-callback-use-arrow-function-notation匿名函数)auto        - [Always include parentheses around arguments for clarity and consistency.(参数加括号)](#always-include-parentheses-around-arguments-for-clarity-and-consistency参数加括号)auto        - [Don’t save references to this. Use arrow functions](#dont-save-references-to-this-use-arrow-functions)auto    - [Classes & Constructors](#classes--constructors)auto        - [Always use class. Avoid manipulating prototype directly](#always-use-class-avoid-manipulating-prototype-directly)auto        - [Use extends for inheritance](#use-extends-for-inheritance)auto        - [Methods can return this to help with method chaining](#methods-can-return-this-to-help-with-method-chaining)auto    - [Modules](#modules)auto        - [Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system](#always-use-modules-importexport-over-a-non-standard-module-system-you-can-always-transpile-to-your-preferred-module-system)auto        - [Do not use wildcard imports](#do-not-use-wildcard-imports)auto        - [In modules with a single export, prefer default export over named export](#in-modules-with-a-single-export-prefer-default-export-over-named-export)auto        - [Do not include JavaScript filename extensions](#do-not-include-javascript-filename-extensions)auto    - [Comparison Operators & Equality](#comparison-operators--equality)auto        - [Use === and !== over == and !=](#use--and--over--and-)auto        - [Use shortcuts for booleans, but explicit comparisons for strings and numbers](#use-shortcuts-for-booleans-but-explicit-comparisons-for-strings-and-numbers)auto        - [When mixing operators, enclose them in parentheses. The only exception is the standard arithmetic operators: +, -, and ** since their precedence is broadly understood. We recommend enclosing / and * in parentheses because their precedence can be ambiguous when they are mixed(提高可读性)](#when-mixing-operators-enclose-them-in-parentheses-the-only-exception-is-the-standard-arithmetic-operators----and--since-their-precedence-is-broadly-understood-we-recommend-enclosing--and--in-parentheses-because-their-precedence-can-be-ambiguous-when-they-are-mixed提高可读性)auto    - [Comments](#comments)auto        - [Use /** ... */ for multiline comments.](#use----for-multiline-comments)auto        - [Use // for single line comments](#use--for-single-line-comments)auto        - [Use // FIXME: to annotate problems](#use--fixme-to-annotate-problems)auto        - [Use // TODO: to annotate solutions to problems](#use--todo-to-annotate-solutions-to-problems)auto    - [Semicolons](#semicolons)autoauto<!-- /TOC -->
## Variables
### Use meaningful and readable variable names
```javascript
// bad
var yyyymmdstr = moment().format('YYYY/MM/DD');

// good
var yearMonthDay = moment().format('YYYY/MM/DD');
```

### Avoid using unary increments and decrements (++, --)
```javascript
// bad

const array = [1, 2, 3];
let num = 1;
num++;
--num;

let sum = 0;
let truthyCount = 0;
for (let i = 0; i < array.length; i++) {
  let value = array[i];
  sum += value;
  if (value) {
    truthyCount++;
  }
}

// good

const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;
```

## References
### Use const for all of your references; avoid using var
```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

### If you must reassign references, use let instead of var
```javascript
// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
```

## Object
### Use object method shorthand
```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

### Use property value shorthand
```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};
```

### Only quote properties that are invalid identifiers
```javascript
// bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

### Prefer the object spread operator over Object.assign to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted(展开操作符和剩余操作符)
```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

## Array
The Array.from() method creates a new, shallow-copied Array instance from an array-like or iterable object.
```javascript
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

### Use array spreads ... to copy arrays
```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

### To convert an iterable object to an array, use spreads ... instead of Array.from.
```javascript
const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```

### Use Array.from for converting an array-like object to an array
```javascript
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

// bad
const arr = Array.prototype.slice.call(arrLike);

// good
const arr = Array.from(arrLike);
```

### Use Array.from instead of spread ... for mapping over iterables, because it avoids creating an intermediate array.
```javascript
// bad
const baz = [...foo].map(bar);

// good
const baz = Array.from(foo, bar);
```

## Destructuring(解构赋值)
### Use object destructuring when accessing and using multiple properties of an object（避免创建临时引用）
```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

### Use array destructuring
```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

## strings
### Use single quotes '' for strings
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```

### When programmatically building up strings, use template strings instead of concatenation.(模板字符串)
```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

## Functions
###  Never use arguments, opt to use rest syntax ... instead
```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```

### Use default parameter syntax rather than mutating function arguments
```javascript
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```

### Never reassign parameters
```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}
```

## Arrow Functions
### When you must use an anonymous function (as when passing an inline callback), use arrow function notation(匿名函数)
```javascript
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

### Always include parentheses around arguments for clarity and consistency.(参数加括号)
```javascript
// bad
[1, 2, 3].map(x => x * x);

// good
[1, 2, 3].map((x) => x * x);
```
### Don’t save references to this. Use arrow functions
```javascript
// bad
function foo() {
  const self = this;
  return function () {
    console.log(self);
  };
}

// bad
function foo() {
  const that = this;
  return function () {
    console.log(that);
  };
}

// good
function foo() {
  return () => {
    console.log(this);
  };
}
```

## Classes & Constructors
### Always use class. Avoid manipulating prototype directly
```javascript
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

### Use extends for inheritance
```javascript
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};

// good
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}
```

### Methods can return this to help with method chaining
```javascript
// bad
Jedi.prototype.jump = function () {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function (height) {
  this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();

luke.jump()
  .setHe
```

## Modules
### Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system
```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

### Do not use wildcard imports
```javascript
// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// good
import AirbnbStyleGuide from './AirbnbStyleGuide';
```

### In modules with a single export, prefer default export over named export
```javascript
// bad
export function foo() {}

// good
export default function foo() {}
```

### Do not include JavaScript filename extensions
```javascript
// bad
import foo from './foo.js';
import bar from './bar.jsx';
import baz from './baz/index.jsx';

// good
import foo from './foo';
import bar from './bar';
import baz from './baz';
```

## Comparison Operators & Equality
### Use === and !== over == and !=
### Use shortcuts for booleans, but explicit comparisons for strings and numbers
```javascript
// bad
if (isValid === true) {
  // ...
}

// good
if (isValid) {
  // ...
}

// bad
if (name) {
  // ...
}

// good
if (name !== '') {
  // ...
}

// bad
if (collection.length) {
  // ...
}

// good
if (collection.length > 0) {
  // ...
}
```

### When mixing operators, enclose them in parentheses. The only exception is the standard arithmetic operators: +, -, and ** since their precedence is broadly understood. We recommend enclosing / and * in parentheses because their precedence can be ambiguous when they are mixed(提高可读性)
```javascript
// bad
const foo = a && b < 0 || c > 0 || d + 1 === 0;

// bad
const bar = a ** b - 5 % d;

// bad
// one may be confused into thinking (a || b) && c
if (a || b && c) {
  return d;
}

// bad
const bar = a + b / c * d;

// good
const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

// good
const bar = a ** b - (5 % d);

// good
if (a || (b && c)) {
  return d;
}

// good
const bar = a + (b / c) * d;
```

## Comments
### Use /** ... */ for multiline comments.
### Use // for single line comments
### Use // FIXME: to annotate problems
### Use // TODO: to annotate solutions to problems

## Semicolons
为避免出现古怪的错误，在换行符之前在代码中放置分号
