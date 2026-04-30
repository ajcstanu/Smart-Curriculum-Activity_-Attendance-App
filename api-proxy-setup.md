# API Proxy Setup Guide

## Why a Proxy?

The EduTrack AI app calls the Anthropic Claude API for the AI Academic Advisor feature. Calling the API directly from the browser requires an API key, which **must never be exposed in client-side code** in a production environment.

This guide explains how to set up a simple backend proxy so your API key stays secure on the server.

---

## Option 1: Node.js / Express Proxy (Recommended)

### Install dependencies

```bash
npm init -y
npm install express cors node-fetch dotenv
```

### Create `proxy-server.js`

```js
require('dotenv').config();
const express = require('express');
const cors = require('cors');

const app = express();
app.use(cors({ origin: 'http://localhost:3000' })); // restrict to your frontend origin
app.use(express.json());

app.post('/api/chat', async (req, res) => {
  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': process.env.ANTHROPIC_API_KEY,
        'anthropic-version': '2023-06-01',
      },
      body: JSON.stringify(req.body),
    });
    const data = await response.json();
    res.json(data);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

app.listen(4000, () => console.log('Proxy running on http://localhost:4000'));
```

### Create `.env`

```
ANTHROPIC_API_KEY=sk-ant-your-key-here
```

### Update the fetch call in `src/index.html`

Change:
```js
const res = await fetch('https://api.anthropic.com/v1/messages', { ... });
```

To:
```js
const res = await fetch('http://localhost:4000/api/chat', { ... });
// Remove the 'x-api-key' header — the proxy adds it server-side
```

---

## Option 2: Python / FastAPI Proxy

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
import httpx, os
from dotenv import load_dotenv

load_dotenv()
app = FastAPI()
app.add_middleware(CORSMiddleware, allow_origins=["*"], allow_methods=["*"], allow_headers=["*"])

@app.post("/api/chat")
async def chat(body: dict):
    async with httpx.AsyncClient() as client:
        r = await client.post(
            "https://api.anthropic.com/v1/messages",
            headers={
                "x-api-key": os.getenv("ANTHROPIC_API_KEY"),
                "anthropic-version": "2023-06-01",
                "Content-Type": "application/json",
            },
            json=body,
        )
        return r.json()
```

Run with: `uvicorn proxy:app --reload`

---

## Option 3: Deploy to Vercel (Serverless)

Create `api/chat.js` in your project root:

```js
export default async function handler(req, res) {
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01',
    },
    body: JSON.stringify(req.body),
  });
  const data = await response.json();
  res.status(200).json(data);
}
```

Add `ANTHROPIC_API_KEY` to your Vercel project environment variables in the dashboard.

---

## Security Checklist

- [ ] Never commit `.env` files — add to `.gitignore`
- [ ] Restrict CORS to your specific frontend domain in production
- [ ] Add rate limiting (e.g. `express-rate-limit`) to prevent abuse
- [ ] Consider adding user authentication before proxying requests
