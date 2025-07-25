# 🚀 Cloud Run

Cloud Run is a fully managed compute platform that lets you deploy and run containerized applications on Google Cloud. For AI agent developers, Cloud Run is one of the easiest ways to deploy LLM agents or backend services as serverless containers — without managing infrastructure.

---
## ✅ Why Use Cloud Run for Agent Development?

| Feature               | Benefit                                                                          |
| --------------------- | -------------------------------------------------------------------------------- |
| Serverless & Scalable | Auto-scales from 0 to thousands of requests per second                           |
| Container-native      | Deploy any app (e.g., FastAPI, Flask, Node.js) as long as it’s in a Docker image |
| Pay-per-use Pricing   | You only pay when the agent is running                                           |
| Secure & Integrated   | Built-in IAM, traffic splitting, HTTPS, and VPC support                          |
| Fast CI/CD Friendly   | Easy to integrate with GitHub or Cloud Build pipelines                           |

----

### 🔧 When Should Agent Developers Use Cloud Run?
- Deploying your AI agent API built with FastAPI/Flask
- Hosting tool services (e.g., file parsers, summarizers)
- Running agent backends that integrate with LangChain, CrewAI, or Flowise
- Building webhook receivers for Slack, Twilio, Discord, etc.
- Creating task processors triggered via Pub/Sub or API

---

### 🚀 How to Deploy an Agent to Cloud Run
**1. Write your agent app (e.g., FastAPI) and a Dockerfile.**
```python
# app.py
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
def root():
    return {"message": "Hello from my agent!"}
```
**2. Create a Dockerfile:**
```docker
FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install fastapi uvicorn
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
```
**3. Build the image and push it to Artifact Registry (or use gcloud builds):**

```bash
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/agent-api
```

**4. Deploy to Cloud Run:**
```bash
gcloud run deploy agent-api \
    --image gcr.io/YOUR_PROJECT_ID/agent-api \
    --platform managed \
    --allow-unauthenticated \
    --region us-central1
```
---

### 🛡️ Security & IAM Tips
- By default, Cloud Run apps are publicly accessible. Use --no-allow-unauthenticated to lock it down.
- Add IAM roles like Cloud Run Invoker to control access.
- Use Secret Manager to securely pass LLM API keys or credentials to your container.

---

### 🧩 Connecting with Other GCP Services
| Use Case                      | Integration Needed              |
| ----------------------------- | ------------------------------- |
| Store agent logs              | Connect with Cloud Logging      |
| Use Vertex AI model endpoints | Authenticate with Vertex AI SDK |
| Receive real-time events      | Connect with Pub/Sub            |
| Monitor app usage             | Enable Cloud Monitoring         |

----
#### ⚙️ Agent Deployment Example
**Let’s say you have an LLM agent exposed via /generate-summary. You can:**

- Host the agent backend using Cloud Run
- Add request logic from a frontend or another agent
- Use tools like Composio, LangChain, or CrewAI to trigger that Cloud Run endpoint

---

#### 📌 Best Practices
- Use health checks to monitor uptime.
- Set a concurrency limit to control how many requests a container can handle.
- Enable cloud logging and error reporting.
- Prefer small, efficient containers for faster cold start.

---

#### 🔄 Versioning & Updates
**To update your agent, just re-run:**
```bash
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/agent-api
gcloud run deploy agent-api --image gcr.io/YOUR_PROJECT_ID/agent-api
```
Cloud Run will automatically replace the old container with the new one, with zero downtime.