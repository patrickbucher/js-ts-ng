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

