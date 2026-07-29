# 🤖 Call an LLM

👉 **Ensure you have installed the** 🧩 **Ollama plugin**

## 🔹 Install Ollama
📥 **Download Ollama:** [Ollama Download](https://ollama.com/download)

Before using, pull an LLM model to run locally:
```bash 
ollama pull llama3.2
```


## 🔄 Streaming AI Responses
💡 **Important:** The comment `//exec: node` is required for proper streaming.

### 🌊 Stream Response in Console
```js 
//exec: node
const streamResponse = true;
await useLocalAI("llama3.2", streamResponse, "Create a short story");
```

## ⏳ Wait for Result and Chain Tasks
Use `streamResponse = false` to wait for a full response before proceeding.
```js 
//exec: node
const streamResponse = false;
const result = await useLocalAI("llama3.2", streamResponse, "Translate this sentence into French: Hello everyone.");
print(result);
```

## 🌍 Use Remote LLM with OpenRouter
🔑 **Get your API key here:** [OpenRouter API Keys](https://openrouter.ai/settings/keys)

```js 
//exec: node
const streamResponse = true;
const baseURL = "https://openrouter.ai/api/v1";
const apiKey = "API_KEY";

await useOpenAIApi(baseURL, apiKey, "sao10k/l3.3-euryale-70b", streamResponse, "Create a short story");
```

✅ **You're now set up to use local and remote AI models!** 🚀
