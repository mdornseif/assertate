# Assertate

> TypeScript 3.7 assertion helper library

## Requirements

| Requirement | Version   |
| ----------- | --------- |
| TypeScript  | `>=3.7.0` |

## About

A minimal library exposing basic
[TypeScript 3.7 assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions)
helpers.

## Installation

```sh
yarn add assertate
```

Or

```sh
npm install assertate
```

## Example

```typescript
import {
  assert,
  assertIsNumber,
  getAssertionMessage,
  getType,
  isNumber,
  isString,
  setAssertionMessage
} from "assertate";

////////////////////////////////////////////////////////////////////////////////
// use the `assertIs` functions for exception based assertions
////////////////////////////////////////////////////////////////////////////////
try {
  const someUndefinedVar: unknown = undefined;
  assertIsNumber(someUndefinedVar); // will throw an Error
} catch (err) {
  console.error(err); // An assertion Error will be logged
}

const someNumber: unknown = 123.456;
assertIsNumber(someNumber); // will not throw
const asFixedPointZero = someNumber.toFixed(0); // compiler now knows `someNumber` is a number and has all instance methods that a number has

////////////////////////////////////////////////////////////////////////////////
// use the `is` functions for control-flow based assertions
////////////////////////////////////////////////////////////////////////////////
const anotherNumber: unknown = 123.123;
if (isNumber(anotherNumber)) {
  // compiler now knows that in this if block, `anotherNumber` is a number
  const anotherNumberAsFixedPointZero = anotherNumber.toFixed(0);
}

////////////////////////////////////////////////////////////////////////////////
// General assertion
// - use the `assert` function if you need to compose more custom assertions
////////////////////////////////////////////////////////////////////////////////
const someNumberOrString: unknown = "123";
assert(isNumber(someNumberOrString) || isString(someNumberOrString)); // compiler now knows someNumberOrString is of type `number | string`

////////////////////////////////////////////////////////////////////////////////
// Set your own assertion messages
// - a default assertion message is provided; will most likely be good enough for most cases
////////////////////////////////////////////////////////////////////////////////
const defaultAssertionMessage = getAssertionMessage();
setAssertionMessage(
  (someValue, expectedType) =>
    `Expected a ${expectedType}, got a ${getType(someValue)}`
);
try {
  const aNumber: unknown = 123;
  assertIsString(aNumber);
} catch (err) {
  console.log(err); // An error with message 'Expected a string, got a number' will be logged
}
```

## API

Swing by the [docs](https://evanlouie.github.io/assertate/) to get a full look
at the available functions.
