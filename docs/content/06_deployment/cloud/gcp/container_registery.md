# 📦 Container Registry (GCP’s Docker Image Hosting)
Agents that use custom logic, tools, or entire apps often run in containers. Google Cloud’s Container Registry (or its newer version: Artifact Registry) is where you store those Docker images before deploying to Cloud Run, GKE, etc.

---

### 🧠 Why Agent Developers Need This

You’ll need a container registry if you’re:

- Packaging your agent logic (Python, Node.js, etc.) into a Docker container
- Deploying agents to Cloud Run
- Using ADK (Agent Development Kit) agents built locally and then pushed to the cloud

---

### ✅ Options: Container Registry vs Artifact Registry
| Feature                 | Container Registry   | Artifact Registry (Recommended) |
| ----------------------- | -------------------- | ------------------------------- |
| Default location        | `gcr.io`             | `LOCATION-docker.pkg.dev`       |
| Scope                   | Global               | Regional                        |
| Security/Access control | Legacy (less secure) | Fine-grained IAM + VPC controls |
| Cost                    | Same                 | Same                            |
>✅ Use Artifact Registry for all new projects — GCP recommends it.

---

#### 🛠️ Enable the API
Before using it:
```bash
gcloud services enable artifactregistry.googleapis.com
```
#### 🏗️ Create a Docker Artifact Repository
```bash
gcloud artifacts repositories create agents-repo \
    --repository-format=docker \
    --location=us-central1 \
    --description="Agent containers"
```
This creates a private Docker repository in Artifact Registry.

---

### 🐳 Push Your Agent Image (Step-by-Step)
**1. Authenticate Docker to GCP:**
```bash
gcloud auth configure-docker us-central1-docker.pkg.dev
```
**2. Build your agent image:**
```bash
docker build -t agent-v1 .
```
**3. Tag the image with registry path:**
```bash
docker tag agent-v1 us-central1-docker.pkg.dev/PROJECT_ID/agents-repo/agent-v1
```
**4. Push the image:**
```bash
docker push us-central1-docker.pkg.dev/PROJECT_ID/agents-repo/agent-v1
```

----

#### 🔐 IAM Permissions
Give push/pull access to service accounts:
```bash
gcloud projects add-iam-policy-binding PROJECT_ID \
  --member="serviceAccount:SA_NAME@PROJECT_ID.iam.gserviceaccount.com" \
  --role="roles/artifactregistry.writer"
```
Or use roles/artifactregistry.reader for read-only access.

#### 🚀 Deploy to Cloud Run
Now that your agent is in the registry, you can deploy it:
```bash
gcloud run deploy agent-service \
  --image us-central1-docker.pkg.dev/PROJECT_ID/agents-repo/agent-v1 \
  --platform managed \
  --region us-central1
```
---

#### 🧼 Clean Up Unused Images
To avoid cost creep:
```bash
gcloud artifacts docker images list us-central1-docker.pkg.dev/PROJECT_ID/agents-repo
```
Then delete old ones:

```bash
gcloud artifacts docker images delete ...
```
---
#### ✅ Summary
| What You Did                             | Why It Matters                        |
| ---------------------------------------- | ------------------------------------- |
| Created Docker repo in Artifact Registry | Store agent containers securely       |
| Built & pushed agent images              | Deploy agents in Cloud Run or GKE     |
| Used IAM to control access               | Production-ready and secure workflows |
