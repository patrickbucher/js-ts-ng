# Eloquent JavaScript

## Values, Types, and Operators

The `typeof` operator returns the type of an expression as a string:

    > typeof true
    'boolean'
    > typeof "hello"
    'string'
    > typeof 4.5
    'number'
    > typeof NaN
    'number'
    > typeof Infinity
    'number'
    > typeof undefined
    'undefined'
    > typeof null
    'object'

Strings can be compared lexicographically (capital letters come first):

    > "ACDC" > "ABBA"
    true
    > "acdc" > "abba"
    true
    > "ACDC" > "abba"
    false

JavaScript automatically converts types upon comparison. USe `===` to compare without type conversion.

    > undefined == null
    true
    > undefined === null
    false

The `??` operator works similar to `||`, but only returns the right-hand value if the left-hand value is either `null` or `undefined`:

    > 0 || 'fallback'
    'fallback'
    > 0 ?? 'fallback'
    0
    > '' || 'fallback'
    'fallback'
    > '' ?? 'fallback'
    ''
    > false || 'fallback'
    'fallback'
    > false ?? 'fallback'
    false
    > undefined || 'fallback'
    'fallback'
    > null ?? 'fallback'
    'fallback'
    > undefined || 'fallback'
    'fallback'
    > null ?? 'fallback'
    'fallback'

## Program Structure

Parse a number and check if it worked:

    > let n = Number('123')
    > Number.isNaN(n)
    false
    > let s = Number('abc')
    > Number.isNaN(s)
    true

Use exponentiation:

    > 2 ** 3
    8

## Functions

-

## Data Structures: Objects and Arrays

The `obj.x` notation fetches a value named "x" from the object, while `obj[x]` evaluates `x` before the object is accessed.

Array modification methods:

| Method           | Semantics   | Position | Return Value                  |
|------------------|-------------|----------|-------------------------------|
| `push(item)`     | add item    | end      | new length                    |
| `item = pop()`   | remove item | end      | removed item (or `undefined`) |
| `unshift(item)`  | add item    | front    | new length                    |
| `item = shift()` | remove item | front    | removed item (or `undefined`) |

Properties can be removed from an object using `delete`:

    > let nums = { a: 3, b: 7 }
    > delete nums.a
    > nums
    { b: 4 }

The `in` operator returns whether or not an object has a property:

    > let food = { breakfast: 'toast', lunch: 'fries' }
    > 'breakfast' in food
    true
    > 'dinner' in food
    false

The `Object.keys` method returns the property names of an object:

    > Object.keys({ first: 'Patrick', last: 'Bucher' })
    [ 'first', 'last' ]

The `Object.assign` method allows to copy one object into another:

    > let drinks = { beer: 'Guinness', wine: 'Bordeaux' };
    > let foods = { starter: 'Salad', main: 'Cheesburger' };
    > Object.assign({}, foods, drinks);
    {
      starter: 'Salad',
      main: 'Cheesburger',
      beer: 'Guinness',
      wine: 'Bordeaux'
    }

Objects and Arrays compare by identity, not by their values.

If the property is to be named after its value's variable, the following syntax can be used:

    > hamster = 'Nibbles'
    > cat = 'Mittens'
    > { hamster, cat }
    { hamster: 'Nibbles', cat: 'Mittens' }

The `includes` method checks whether or not a value is included in an array:

    > [1,1,2,3,5,8,13].includes(4)
    false
    > [1,1,2,3,5,8,13].includes(5)
    true

The index of an item can be found using the `indexOf` method:

    > [2,4,8,16,32].indexOf(7)
    -1
    > [2,4,8,16,32].indexOf(8)
    2

The `lastIndexOf` methods searches from the end.

The `slice` method returns parts of an array bounded by lower (inclusive) and upper (exclusive) indices:

    > [2,4,8,16,32].slice(0, 3)
    [2,4,8]
    > [2,4,8,16,32].slice(3)
    [16,32]

Use `for`/`in` to loop over indices, and `for`/`of` to loop over values:

```javascript
const numbers = [2, 4, 8, 16, 32];
for (let i in numbers) {
  console.log(i);
}
for (let n of numbers) {
  console.log(n);
}
```

