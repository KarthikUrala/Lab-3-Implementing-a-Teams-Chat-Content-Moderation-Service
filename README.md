# 🔒 Microsoft Teams Moderation Workflow with Azure Logic Apps

This project implements a real-time moderation system for Microsoft Teams using Azure Logic Apps and Azure AI Content Safety. The system automatically analyzes messages posted in Teams channels and sends an email alert if inappropriate content is detected.

<img width="1612" height="776" alt="Image" src="https://github.com/user-attachments/assets/09416191-819b-4074-9bdf-f7ff253b0ce2" />

## 🔧 Logic App Setup

### **Trigger:**
- **Connector:** Microsoft Teams
- **Action:** `When a new message is added to a chat or channel`
- Purpose: Captures new messages posted in the selected channel in real time.

### **Loop:**
- **Action:** `For Each`
- Used to process each message in a batch (Microsoft Teams may return multiple messages).

### **Message Retrieval:**
- **Action:** `Get message details`
- Ensures the full message content is extracted from Teams.

### **Content Safety API Integration:**
- **Action:** HTTP POST request
- **Target:** Azure AI Content Safety API (`eastus.api.cognitive.microsoft.com`)
- **Payload:** Includes message text and analysis categories (hate, violence, sexual, self_harm)

### **Condition Block:**
- Custom expression checks:
  ```text
  If any severity score > 0

---

## 📌 Features

- Listens to new messages in a Microsoft Teams channel
- Analyzes content using Azure AI Content Safety (Hate, Violence, Sexual, Self-harm)
- Triggers alert emails when violations occur
- Serverless and scalable using Logic Apps and HTTP connector
- Fully customizable and extendable

Recommendations for Future Improvements
✅ Store flagged messages in Azure Table Storage for audit trails

✅ Visualize moderation history in Power BI via Logic App logs

✅ Auto-notify the user via Teams chatbot or Adaptive Card

✅ Integrate Azure Functions for pre-processing or translation

✅ Add retry policy for HTTP failures

## Youtube link- [https://youtu.be/275cG0HjyQg](https://www.youtube.com/watch?v=275cG0HjyQg&ab_channel=KarthikRaghavendraUrala)

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
