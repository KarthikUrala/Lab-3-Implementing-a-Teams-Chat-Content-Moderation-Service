# 🔒 Microsoft Teams Moderation Workflow with Azure Logic Apps

This project implements a real-time moderation system for Microsoft Teams using Azure Logic Apps and Azure AI Content Safety. The system automatically analyzes messages posted in Teams channels and sends an email alert if inappropriate content is detected.

---

## 📌 Features

- Listens to new messages in a Microsoft Teams channel
- Analyzes content using Azure AI Content Safety (Hate, Violence, Sexual, Self-harm)
- Triggers alert emails when violations occur
- Serverless and scalable using Logic Apps and HTTP connector
- Fully customizable and extendable

---

## 🔧 Architecture Overview

```mermaid
flowchart TD
    A[Teams Trigger<br>New message in channel] --> B[For Each Message]
    B --> C[Get Message Details]
    C --> D[HTTP Request to Content Safety API]
    D --> E{Is any category<br>severity > 0?}
    E -- Yes --> F[Send Email Notification]
    E -- No --> G[No Action]
