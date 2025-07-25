# 🔑 Gemini API Key (Accessing Gemini Models)
If your agent wants to use Gemini (Google's powerful LLM family), it needs a Gemini API key — simple, but important. Without it, your agent can’t generate content, extract info, summarize, or chat using Gemini.

---

### 🎯 When Do You Need Gemini API?
You need the Gemini API key if:

- You’re calling Gemini Pro / Gemini 1.5 via REST or client libraries (Python, Node, etc.)

- You’re not using Vertex AI’s built-in Gemini integration (which uses IAM)

---

### 🛠️ How to Get the Gemini API Key
- Go to Google AI Studio

- Sign in with your Google account

- Click on "Get API Key"

- Copy the key — treat it like a password

---

### 📦 Add API Key to Your Agent Securely
Never hardcode the key. Instead:

✅ Option 1: Use GCP Secret Manager
1. Go to Secret Manager
2. Click Create Secret
3. Name it: GEMINI_API_KEY
4. Paste your key and save

In your code:
```python
from google.cloud import secretmanager

def get_gemini_key():
    client = secretmanager.SecretManagerServiceClient()
    name = "projects/PROJECT_ID/secrets/GEMINI_API_KEY/versions/latest"
    response = client.access_secret_version(request={"name": name})
    return response.payload.data.decode("UTF-8")
```
> You must give your service account roles/secretmanager.secretAccessor

#### ✅ Option 2: Use Environment Variables (for quick testing)
```bash
export GEMINI_API_KEY="your-api-key"
```
In Python:

```python
import os
api_key = os.getenv("GEMINI_API_KEY")
```
----


### 🧪 Test Your Key
Use this curl command to verify:
```bash
curl -H "Authorization: Bearer $GEMINI_API_KEY" \
  -H "Content-Type: application/json" \
  -X POST https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent \
  -d '{"contents":[{"parts":[{"text":"Hello, Gemini!"}]}]}'
```

----

###  Warning
- The free tier has rate limits (check pricing page)

- Abuse may revoke your key

- Do not commit your key to GitHub or share it in screenshots

----

### 🧠 When to Use IAM Instead
If you're using Vertex AI with Gemini, you don’t need an API key. You’ll access Gemini via IAM-authenticated SDKs or pipelines.

Use API Key only if:
- You’re building quick demos
- You’re outside GCP but want Gemini capabilities
- You’re using LangChain, CrewAI, or Flowise with Gemini tools

---
### ✅ Summary
| What You Did                         | Why It Matters                             |
| ------------------------------------ | ------------------------------------------ |
| Got Gemini API Key from AI Studio    | Allows your agent to use Gemini LLMs       |
| Secured it via Secret Manager or ENV | Prevents leaks, secures production agents  |
| Integrated it with agent code        | Enables generation, chat, extraction, etc. |
