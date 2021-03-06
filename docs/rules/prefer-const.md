---
title: Rule prefer-const
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Suggest using `const` (prefer-const)

If a variable is never reassigned, using the `const` declaration is better.

`const` declaration tells readers, "this variable is never reassigned," reducing cognitive load and improving maintainability.

## Rule Details

This rule is aimed at flagging variables that are declared using `let` keyword, but never reassigned after the initial assignment.

The following patterns are considered problems:

```js
/*eslint prefer-const: 2*/
/*eslint-env es6*/

let a = 3;
console.log(a);

// `i` is redefined (not reassigned) on each loop step.
for (let i in [1,2,3]) {
    console.log(i);
}

// `a` is redefined (not reassigned) on each loop step.
for (let a of [1,2,3]) {
    console.log(a);
}
```

The following patterns are not considered problems:

```js
/*eslint prefer-const: 2*/
/*eslint-env es6*/

let a; // there is no initialization.
console.log(a);

// `i` gets a new binding each iteration
for (const i in [1,2,3]) {
  console.log(i);
}

// `a` gets a new binding each iteration
for (const a of [1,2,3]) {
  console.log(a);
}

// `end` is never reassigned, but we cannot separate the declarations without modifying the scope.
for (let i = 0, end = 10; i < end; ++i) {
    console.log(a);
}

// suggest to use `no-var` rule.
var b = 3;
console.log(b);
```

## When Not To Use It

If you don't want to be notified about variables that are never reassigned after initial assignment, you can safely disable this rule.

## Related Rules

* [no-var](no-var)

## Version

This rule was introduced in ESLint 0.23.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/prefer-const.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/prefer-const.md)
