# Type Narrowing in TypeScript

Type narrowing is when you take a general type and narrow it down to a more specific type inside a block of code. TypeScript uses control flow analysis to reason about what a value can be at any given point. Narrowing is safer and easier for unions to use.

Consider a variable typed as `string | number`. You cannot call string methods on it directly because it might be a number. A `typeof` check solves this problem:

```ts
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.trim();
  }
  return value.toFixed(2);
}
```

Inside the first branch, TypeScript knows that `value` is a string. After the branch, it knows that `value` is a number.

The `instanceof` operator narrows class-based types:

```ts
function getMessage(error: Error | string): string {
  if (error instanceof Error) {
    return error.message;
  }
  return error;
}
```

The `in` operator checks whether a property exists on an object. It is useful for unions of object types:

```ts
type Cat = { meow: () => void };
type Dog = { bark: () => void };

function speak(animal: Cat | Dog): void {
  if ("meow" in animal) {
    animal.meow();
  } else {
    animal.bark();
  }
}
```

Narrowing also applies to literal checks, truthiness, and user-defined type guards. These techniques stop you from accessing properties that don't exist and catch errors at compile time. You can prove the type to the compiler, instead of using unsafe casts. This leads to better autocomplete, refactoring safety and reliability at runtime. Clear checks also make code easier to read through. Good narrowing lets unions stay expressive without sacrificing type safety.

Type narrowing turns uncertain unions into precise types. By using `typeof`, `instanceof`, and `in`, you can write flexible code that remains safe and readable.