Use _rest parameters_ to accept a variable number of values:

```javascript
function mean(...numbers) {
  let total = 0;
  for (const n of numbers) {
    total += n;
  }
  return total / numbers.length;
}
const numbers = [1,2,3,4];
console.log(...numbers);
```

Arrays and objects can be destructured as function arguments:

```javascript
function greetPerson({ first, last }) {
  return `Hello, ${first} ${last}!`;
}

function formatTriplet([a, b, c]) {
  return `${a}²+${b}²=${c}²`;
}
```

If it's not certain that a property exists on an object, use the `?.` notation to get `undefined` for a non-existand property:

    > { a: 13, b: 16 }?.a
    13
    > { a: 13, b: 16 }?.c
    undefined

Use `JSON.stringify` to turn JavaScript values into JSON, and `JSON.parse` for the reverse conversion.

## Higher-Order Functions

Use `codePointAt` to get the unicode code point from a string:

    > 'Достоевский'.codePointAt(3)
    1090

A `for`/`of` loop over a string returns characters:

    > let name = 'Достоевский';
    > for (const c of name) { console.log(c); }
    Д
    о
    с
    т
    о
    е
    в
    с
    к
    и
    й

## The Secret Life of Objects

For functions defined using the `function` keyword or as methods, `this` refers to the surrounding object literal. However, for arrow functions, `this` is not bound:

```javascript
let person = {
  name: "Joe Doe",
  introduce: function () {
    return `Hello, my name is ${this.name}!`;
  },
  complain(about) {
    return `I, ${this.name}, don't like ${about}!`;
  },
  greet: (whom) => {
    return `Greetings, to ${whom} from ${this.name}!`;
  },
};

console.log(person.introduce()); // ok
console.log(person.complain("Dane Jone")); // ok
console.log(person.greet("Jane Done")); // error: Cannot read properties of undefined (reading 'name')
```

Use `Object.create` to create an object with a specific prototype:

```javascript
let protoPerson = {
  introduce() {
    return `Hello, my name is ${this.name}!`;
  },
};

let alice = Object.create(protoPerson);
let bob = Object.create(protoPerson);
alice.name = "Alice";
bob.name = "Bob";
console.log(alice.introduce());
console.log(bob.introduce());
```

Since 2015, JavaScript also supports classes:

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  introduce() {
    return `Hello, my name is ${this.name}!`;
  }
}

let charles = new Person("Charles");
let danielle = new Person("Danielle");
console.log(charles.introduce());
console.log(danielle.introduce());
```

Private properties and methods are prefixed with an `#`:

```javascript
class Athlete {
  #bmi;
  constructor(name, height, weight) {
    this.name = name;
    this.height = height;
    this.weight = weight;
    this.#bmi = this.#calcBMI();
  }
  #calcBMI() {
    return this.weight / this.height ** 2;
  }
  describe() {
    let rating;
    if (this.#bmi > 25) {
      rating = "overweight";
    } else if (this.#bmi > 20) {
      rating = "normal weight";
    } else {
      rating = "underweight";
    }
    return `${this.name} is ${this.height}m tall and ${this.weight}kg heavy (i.e. ${rating}).`;
  }
}

let patrick = new Athlete("Patrick", 1.88, 78.0);
console.log(patrick.describe());
```

Use `Map` and its methods `has`, `get`, `set` to manage key-value pairs. To use an object like a map, access its _own_ properties using `Object.keys`.

Prefix a method with `get` and `set` to control access to a property with the method's name, and `static` to declare methods to be accessed on the class rather than on its instances:

```javascript
class Weight {
  kilogramsInPounds = 2.20462262;
  constructor(kilograms) {
    this.kilograms = kilograms;
  }
  get pounds() {
    return this.kilograms * this.kilogramsInPounds;
  }
  set pounds(pounds) {
    this.kilograms = pounds / this.kilogramsInPounds;
  }
  static fromPounds(lbs) {
    return new Weight(lbs / kilogramsInPounds);
  }
}

let weight = new Weight(78);
console.log(weight.pounds);
weight.pounds = weight.pounds + 10;
console.log(weight.kilograms);
```

