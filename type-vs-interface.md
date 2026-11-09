# Type Aliases vs Interfaces in TypeScript

TypeScript gives developers two common ways to describe the shape of data: type aliases and interfaces. Both appear often in real projects, so knowing their differences helps you choose the right tool. This post compares them with small examples.

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

TypeScript uses structural typing, so compatibility depends on a value's members, not its type name. If two types share the same required properties, values can be assigned between them.

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

Choose an interface for extendable object shapes and public APIs. Choose a type alias for unions, tuples, primitives, and advanced type transformations. Start with the simpler option and change it only when your design needs more flexibility. Both tools are useful, and experienced developers often mix them.

In short, interfaces are great for reusable object contracts, while type aliases handle flexible combinations. Choose based on the problem. Understanding both makes your TypeScript code clearer and safer.
