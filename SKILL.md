# Security 10: 10 Rules for Writing Secure Code

---
name: security-rules
description: "Security 10: 10 rules for writing secure TypeScript/JavaScript code. Use this skill when reviewing or writing code that handles sensitive data, authentication, or authorization."
user-invocable: true
---

# Rule 1: Validate All Input, Sanitize All Output

Never trust external data. Validate on entry, sanitize on exit.

## BAD:
```typescript
function search(query: string) {
  return db.query(`SELECT * FROM users WHERE name = '${query}'`);
}
```

## GOOD:
```typescript
import { z } from 'zod';
const SearchSchema = z.object({
  query: z.string().min(1).max(100).regex(/^[a-zA-Z0-9]+$/),
});
function search(raw: unknown) {
  const { query } = SearchSchema.parse(raw);
  return db.query('SELECT * FROM users WHERE name = $1', [query]);
}
```

# Rule 2: Principle of Least Privilege

Every component runs with minimum permissions needed.

# Rule 3: Never Expose Secrets in Code

No API keys, passwords in source code. Use env vars/vault.

# Rule 4: Proper Authentication & Session Management

Use established libraries. Never roll your own auth.

# Rule 5: Encrypt Data at Rest and in Transit

TLS for transit, strong encryption for storage.

# Rule 6: Implement Access Control

Check permissions on every request. Deny by default.

# Rule 7: Protect Against Injection

No concatenation of untrusted data into commands.

# Rule 8: Secure Dependencies

Audit and update dependencies regularly.

# Rule 9: Secure File Handling

Validate file type, size, random filenames, store outside webroot.

# Rule 10: Log Security Events

Log auth failures, access denied. Never log secrets.
