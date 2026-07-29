# 🎯 Regex Playground

**Test, debug, and understand regular expressions — directly in your note.**
No external website. No copy-paste. Just text → result.

---

## ✍️ Input

```text blockName=data;
john.doe@email.com
support@company.io
invalid-email@
admin@test.co.uk
https://example.com/page?id=42
```

---

## ⚡ Regex Playground (Ctrl+Enter)

👉 **Edit the regex below, then press `Ctrl+Enter`:**

```js 
// 1️⃣ Choose a regex to test

// Email addresses
const regex = /([a-z0-9._%+-]+)@([a-z0-9.-]+\.[a-z]{2,})/gi;

// URL (http / https)
// const regex = /https?:\/\/[^\s/$.?#].[^\s]*/gi;

// Simple ISO date (YYYY-MM-DD)
// const regex = /\b\d{4}-\d{2}-\d{2}\b/g;


// 2️⃣ Load input
const input = loadBlock("data");

// 3️⃣ Run regex
const matches = [...input.matchAll(regex)].map(m => ({
  match: m[0],
  groups: m.slice(1)
}));

printJSON(matches);
print(`✅ ${matches.length} match(es) found`);
```
