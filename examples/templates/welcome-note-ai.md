# ⚡ Run code and AI

Your notes run. Hit **Run** on a block — no setup, no account.

## 1. Run code

```js 
const r = await fetch("https://api.github.com/users/torvalds");
const u = await r.json();
console.log(`${u.name} · ${u.public_repos} repos · ${u.followers} followers`);
```

> ▶️ That ran on your machine. API calls, SQL, scripts

## 2. Let the AI judge the result

Code fetches the data; the AI reasons over it and gives you a call — on *live* data, in place.

```js global
async function getReleases(repo) {
  const r = await fetch(`https://api.github.com/repos/${repo}/releases?per_page=5`);
  return (await r.json()).map(x => ({ tag: x.tag_name, notes: x.body?.slice(0, 800) }));
}
```

```ai tools=getReleases
Look at the last 5 releases of "vercel/next.js". If I upgrade, what's the single most likely thing to break — and should I do it now? One reason.
```

> 💡 The move: **your code fetches, the AI judges.** Point it at *your* repo, DB or API.


## 3. Analyze any file

Copy a file from your explorer — PDF, screenshot, meeting transcript, spec — and paste it into the block below. Znote drops in the path and reads it as context:

```ai 
Summarize this file in 3 bullets, then flag the one thing most likely to bite me.
@file:///👉-paste-your-file-here.txt
```


## 4. Let the AI browse the web

```ai websearch
Search for the latest LTS version of Node.js, and the single biggest change it introduced?
```



## Make it yours

Browse the gallery for ready-to-run templates — **API tester**, **SQL explorer**, **file analysis**.

> Code runs free. The AI is free to try, then runs on your own key (OpenAI · Ollama · OpenRouter).
