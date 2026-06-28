# TypeScript Patterns

> Summary: TypeScript patterns and conventions I use regularly across projects.

---

## General rules

- Always use TypeScript over plain JavaScript for new code.
- Never use `any` — if you do not know the type yet, use `unknown` and narrow it.
- Prefer explicit return types on functions, especially public ones.
- Use `interface` for objects that describe shapes. Use `type` for unions, intersections, and aliases.

---

## Typing objects and models

```typescript
// Use interface for object shapes
interface User {
  id: number
  name: string
  email: string
  createdAt: Date
}

// Use type for unions
type Status = "active" | "inactive" | "pending"

// Optional fields with ?
interface CreateUserRequest {
  name: string
  email: string
  role?: string  // optional
}
```

---

## Null and undefined handling

```typescript
// Never assume something exists — check first
const user = users.find(u => u.id === id)
if (!user) throw new Error(`User ${id} not found`)

// Optional chaining (like Java's Optional in a way)
const city = user?.address?.city  // undefined if any part is missing

// Nullish coalescing — use default if null or undefined
const name = user?.name ?? "Anonymous"

// Do NOT use || for defaults — it catches empty string and 0 too
const name = user?.name || "Anonymous"  // wrong if name can be ""
```

---

## Async / await

```typescript
// Always async/await over .then() chains
// Good
async function getUser(id: number): Promise<User> {
  const user = await db.findById(id)
  if (!user) throw new Error("Not found")
  return user
}

// Bad
function getUser(id: number): Promise<User> {
  return db.findById(id).then(user => {
    if (!user) throw new Error("Not found")
    return user
  })
}
```

---

## Error handling

```typescript
// Never silent catches
// Bad
try {
  await doSomething()
} catch (e) {
  // nothing here — dangerous
}

// Good — always log or rethrow
try {
  await doSomething()
} catch (error) {
  console.error("doSomething failed:", error)
  throw error  // or handle it explicitly
}

// Type the error properly
} catch (error) {
  if (error instanceof Error) {
    console.error(error.message)
  }
}
```

---

## Array operations — prefer functional

```typescript
const users: User[] = [...]

// Filter
const activeUsers = users.filter(u => u.status === "active")

// Transform
const names = users.map(u => u.name)

// Find one
const admin = users.find(u => u.role === "admin")

// Check existence
const hasAdmin = users.some(u => u.role === "admin")

// Avoid for loops for these — use map/filter/find/some/every/reduce
```

---

## API response envelope

Every API response follows this shape (see also api-patterns.md):

```typescript
interface ApiResponse<T> {
  data: T | null
  error: string | null
  meta: {
    page?: number
    total?: number
  }
}

// Usage
function ok<T>(data: T): ApiResponse<T> {
  return { data, error: null, meta: {} }
}

function fail(message: string): ApiResponse<null> {
  return { data: null, error: message, meta: {} }
}
```

---

## Utility types I use often

```typescript
// Partial — all fields become optional (useful for update payloads)
type UpdateUserRequest = Partial<User>

// Pick — take only specific fields
type UserSummary = Pick<User, "id" | "name">

// Omit — remove specific fields
type UserWithoutPassword = Omit<User, "password">

// Record — typed key-value map
const usersByid: Record<number, User> = {}
```

---

## Things I always forget

- `unknown` is safer than `any` — forces you to check the type before using it.
- `interface` can be extended, `type` cannot be re-opened — use interface for things that might grow.
- TypeScript types disappear at runtime — they are only for the compiler and your editor.
- `as` casting does not convert anything, it just silences TypeScript — use it carefully.

---

## Still learning / open questions

- Generics beyond basic usage — when to use constraints like `<T extends object>`.
- Decorators — used in NestJS but not fully comfortable with them yet.
- Type guards — custom `is` functions for narrowing complex types.