An _iterable_ is a class having a `[Symbol.iterator]` method; an _iteartor_ is a class having a `next` method that returns either `{ done: true }` if the iteration is finished, or `{ value, done: false }` if there are still values to be expected. A class can both be an _iterable_ and an _iterator_:

```javascript
class FibonacciIterator {
  constructor(max) {
    this.max = max;
    this.i = 0;
    this.n0 = 1;
    this.n1 = 1;
  }
  next() {
    let value;
    if (this.i == 0 || this.i == 1) {
      value = 1;
    } else {
      value = this.n0 + this.n1;
    }
    if (value > this.max) {
      return { done: true };
    }
    this.i++;
    this.n0 = this.n1;
    this.n1 = value;
    return { value: value, done: false };
  }
  [Symbol.iterator]() {
    return this;
  }
}

let fib = new FibonacciIterator(10);
for (let f of fib) {
  console.log(f);
}
```

Use `extends` to inherit from another class, which then can be accessed using `super`:

```javascript
class Circle {
  constructor(radius) {
    this.radius = radius;
  }
  circumference() {
    return 2 * this.radius * Math.PI;
  }
  area() {
    return this.radius ** 2 * Math.PI;
  }
}

class Cylinder extends Circle {
  constructor(radius, height) {
    super(radius);
    this.height = height;
  }
  volume() {
    return super.area() * this.height;
  }
}

let coin = new Circle(1.0);
let cigarette = new Cylinder(0.5, 7.0);
console.log(coin.circumference(), coin.area());
console.log(cigarette.volume());
```

## Bugs and Errors

The argument passed to `throw new Error(argument);` is accessible through the `message` property of the caught exception. Extend the `Error` class for own exceptions and compare caught exceptions using `instanceof` against that custom class.

## Regular Expressions

Create regular expressions using a constructor or in between forward slash characters, the latter of which requires less escaping:

```javascript
let numbers = new RegExp("[0-9]");
let letters = /[A-Za-z]/;
```

Use the `test` method to test for a match:

    > let chessCoord = /[a-h][1-8]/
    > chessCoord.test("b7")
    true
    > chessCoord.test("x9")
    false

Use the `u` suffix to unlock Unicode features:

- `\p{L}`: any letter
- `\p{N}`: any numeric character
- `\p{P}`: any punctuation character
- `\P{L}`: any non-letter (capital `P`)
- `\p{Script=SCRIPT}`: any character from a script

Example:

    > /\w/.test('Достоевсвий')
    false
    > /\p{L}+/u.test('Достоевсвий')
    true
    > /\p{Script=Cyrillic}/u.test('Достоевсвий')
    true

Use the `i` suffix to ignore lower/upper case.

Use `exec` to get hold of the resulting matches:

    > /([a-h])([1-8])/.exec("h3")
    [ "h3", "h", "3", index: 0, input: "h3", groups: undefined ]

The first element contains the whole match, the further elements the matched groups.

Use the `Date` constructor to create dates, and its `getTime` method to get a timestamp; use `Date.now()` to get the current timestamp:

    > new Date(1234567890000);
    2009-02-13T23:31:30.000Z 
    > new Date(2022, 6, 15, 8, 25, 13)
    2022-07-15T06:25:13.000Z
    > new Date(1987, 6, 24)
    1987-07-23T22:00:00.000Z
    > new Date(1987, 6, 24).getTime()
    554076000000
    > Date.now()
    1759938816573

Use look-ahead tests between `(?=` and `)` (positive) or `(?!` and `)` (negative) to match based on some input to follow:

    > /e(?=u)/.test('eudaimonia')
    true
    > /e(?=u)/.test('endangered')
    false
    > /e(?!u)/.test('eudaimonia')
    false
    > /e(?!u)/.test('endangered')
    true

The `replace` method for strings supports regular expressions:

    > 'damage'.replace(/[aeiou]/, '*')
    "d*mage"
    > 'damage'.replace(/[aeiou]/g, '*')
    "d*m*g*"

The second argument has direct access to the matched groups or can be a function:

    > "John Doe".replace(/(\w+) (\w+)/, "$&: $2, $1")
    "John Doe: Doe, John"
    > "3 + 5 = 8".replace(/\d/g, (m) => parseInt(m) * 2)
    "6 + 10 = 16"

