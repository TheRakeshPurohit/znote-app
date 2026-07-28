<p align="center">
    <a href="https://znote.io">
    <img width="50" alt="znote logo" src="https://github.com/alagrede/znote-app/assets/5312754/ea8fcb93-1dc9-4938-9fba-a8e5ae667873">
    </a>
</p>

<h1 align="center">Znote — Markdown notes that <em>run</em>.</h1>

<p align="center">
  Write a note. Press play. The AI reads your files, runs your code, and writes the result inline.<br>
  Plain <code>.md</code> files on your disk — yours forever.
</p>

<p align="center">
  <a href="https://znote.io"><img src="https://img.shields.io/badge/website-znote.io-blue" alt="Website"></a>
  <a href="https://znote.io/#download"><img src="https://img.shields.io/badge/platforms-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey" alt="Platforms"></a>
  <a href="https://znote.io/#download"><img src="https://img.shields.io/badge/download-free-brightgreen" alt="Free download"></a>
  <img src="https://img.shields.io/badge/Product%20Hunt-%E2%98%85%205.0-orange" alt="Top on Product Hunt">
</p>

<p align="center">
  <a href="https://znote.io/#download">Download</a>
  ·
  <a href="https://doc.znote.io">Docs</a>
  ·
  <a href="https://recipe.znote.io">Recipes</a>
  ·
  <a href="https://znote.io/obsidian">Znote + Obsidian</a>
  ·
  <a href="https://blog.znote.io">Blog</a>
  ·
  <a href="https://znote.io/faq.html">FAQ</a>
</p>

<a href="https://znote.io">
  <img width="1000" alt="Znote editor with a runnable code block" src="https://znote.io/assets/screenshots/znote-screenshot-code-bar.webp">
</a>

## What is Znote?

**Znote** is a clean, **local-first Markdown editor** for your `.md` files — minimalist by default, powerful when you need it. On top of a calm, beautiful editor sit **two superpowers**, and only two:

1. **🧠 AI inside the editor.** Type `@` to bring any note, folder, or code block in as grounded context — the AI reads *your* files and writes the result inline, right where you're writing. No second app, no chat window, no copy-paste.
2. **▶️ Code blocks that run.** JavaScript / Node.js executes locally in the note. Query a database, fetch an API, shape the rows — the chart or table renders inline, right under the code that produced it. Save the note and you've built a tool.

Everything else is a gorgeous Markdown editor: WYSIWYG, built-in themes (Dark, Nord, Orange, Terminal…), focus mode, tabs, tags, full-text search — and a treeview that **composes folders from anywhere on your disk into one workspace**. Your files stay put, nothing to migrate.

<a href="https://znote.io">
  <img width="1000" alt="Compose AI prompts from your notes with @references" src="https://znote.io/assets/screenshots/znote-screenshot-mention.webp">
</a>

## Everything your notes can do

| | Feature | |
|---|---|---|
| 📝 | **WYSIWYG Markdown** | Write clean Markdown, rendered as you type. No mode-switching, no clutter. |
| 🔗 | **AI `@references`** | Point the AI at notes, folders, files, or code blocks. Answers stay grounded in your material — no generic guesses. |
| ⚡ | **Run JS & Node.js inline** | `await fetch(...)`, `db.query(...)`, per-file NPM, charts and tables rendered next to the code. |
| 🎙️ | **Voice recording & transcription** | Hit record, get a clean, structured note back — typed up for you, inline. |
| 🌐 | **Web search from AI blocks** | The AI browses the web and writes current results back as context you can keep. |
| 🧩 | **Tool calls & plugins** | The AI calls your JS functions; Gmail, Jira, Slack and database plugins available when you want them. |
| 🗂️ | **Composable treeview** | Aggregate folders from anywhere on your disk into one unified tree — files stay where they are. |
| 🎨 | **Beautiful themes** | Dark, Nord, Orange, Terminal and more. An editor you'll actually want to open. |
| 📤 | **Exports** | HTML, PDF, or runnable script — from the same `.md` file. |
| 🔒 | **100% local-first** | Plain `.md` files on your disk. Offline, no cloud, no account, no telemetry by default. |

