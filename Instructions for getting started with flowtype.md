Instructions for getting started with flow:

1. Install the `flow-bin` package and the `babel-plugin-transform-flow-strip-types`

2. Add a file called .flowconfig and add an entry to `scripts` in `package.json`

3. Add `@flow` at the top of your file when it is ready for type-checking.

4. run code with babel-node even if there are type errors

5. add type annotations to your code:

```
function foo(x: string, y: number): number {
  return x.length * y
}
```

6. Flow tracks `null` seperately and warns you when you try and use null where it is not allowed

7. For Arrays, there is a generic syntax that looks like Array<Number>

8. Flow supports interface files for libraries(such as React).

9. Once the `flow` command is run, it starts a server and keeps it alive. It will connect to the server whenever we run `flow`.

10. Flow must be used if you plan on importing a function from one function to another, if not it cannot annotate the function that has been imported

11. Do not use `any` type with flow. Using it means that you are an expert.

12. Define interfaces under the `libs` part of `.flowconfig`. An interface represents a function definition:

13. Flow comes with out of the box support for Node.js API and standard JS API.

```
declare class Underscore {
  findWhere<T>(list: Array<T>, properties: {}): T;
}

declare var _: Underscore;
```

+ An argument to a function can be declared as `nullable` if it is added a `?` parameter.

---

Basic Types:

+ any

> do not use unless bypassing type checker

+ mixed

> use for dynamic type tests

+ number

+ string

+ void

+ null

+ boolean

+ arrays

> must be homogenous arrays, can also be used with number[] syntax which I would prefer.

+ tuples

> a hetrogenous array, must be of a fixed length can be specified as [number,string,boolean]

+ objects

```
{
foo:string,
bool:number
}
```

> can be used as a map type:

```
{
  [id:string]:number
}
```

if a function is treated as an object, it becomes something wierd known as a `callable type`:

```
function makeCallable(): { (x: number): string; foo: number } {
  function callable(number) {
    return number.toFixed(2);
  }
  callable.foo = 123;
  return callable;
}

```

string concatenation is accepted by `flow` as a valid typecast.

flow treats `null` and `undefined` as seperate types, `void` is the type for `undefined`. if a function param is optional, it uses `T|void` as its type.

type aliases can be used to explain the types of your objects,function in isolation.

create type aliases in one file and export them into another

```
export type Foo = string
import type Foo from './foo'
```

when working with destructuring patterns, you either need to do the entire pattern or not do it at all.

tuples only guarantee that elements upto the specified length are type checked, if the array is larger than expected, flow can only check the elements upto a specified length
after that, anything could happen.

for a local class, type inference can occur on the methods if enough information is provided on the properties. however, type annotations are a must for exported classes.

also, for reasons beyond my understanding, there is polymorphism, bounded polymorphism and a `this` type.

objects can have optional properties, they are defined using a `?` on the syntax, if a property is optional, flow will make you check that it is not undefined before using it.

flow supports the adding of properties to a Javascript object after it has been created, it cannot guarantee its existence but can check read and write operations on it.

flow does not primitives and arrays as objects.

---

flow types pass through `this` as well.

variadics are considered optional parameters

if a function is called with too few arguments, flow uses `void` as the type for the rest of the arguments.

to prevent a function from taking too many arguments:

```
function takesOnlyOneNumber(x:number,...rest:Array<void>) {
  return x;
}
```

it is possible to use `union` and `disjoint` types in Javascript

flow does not detect `void` types in `array accesses` and `object properties`.

flow has union and intersection types, the former requires that the value assigned be atleast one of the types
the latter expects that all the types in the annotation are satisfied.

```
var x :string|number = 22
x = 'twenty two'
x = false
```

in flow, the typeof operator can be used to capture information about existing type annotations within other type annotations.

In flow, disjoint union types are just regular union types that rely on type literals with literal types.

flow throws errors when you do not annotate your exports with type definitions.

flow understands `propTypes`,`defaultProps`,`state` and works amazingly well with `react`.
```


Flow also supports static typing for arrow functions, generators and Promises. We will find out each of these as we go along.
You can create `interfaces` that span across multiple classes. Flow also supports `generic` types.

Type aliases in flow seem to be the most interesting part of the advanced types:

```
type ObjectWithManyProperties = {
  foo: string,
  bar: number,
  baz: boolean,
  qux: (foo: string, bar: number) => boolean;
}
```

---
