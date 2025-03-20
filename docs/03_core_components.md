# Core Components of Agentic AI in Amazon Bedrock

## 3.1 Foundation Models (FMs)
Amazon Bedrock offers a range of **pre-trained foundation models (FMs)** optimized for different AI tasks.

### 🔹 Amazon Titan (AWS)
- Developed by AWS for **general-purpose AI** tasks.
- Supports **text generation, embeddings, and multimodal processing**.

#### 📌 Example: Text Embeddings with Amazon Titan
```python
import boto3
import json

client = boto3.client('bedrock-runtime')
prompt = "Generate an embedding for 'AI-powered automation'."

response = client.invoke_model(
    modelId='amazon.titan-embed-text-v1',
    body=json.dumps({"inputText": prompt})
)
print(json.loads(response['body'].read()))
```

### 🔹 Anthropic Claude
- **Optimized for chat, reasoning, and summarization**.
- Provides human-like conversations and better contextual awareness.

#### 📌 Example: AI-Powered Virtual Assistant
```python
prompt = "Draft an email to schedule a meeting for next Monday."
response = client.invoke_model(
    modelId='anthropic.claude-v1',
    body=json.dumps({"prompt": prompt, "max_tokens": 100})
)
print(json.loads(response['body'].read())['completion'])
```

### 🔹 AI21 Labs Jurassic-2
- Best for **long-form content generation**.
- Suitable for articles, blogs, and creative writing.

### 🔹 Stable Diffusion
- **Image generation model** for creating high-quality AI-generated images.

#### 📌 Example: Generating an AI Image with Stable Diffusion
```python
prompt = "Generate an image of a futuristic AI city."
response = client.invoke_model(
    modelId='stability.stable-diffusion-v2',
    body=json.dumps({"prompt": prompt})
)
print("Image generated successfully.")
```

---

## 3.2 Orchestration & Planning
### 🔹 Multi-Agent Collaboration
- AI models work together to **break down complex tasks** into subtasks.
- Example: **AI-powered workflow automation** with multiple models handling different stages.

### 🔹 Task Decomposition & Execution
- AI identifies **subtasks** and executes them efficiently.

### 🔹 Memory & Context Awareness
- AI agents retain memory for **better decision-making over time**.

#### 📌 Example: AI Task Execution with AWS Lambda
```python
import boto3

lambda_client = boto3.client('lambda')
response = lambda_client.invoke(
    FunctionName='AI_Agent_Task_Handler',
    Payload=json.dumps({'task': 'summarize_report'})
)
print(response['Payload'].read())
```

---

## 3.3 Data & Knowledge Integration
### 🔹 Retrieval-Augmented Generation (RAG)
- Combines foundation models with **real-time data retrieval** for accuracy.

### 🔹 Fine-Tuning Customization
- Tailor models to **specific domains** using custom datasets.

### 🔹 Vector Databases for AI Memory
- **Amazon OpenSearch, Pinecone** store embeddings for memory-based AI applications.

#### 📌 Example: RAG Implementation Using OpenSearch
```python
import boto3

opensearch = boto3.client('opensearch')
response = opensearch.search(
    index='knowledge_base',
    body={'query': {'match': {'text': 'latest AI trends'}}}
)
print(response)
```

---

## 3.4 API & Automation
### 🔹 AWS Lambda for Task Execution
- Automates AI workflows by **triggering events**.

### 🔹 Amazon Step Functions for Workflow Orchestration
- Helps **connect multiple AI models** into a pipeline.

### 🔹 Event-Driven AI Pipelines
- **Use cases:** Automated AI responses, document processing, etc.

#### 📌 Example: AI Workflow Automation with Step Functions
```json
{
    "StartAt": "InvokeModel",
    "States": {
        "InvokeModel": {
            "Type": "Task",
            "Resource": "arn:aws:lambda:us-east-1:123456789012:function:invoke_bedrock_model",
            "End": true
        }
    }
}
```

---
### 🚀 Next Steps:
Proceed to **[Building an Agentic AI Solution](./04_building_solution.md)** to learn how to integrate all these components.
