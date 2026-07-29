# 🧪 API Playground

### Quickly test API requests and inspect responses

Use this note to try endpoints, tweak parameters, and **keep requests + responses documented** in one place.

---

## 1️⃣ API Setup (shared)

```js global;
const baseURL = "https://jsonplaceholder.typicode.com";
const token = null; //"YOUR_API_TOKEN"; // optional

const headers = {
  "Content-Type": "application/json",
  ...(token ? { Authorization: `Bearer ${token}` } : {})
};
```

---

## 2️⃣ Requests Collection

### 📥 GET — List Users

```js 
const res = await fetch(`${baseURL}/users`, { headers });
const users = await res.json();

showDatagrid({
  data: users,
  pagination: true
});
```

---

### 🔍 GET — User by ID

```js 
const userId = 1;
const res = await fetch(`${baseURL}/users/${userId}`, { headers });
printJSON(await res.json());
```

---

### 📤 POST — Create User

```js 
const res = await fetch(`${baseURL}/users`, {
  method: "POST",
  headers,
  body: JSON.stringify({
    name: "John Doe",
    email: "john@example.com"
  })
});

printJSON(await res.json());
```

---

### ✏️ PUT — Update User

```js 
const userId = 1;
const res = await fetch(`${baseURL}/users/${userId}`, {
  method: "PUT",
  headers,
  body: JSON.stringify({
    name: "Jane Doe"
  })
});

printJSON(await res.json());
```

---

### 🗑️ DELETE — Remove User

```js 
const userId = 1;
const res = await fetch(`${baseURL}/users/${userId}`, {
  method: "DELETE",
  headers
});

print(`Status: ${res.status}`);
```

---

## 🔐 (Optional) OAuth Token Helper

Use only if needed.

```js 
const authRes = await fetch("https://auth.example.com/token", {
  method: "POST",
  headers: { "Content-Type": "application/x-www-form-urlencoded" },
  body: new URLSearchParams({
    grant_type: "client_credentials",
    client_id: "CLIENT_ID",
    client_secret: "CLIENT_SECRET"
  })
});

const { access_token } = await authRes.json();
print(access_token);
```
