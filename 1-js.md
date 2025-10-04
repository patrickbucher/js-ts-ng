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

