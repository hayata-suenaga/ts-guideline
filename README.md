## Organization

## Conventions

- [1.1] **Extensions**: Do not use d.ts file extension even when a file contains only type declarations.

  > Why? Type errors in `d.ts` files are not checked by TypeScript [^1].

[^1]: This is because `skipLibCheck` TypeScript configuration is set to `true` in this project.

- [1.2] **Type Aliases vs. Interfaces**: Do not use `interface`. Use `type`.

  > Why? In TypeScript, `type` and `interface` can be used interchangeably to declare types. Use `type` for consistency.

```ts
// bad
interface Person {
  name: string;
}

// good
type Person = {
  name: string;
};
```

- [1.3] Do not use `enum`. Use union types.

  > Why? Enums come with several [pitfalls](https://blog.logrocket.com/why-typescript-enums-suck/). Most enum use cases can be replaced with union types.

## `unknown` vs. `any`

## `T[]` vs. `Array<T>`

## `@ts-expect-error`

## Optional chaining and nullish coalescing

## Type Inference

### Return types

## JSDoc

Omit comments that are redundant with TypeScript. Do not declare types in `@param` or `@return` blocks. Do not write `@implements`, `@enum`, `@private`, `@override`

## Default Props

## Naming Conventions

- Use PascalCase for type names

  ```ts
  // bad
  type foo = ...;
  type BAR = ...;

  // good
  type Foo = ...;
  type Bar = ...;
  ```

- Do not postfix type aliases with Type

  ```ts
  // bad
  type PersonType = { name: string };

  // good
  type Person = { name: string };
  ```
