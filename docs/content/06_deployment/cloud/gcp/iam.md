# IAM (Identity and Access Management)
**Google Cloud’s Identity and Access Management (IAM) system controls who has what access to which resources in your GCP project.**

For AI agent developers, IAM is not just a backend topic — it's essential for:

- Granting agents access to APIs (like Vertex AI or Cloud Storage)
- Creating service accounts for agent workflows
- Managing roles and permissions securely
- Avoiding access errors due to misconfigured policies

---

### 🚀 Why IAM Matters for Agents
| Use Case                             | IAM Usage                                          |
| ------------------------------------ | -------------------------------------------------- |
| Using Gemini API                     | Attach API key to a service account                |
| Deploying agent on Cloud Run         | Bind service account with proper roles             |
| Saving outputs to Cloud Storage      | Grant write access to the agent                    |
| Accessing vector stores or pipelines | Enable scoped permissions for privacy and security |

---

### 🔐 Key IAM Concepts
1. Identities

These are who is accessing a resource. Could be:
- Google accounts
- Service accounts (used by agents or apps)
- Google Groups
- G Suite domains

2. Roles

These are what the identity can do. Examples:

- `roles/viewer`: Read-only access
- `roles/editor`: Full access except billing
- `roles/aiplatform`.user: Required for using Vertex AI

Use **predefined roles** or custom roles if needed.

3. Policies

IAM policies bind members (identities) to roles on resources.

Example policy snippet:
```json
{
  "bindings": [
    {
      "role": "roles/aiplatform.user",
      "members": [
        "serviceAccount:my-agent@appspot.gserviceaccount.com"
      ]
    }
  ]
}
```

---

#### 🛠️ Setting Up IAM for Agents (Step-by-Step)
✅ Step 1: Create a Service Account

Go to:
Console > IAM & Admin > Service Accounts > Create

Give it a name like:
agent-executor-sa

✅ Step 2: Assign Required Roles

Click on the created service account → Permissions → Grant Access

Common roles for agents:
- Vertex AI User
- Storage Admin (for file read/write)
- Service Account Token Creator (for impersonation)

✅ Step 3: Attach to Agent Environment

If you're deploying the agent on:

- Cloud Run: Bind the service account at deploy time
- Vertex AI: Specify service account in job/pipeline settings

---

#### 🧪 Quick Tips
- Always follow the principle of least privilege.
- Never hardcode API keys. Use service accounts or Secret Manager.
- Monitor access via Cloud Audit Logs.
- Use IAM Conditions if you want time-based or context-aware policies.

---
### ✅ Useful CLI Commands
```bash
# List current IAM policies for a project
gcloud projects get-iam-policy [PROJECT_ID]

# Add role to a service account
gcloud projects add-iam-policy-binding [PROJECT_ID] \
  --member="serviceAccount:my-sa@project.iam.gserviceaccount.com" \
  --role="roles/aiplatform.user"
```

--- 
### 📎 When Agents Fail Due to IAM
If your agent says things like:

`403 PERMISSION_DENIED`

`The caller does not have permission`

Then IAM is the first place to check. Either the service account doesn't have the right role, or it's not attached to the environment.