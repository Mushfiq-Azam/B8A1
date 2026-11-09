# Type Aliases vs Interfaces in TypeScript

TypeScript provides developers with two common ways to describe the shape of data: type aliases and interfaces. Both are common in real projects, so the knowledge of their differences will help you to choose the right tool. In this post we will compare them with small examples.

A type alias creates a new name for any type. It can name objects, unions, tuples, and primitives:

```ts
type User = { name: string; age: number };
type Status = "active" | "inactive";
```

An interface describes the shape of an object. It commonly models classes, API data, and public contracts:

```ts
interface Product {
  title: string;
  price: number;
}
```

TypeScript is structurally typed . Compatibility is based on the members of a value , not on the name of the type . If two types have the same required properties you can assign values between them.

Interfaces support declaration merging. If you declare the same interface twice, TypeScript combines the declarations:

```ts
interface Settings {
  theme: string;
}

interface Settings {
  language: string;
}
```

Type aliases do not merge, and duplicate declarations cause an error. Interfaces can also extend other interfaces, including several at once:

```ts
interface Admin extends User {
  permissions: string[];
}
```

Type aliases use intersections to combine object types and unions to express alternatives:

```ts
type AdminRole = User & { permissions: string[] };
type Result = string | number;
```

Interface for public APIs and extensible object shapes. Choose a type alias for unions, tuples, primitives, and advanced type transformations.  Choose the easier option and change it only if your design needs more flexibility. Both tools are useful and experienced developers often mix them.

In short, interfaces are good for reusable object contracts, while type aliases are for flexible combinations. Pick depending on the problem. Knowing both makes your Typescript code more clear and safer.
