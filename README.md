## Extensions

Do not use d.ts file extension even when a file contains only type declarations. Type errors in `d.ts` files are not checked by TypeScript. [^1]

[^1]: This is because `skipLibCheck` TypeScript configuration is set to `true` in this project.

## Type Aliases vs. Interfaces

Do not use `interface`. In TypeScript, `type` and `interface` can be used interchangeably to declare types. Use `type` for consistency.

## Union Types vs. Enums

Do not use `enum`. When definitnin

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
