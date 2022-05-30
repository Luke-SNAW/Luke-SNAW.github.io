---
id: 2s24x5q1mo7d1hy2oauofwy
title: 13 Typescript Utility - A Cheat Sheet for Developer
desc: ""
updated: 1652830904122
created: 1652830715805
---

https://devsmitra.medium.com/13-typescript-utility-a-cheat-sheet-for-developer-9dfd23cb1bbc

# Let's take an example, you have 2 response types:

UserProfileResponse

```typescript
interface UserProfileResponse {
  id: number;
  name: string;
  email: string;
  phone: string;
  avatar: string;
}
```

LoginResponse

```typescript
interface LoginResponse {
  id: number;
  name: string;
}
```

Instead of defining types of the same context LoginResponse and UserProfileResponse, we can define the type for UserProfileResponse and pick some properties for LoginResponse.

```typescript
type LoginResponse = Pick<UserProfileResponse, "id" | "name">;
```

Let’s understand some utility functions that can help you to write better code.

# Uppercase

Constructs a type with all properties of Type set to uppercase.

```typescript
type Role = "admin" | "user" | "guest"; // Bad practice 💩
type UppercaseRole = "ADMIN" | "USER" | "GUEST"; // Good practice ✅
type UppercaseRole = Uppercase<Role>; // "ADMIN" | "USER" | "GUEST"
```

# Lowercase

Constructs a type with all properties of Type set to lowercase. Opposite of Uppercase.

```typescript
type Role = "ADMIN" | "USER" | "GUEST"; // Bad practice 💩
type LowercaseRole = "admin" | "user" | "guest"; // Good practice ✅
type LowercaseRole = Lowercase<Role>; // "admin" | "user" | "guest"
```

# Capitalize

Constructs a type with all properties of Type set to capitalize.

```typescript
type Role = "admin" | "user" | "guest"; // Bad practice 💩
type CapitalizeRole = "Admin" | "User" | "Guest"; // Good practice ✅
type CapitalizeRole = Capitalize<Role>; // "Admin" | "User" | "Guest"
```

# Uncapitalize

Constructs a type with all properties of Type set to uncapitalize. Opposite of Capitalize.

```typescript
type Role = "Admin" | "User" | "Guest"; // Bad practice 💩
type UncapitalizeRole = "admin" | "user" | "guest"; // Good practice ✅
type UncapitalizeRole = Uncapitalize<Role>; // "admin" | "user" | "guest"
```

# Partial

Constructs a type with all properties of Type set to optional.

```typescript
interface User {
  name: string;
  age: number;
  password: string;
} // Bad practice 💩
interface PartialUser {
  name?: string;
  age?: number;
  password?: string;
} // Good practice ✅
type PartialUser = Partial<User>;
```

RequiredConstructs a type consisting of all properties of Type set to required. Opposite of Partial.

```typescript
interface User {
  name?: string;
  age?: number;
  password?: string;
} // Bad practice 💩
interface RequiredUser {
  name: string;
  age: number;
  password: string;
} // Good practice ✅
type RequiredUser = Required<User>;
```

# Readonly

Constructs a type consisting of all properties of Type set to readonly.

```typescript
interface User {
  role: string;
} // Bad practice 💩
const user: User = { role: "ADMIN" };
user.role = "USER"; // Good practice ✅
type ReadonlyUser = Readonly<User>;
const user: ReadonlyUser = { role: "ADMIN" };
user.role = "USER"; // Error: Cannot assign to 'role' because it is a read-only property.
```

# Record

Constructs a type with a set of properties K of type T. Each property K is mapped to the type T.

```typescript
interface Address {
  street: string;
  pin: number;
}
interface Addresses {
  home: Address;
  office: Address;
} // Alternative ✅
type AddressesRecord = Record<"home" | "office", Address>;
```

# Pick

Pick only the properties of Type whose keys are in the union type keys.

```typescript
interface User {
  name: string;
  age: number;
  password: string;
} // Bad practice 💩
interface UserPartial {
  name: string;
  age: number;
} // Good practice ✅
type UserPartial = Pick<User, "name" | "age">;
```

# Omit

Omit only the properties of Type whose keys are in the union type keys.

```typescript
interface User {
  name: string;
  age: number;
  password: string;
} // Bad practice 💩
interface UserPartial {
  name: string;
  age: number;
} // Good practice ✅
type UserPartial = Omit<User, "password">;
```

# Exclude

Constructs a type with all properties of Type except for those whose keys are in the union type Excluded.

```typescript
type Role = "ADMIN" | "USER" | "GUEST"; // Bad practice 💩
type NonAdminRole = "USER" | "GUEST"; // Good practice ✅
type NonAdmin = Exclude<Role, "ADMIN">; // "USER" | "GUEST"
```

# Extract

Constructs a type with all properties of Type whose keys are in the union type Extract.

```typescript
type Role = "ADMIN" | "USER" | "GUEST"; // Bad practice 💩
type AdminRole = "ADMIN"; // Good practice ✅
type Admin = Extract<Role, "ADMIN">; // "ADMIN"
```

# NonNullable

Constructs a type with all properties of Type set to non-nullable.

```typescript
type Role = "ADMIN" | "USER" | null; // Bad practice 💩
type NonNullableRole = "ADMIN" | "USER"; // Good practice ✅
type NonNullableRole = NonNullable<Role>; // "ADMIN" | "USER"
```