## What lives in a `.md` file?

Your notes, your AI's context, and your code — all in one plain Markdown file:

````markdown
# Weekly report — week 18

Reviewed onboarding metrics with the team.       ← Markdown prose, like always.

@analytics/onboarding-funnel.md                  ← @references — the AI reads files & blocks as context.

```ai
Write a 3-bullet summary of @onboarding-funnel.  ← AI block — calls your model with the @context above.
```

```js
const data = await db.query(...)                 ← JS / Node block — runs locally, output renders inline.
barChart(data)
```
````

Want ready-to-run examples? Check the [`examples/`](examples) folder in this repo, or install working workflows in one click from the [Recipe Library](https://recipe.znote.io) — Gmail auto-reply, Jira from specs, API tester, SQL explorer, standup digest, and more.

## Works with your Obsidian vault

<a href="https://znote.io/obsidian">
  <img width="1000" alt="Znote Obsidian companion plugin" src="https://znote.io/assets/screenshots/obsidian-companion.png">
</a>

Znote is not an Obsidian replacement — it's a **companion**. Since it's all plain `.md`, your vault opens as-is: wikilinks, embeds, attachments, your settings. Znote adds executable code blocks and inline AI, and saves results back as Markdown Obsidian can read. A one-click companion plugin even adds **"▶ Run in Znote"** buttons inside Obsidian.

Stop using Znote tomorrow — your vault won't notice. [Learn more →](https://znote.io/obsidian)

## Bring Your Own AI (BYOK)

Your AI key. Your models. Your rules. No vendor lock-in.

- **OpenAI** — direct API key, the most-used path.
- **Ollama (local)** — run models like LLaMA or Mistral on your own machine, fully offline. Nothing ever leaves your computer.
- **OpenRouter** — one API, hundreds of models from many providers.

New to API keys? Znote walks you through it in 2 minutes on first launch. **~5€ of API credit ≈ months of daily use.**

## Installation

Znote is **free** with every feature included, for **Windows** (x64 & arm64), **macOS** (Intel & Apple Silicon), and **Linux** (x64 & arm64).

1. Download from [znote.io](https://znote.io/#download).
2. **Windows**: run the `.exe` installer · **macOS**: open the `.dmg` and drag Znote to Applications · **Linux**: run the `.AppImage`.
3. That's it — no account, works offline.

The AI comes with free requests to try, and you can bring your own key to keep going on your own terms — see [znote.io](https://znote.io) for details.

## A word from the maker

> I built Znote because I believe your notes shouldn't be a dead archive — they should *work with you*. Being able to **converse with your own notes** changes everything for productivity: the AI answers from what *you* wrote — your specs, your meetings, your research — not generic guesses. And **runnable code blocks** turn a simple note into a little tool: query a database, call an API, render a chart, save the file — next week you just open it and press play. Once your notes can think and run, you stop copy-pasting between five apps and start getting things done in one place.
>
> — **Anthony**, maker of Znote

## Community & support

Znote is built by **one indie dev** who reads every email. 🚀

- 💡 **Ideas & questions** — [GitHub Discussions](https://github.com/alagrede/znote-app/discussions)
- 🐛 **Bug reports** — [GitHub Issues](https://github.com/alagrede/znote-app/issues)
- 📚 **Documentation** — [doc.znote.io](https://doc.znote.io)
- ✉️ **Email** — contact@alc-digital.fr
- 🐦 **Twitter/X** — [@alagrede](https://twitter.com/alagrede)

## Credits

Znote is built with love using [Electron](https://www.electronjs.org/) and [React](https://reactjs.org/).

---

<p align="center">
  <b>Turn your first note into action.</b><br>
  <a href="https://znote.io/#download">Download free →</a>
</p>
