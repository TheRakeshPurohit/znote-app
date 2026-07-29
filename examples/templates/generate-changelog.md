# 🧾 Commits to Changelog

### Turn raw git log output into a clean, ready-to-publish changelog.

---

## 📥 Step 1 — Collect commits from CLI

Run one of these commands in your terminal, then **paste the output below**.

### Last commits

```bash 
cd ~/YOUR_PROJECT && git log --oneline -20
```

### Since last tag

```bash 
cd ~/YOUR_PROJECT && git log --oneline $(git describe --tags --abbrev=0)..HEAD
```

### Between two tags

```bash 
cd ~/YOUR_PROJECT && git log --oneline v3.2.0..v3.3.0
```

---

## 📋 Step 2 — Paste commits here

```text blockName=commits;
feat: add pwsh support on Windows
fix: prevent tab content flicker on close
fix: handle image paths with spaces
refactor: stabilize treeview state
chore: minor UI polish
```

---

## 🧠 Step 3 — Generate Changelog (AI)

👉 Ask the AI:

> Generate a md code block to generate the output.
> **Keep a Changelog** compliant in Markdown.
> Group entries into **Added / Changed / Fixed**.
> Remove noise (chores), keep it concise and user-facing.
> @commits


---

## 🧾 Output
