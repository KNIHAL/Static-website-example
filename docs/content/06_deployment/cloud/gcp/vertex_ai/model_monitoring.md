# Vertex AI Model Monitoring

Vertex AI Model Monitoring lets you track and analyze the performance of deployed models and agent endpoints over time. For agent developers, it’s critical to ensure your agents are stable, accurate, and safe after deployment — and this service helps automate that.

---

### Why It Matters for AI Agents
AI agents rely on multiple moving parts: LLMs, tool outputs, RAG pipelines, and APIs. If any part starts failing silently or degrading in performance (e.g., hallucinations, slow responses, or broken tool calls), you need to know immediately.

- Monitoring allows you to:

- Detect data drift and prediction drift

- Monitor latency and tool errors

- Track user feedback (thumbs up/down)

- Create alerts and dashboards in real-time

----

### What Can You Monitor?
| Category           | Monitored Element                  |
| ------------------ | ---------------------------------- |
| Input Drift        | Prompt content or tool inputs      |
| Prediction Drift   | LLM responses, API outputs         |
| Latency & Errors   | Agent endpoint response time       |
| Custom Signals     | User satisfaction, success/failure |
| Integration Health | Tool and external API availability |

---

#### How It Works
1. Deploy your agent as a Vertex AI endpoint (e.g., via Cloud Run or Model Registry).

2. Enable model monitoring on that endpoint.

3. Configure:

- Objective type (e.g., prediction drift)

- Schema of input/output

- Alert thresholds

4. Use logs, metrics, and dashboards to observe behavior.

----

#### Integration Example: Tool Error Monitoring
You can push custom logs from your agent to Vertex AI Monitoring:
```python
from google.cloud import aiplatform_v1
log_client = aiplatform_v1.PredictionServiceClient()

log_client.upload_model_monitoring_stats_anomalies(
    model_endpoint=your_endpoint,
    stats_data={
      "tool_error_rate": 0.15,
      "response_latency_ms": 2300
    },
)
```

---
#### Setup Guide
1. Enable Monitoring in the GCP Console under Vertex AI > Endpoints.

2. Upload baseline data (optional).

3. Configure alerting policy with Cloud Monitoring.

4. Visualize data in Cloud Logging or BigQuery.

----

#### Best Practices
1. Log important events: tool calls, tool failures, user inputs.

2. Monitor both system metrics (latency, error rate) and human metrics (feedback, confidence).

3. Use structured logging for easy parsing.

4. Enable Slack or email alerts for failures.

5. Evaluate agent updates with monitoring history before rolling out.

---

#### When to Use
- You're deploying production-grade agents.
-  You want to catch failures or performance issues early.
-  You care about long-term agent quality assurance.
- You’re integrating external APIs or RAG sources.