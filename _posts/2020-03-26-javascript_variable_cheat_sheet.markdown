---
layout: post
title:      "JavaScript Variable Cheat Sheet"
date:       2020-03-26 17:55:44 +0000
permalink:  javascript_variable_cheat_sheet
---

 
## VAR
Scope of `var` is global and functional. Any `var` variable declared outside a function is scoped globally. `Var` is function scoped when declared inside of a function. Meaning that the variable is only accessible inside the function in which it is declared. 

#### Global Scope

`
var foo = “foo”

function sayWord() {
console.log(foo)
}

sayWord(); // ”foo”
`

**Local/Function Scope**

`
var foo = “foo”

function sayWord() {
   var bar = “bar”
}
console.log(bar); // error: bar not defined
`

**Var can be re-declared and updated**

`
var foo = “foo”
var foo = “bar”
`

****Also works****

`
var foo = “foo”
foo = ”bar”
`
### Var is Hoisted and Initialized
Meaning that the variable is initialized first without declaring the value.

`
console.log(foo)
var foo = “foo”
`

### Interpreted as

`
var foo
console.log(foo) // foo undefined
var foo = “foo”
`

The problem with `var` is that it tries its hardest to not error and you can run into 
problems if you have to use the same variable for whatever reason

`
var foo = “foo”

If (true) {
   var foo = “bar”
}

console.log(foo) // “bar”
`

## LET

Scope is block scoped. This means that a `let` variable is only available within the block it’s declared.

`
let foo = “foo”

if (true) {
   Let bar = “bar”
   console.log(bar) // “bar”
}
console.log(bar) // error: bar is undefined
`

**`let` can be updated but not re-declared**

`
let foo = “foo”
foo = “bar”
console.log(foo) // “bar”

let foo = “foo”
let foo = “bar”
console.log(foo) // error: foo already declared
`

The same `let` variable defined in different scopes will not return an error. Because they are treated as different variables

`
let foo = “foo”

if(true) {
   let foo = “bar”
   console.log(foo) // “bar”
}
console.log(foo) // “foo”
`

Let is Hoisted but not initialized meaning you get a `reference error` if you try to use a let before declaration.

## Const

Similar to `let` but it cannot be updated 

`
const foo = “foo”
foo = “bar”
console.log(foo) // error: assignment to constant variable 
`

Const objects
While an object declared with `const` can’t be re-declared its property values can be updated.

`
const newObj = {
   prop1: “foo”
   prop2: 4
}
 newObj.prop1 = “bar”
newObj // {prop1: “bar”, prop2: 4}
`

**But if you try to re-declare**

`
const newObj = {
   newProp: “Nice!”
   otherProp: 42
} // error: ‘newObj’ has already been declared
`

