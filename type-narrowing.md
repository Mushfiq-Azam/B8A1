# Type Narrowing in TypeScript

Type narrowing is the process of reducing a broad type to a more specific type inside a block of code. TypeScript uses control flow checks to understand what a value can be at each point. Narrowing makes unions safer and easier to use.

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

Narrowing also works with literal checks, truthiness, and user-defined type guards. These techniques prevent invalid property access and catch mistakes at compile time. Instead of using unsafe casts, you can prove the type to the compiler. This improves autocomplete, refactoring safety, and runtime reliability. Clear checks also make code easier to review. Good narrowing keeps unions expressive without giving up type safety.

Type narrowing turns uncertain unions into precise types. By using `typeof`, `instanceof`, and `in`, you can write flexible code that remains safe and readable.
