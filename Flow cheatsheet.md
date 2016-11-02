Flow cheatsheet

Primitive types

+ number

+ string

+ boolean

+ null

+ void

`null` and `undefined` are tracked by flow, the latter is not tracked during array accesses and `object` accesses.

Reference types

+ Array

+ Tuple

+ Object

+ Map

Arrays are like Lists in other languages, they are homogeneous, the syntax for arrays looks like:

```
number[]
Array<Number>
```

Tuples are lists of fixed length with variable types:

```
[string,number,boolean]
```

Tuples can only be checked for the properties provided, if there are additional properties
within the array they cannot be type checked.

The syntax for objects is pretty obvious:

```
{
  x:string,
  y:number
}
```

If you want to use a fixed type for the key and value:

```
{
  [key:number]:string
}
```

Function types are specified like this:

```
function(x:?number,y:string = 'world'): string {
  return y
}
```

When destructuring, type annotations need to be supplied for the entire destructuring pattern:

```
//{x:string, y: { z:number|string }}
```

rest parameters are optional.

if a function is called with too few arguments, the other parameters have the type `void`.

---

Flow has type aliases which can be exported and imported:

```
type X = number
export type X
import type Y from '../y'
```

Flow makes it mandatory to specify type annotations for module exports.

---

flow has union and intersection types:

union types:

```
var x: string|number
var obj = {y:number & x}
```

flow has literal types:

```
type y = {
  x:'One'
}
```

these literal types can be used with union types to create what are known as disjoint union types.
---
