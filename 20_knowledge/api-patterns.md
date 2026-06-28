# API Patterns

> Summary: REST API conventions and response structures I use across projects.

---

## Standard response envelope

Every API I build returns this shape:

```typescript
{
  data: T | null,       // the actual result
  error: string | null, // error message if something went wrong
  meta: {               // optional extra info (pagination, etc.)
    page?: number,
    total?: number,
  }
}
```

Why: consistent shape means the frontend always knows where to look.
It never has to guess if the result is in `result`, `response`, `payload`, etc.

---

## Error handling convention

- 4xx errors = the client did something wrong (bad input, not authenticated, not found).
- 5xx errors = the server failed — do not expose internal details in the message.
- Always return a human-readable `error` string, not just a status code.

```typescript
// Good
res.status(404).json({ data: null, error: "User not found", meta: {} })

// Bad
res.status(404).json({ message: "Not found" }) // inconsistent shape
```

---

## Authentication

- Use JWT for stateless auth.
- Access tokens expire in 15 minutes.
- Refresh tokens expire in 7 days, stored in HttpOnly cookies.
- Always validate the token in middleware, never in the route handler itself.

---

## Notes / open questions

- Still deciding: should `meta` always be present even when empty, or omit it?
- Need to document the pagination pattern once I standardise it.