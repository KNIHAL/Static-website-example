# ☁️ Cloud
I assume you already have some basic understanding of cloud computing — why it's important, when to use it, and the general concept.
In this section, we’ll focus only on the cloud services that AI agent developers actually need to know.

There are many cloud providers — AWS, GCP, Azure, IBM, Railway, etc. But in this handbook, we’ll only focus on GCP (Google Cloud Platform) and AWS (Amazon Web Services).

You might be wondering — why only GCP and AWS?
You’ll find the answer very soon.

---

### 🌐 Let’s Start with GCP
GCP (Google Cloud Platform) is one of the most AI-friendly clouds available today.
It offers a wide range of tools tailored specifically for machine learning, LLMs, and AI agent development.

You may have already heard terms like Vertex AI, ADK, or Workbench Notebooks.
If not, don’t worry — we’ll explore all of these in detail.

Everything related to GCP is documented inside the gcp/ folder.
Here are the services we will cover:

- Vertex AI Workbench Notebooks
- Cloud Run
- Vertex AI Builder
- Agent Development Kit (ADK)
- Agent Garden (for testing and practicing with sample agents)
- Learning RAG (Retrieval-Augmented Generation) and building RAG projects
- Cloud Storage
- IAM (Identity and Access Management)
- Gemini API Key (Accessing Gemini models)
- Container Registry (GCP’s Docker image hosting)
- Vertex AI Agent Builder
- Vertex AI Search (for RAG)
- Vertex AI Vector Search
- Vertex AI Pipelines
- Vertex AI Model Monitoring
- Cloud Logging & Monitoring
- Secret Manager
- Cloud Build (Advanced use cases)
- Databases: Cloud SQL, AlloyDB, Firestore
- Billing & Cost Management
- Security (Service Accounts, VPC Service Controls, Encryption)

Each service has its own separate file with detailed usage instructions, examples, and tips specific to AI agent development.

---

### ☁️ What About AWS?
AWS (Amazon Web Services) is beginner-friendly and great for DevOps and deployment.
While AWS does support AI tools (like Bedrock), it’s not as seamless as GCP when building agents from scratch.

That said, AWS wins when it comes to:

Clean UI and simpler console

Easier service onboarding (no need to manually enable APIs)

Faster initial setup

Cheaper for small experiments

Great for Docker-based deployments (e.g., running Flowise, Langflow)

Strong DevOps and infra tools

We’ll primarily use AWS for hosting tools, managing Docker containers, and experimenting with agentic servers.

Here’s what we’ll cover inside the aws/ folder:

- EC2 Instances
- Security Groups
- Elastic IP (EIP)
- S3 Buckets
- RDS (Relational Database Service)
- AWS Lambd
- Bedrock (for LLMs like Claude, Titan, Mistral, etc.)
- Transcribe, etc.
___


### 🧠 Which Cloud Should You Use?
Good question.

    I’ve personally worked with both AWS and GCP, and here’s my honest breakdown:

#### ✅ AWS — Pros & Cons
**Pros**

- Clean and beginner-friendly UI
- Easy to launch services (EC2, S3, Lambda)
- Great for quick DevOps use cases
- No need to manually enable services
- Rich ecosystem of integrations

**Cons**

- Slightly more expensive than GCP
- Some AI features are limited or paid (Bedrock)
- SSH and permission issues are common in EC2

#### ✅ GCP — Pros & Cons
**Pros**

- Built specifically for AI development
- Workbench notebooks, Agent Garden, ADK – huge plus
- Vertex AI tools are production-grade
- RAG, vector DB, and agent pipelines are easier to manage

**Cons**

- UI is cluttered and not beginner-friendly
- Services need to be enabled manually
- Learning curve is steep without prior experience
- You need to know Docker to use tools like Cloud Run

---
### ✍️ Final Note

**This is based on my personal experience. You don’t need to switch platforms if you’re already comfortable with one. The goal is not to master the cloud itself, but to learn how to leverage it for building, running, and deploying AI agents.**

>Some of you might wonder why I haven’t included Azure.
>Honestly, I haven’t explored it deeply yet — but once I do, I’ll update this section with practical Azure resources for AI agents too.


