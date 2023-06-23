## Organization

## Conventions

- [1.1](#convensions-d-ts-extension) **`d.ts` Extension**: Do not use `d.ts` file extension even when a file contains only type declarations.

  > Why? Type errors in `d.ts` files are not checked by TypeScript [^1].

[^1]: This is because `skipLibCheck` TypeScript configuration is set to `true` in this project.

- [1.2](#convensions-type-alias-vs-interface) **Type Alias vs. Interface**: Do not use `interface`. Use `type`.

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

- [1.3](#convensions-enum-vs-union-type) **Enum vs. Union Type**: Do not use `enum`. Use union types.

  > Why? Enums come with several [pitfalls](https://blog.logrocket.com/why-typescript-enums-suck/). Most enum use cases can be replaced with union types.

  ```ts
  // Most simple form of union type.
  type Color = "red" | "green" | "blue";
  function printColors(color: Color) {
    console.log(color);
  }

  // When the values need to be iterated upon.
  import { TupleToUnion } from "type-fest";
  const COLORS = ["red", "green", "blue"] as const;
  type Color = TupleToUnion<typeof COLORS>; // type: 'red' | 'green' | 'blue'

  for (const colors of color) {
    printColor(color);
  }

  // When you prefer to use object keys to access values over directly using literal values.
  // i.e. `COLORS.Red` vs. `"red"`
  import { ValueOf } from "type-fest";
  const COLORS = {
    Red: "red",
    Green: "green",
    Blue: "blue",
  } as const;
  type Color = ValueOf<typeof COLORS>; // type: 'red' | 'green' | 'blue'

  printColor(COLORS.Red);
  ```

- [1.4](#convensions-unknown-vs-any) **`unknown` vs. `any`**: Don't use `any`. Use `unknown` if type is not known beforehand

  > Why? `any` type bypasses type checking.

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
