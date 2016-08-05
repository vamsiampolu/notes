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

```
declare class Underscore {
  findWhere<T>(list: Array<T>, properties: {}): T;
}

declare var _: Underscore;
```

+ An argument to a function can be declared as `nullable` if it is added a `?` parameter.

---
