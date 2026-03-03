# CLAUDE.md
## AI Workflow Automation Architecture – n8n + AI + Voice Systems

---

## 1. Overview

This project defines a production-level AI automation architecture designed to transform manual business processes into scalable, AI-driven workflow systems.

The system leverages:

- n8n as the workflow orchestration engine
- GPT-based AI models for structured decision logic
- REST API integrations (CRM, payments, internal tools)
- Optional voice automation layer (Vapi / Retell)
- Structured logging, monitoring, and lifecycle automation

This architecture is built for scalability, maintainability, and long-term operational stability.

---

## 2. Core Architecture

### High-Level Flow

Inbound Trigger
→ Data Validation
→ AI Decision Layer (Structured JSON)
→ Business Logic Routing
→ External API Integrations
→ CRM Update
→ Notification Layer
→ Logging & Monitoring

---

## 3. Technology Stack

### Orchestration
- Self-hosted n8n (Docker-based deployment)

### AI Layer
- OpenAI GPT API (JSON structured output mode)

### Voice Layer (Optional)
- Vapi (Voice AI Infrastructure)
- Retell AI (Low-latency voice conversations)

### CRM & Integrations
- GoHighLevel
- HubSpot
- Custom REST APIs

### Communication
- Twilio (SMS / Voice)
- Slack (Internal alerts)
- SMTP / Email API

### Database Layer
- PostgreSQL / Supabase
- CRM-native storage

---

## 4. AI Decision Framework

AI is used strictly for structured decision-making, not free-form output.

All AI prompts must enforce JSON responses.

### Example Prompt Template

You are a business automation assistant.

Extract and classify:
- intent
- urgency
- budget
- service_type
- confidence_score

Return JSON only in this format:

{
  "intent": "",
  "urgency": "",
  "budget": "",
  "service_type": "",
  "confidence_score": ""
}

This allows deterministic routing inside n8n workflows.

---

## 5. Workflow Design Principles

1. Webhook-first trigger design
2. Stateless processing when possible
3. Structured AI outputs only
4. Clear IF/ELSE routing logic
5. Error-handling branch for every external API
6. Centralized logging
7. Idempotent execution to prevent duplicates
8. Modular workflow separation

---

## 6. Production Workflow Example

### AI Lead Qualification System

Trigger:
Webhook (Inbound form submission)

Flow:

1. Validate required fields
2. Send input to GPT for classification
3. Parse JSON response
4. Route based on lead_score:
   - High Intent → Priority Pipeline + Slack Alert
   - Medium Intent → Standard Pipeline
   - Low Intent → Nurture Campaign
5. Push structured data to CRM via API
6. Log transaction to database
7. Send confirmation email

---

## 7. Voice Agent Architecture (Optional)

### Flow Structure

Inbound Call
→ Speech-to-Text
→ GPT Decision Logic
→ n8n Business Workflow
→ CRM / Calendar API
→ Response Generation
→ Text-to-Speech
→ Caller

Voice Responsibilities:
- Capture caller information
- Detect intent
- Check availability
- Book appointments
- Save transcript
- Log call outcome

All voice systems must send structured payloads to n8n via authenticated webhook.

---

## 8. API Integration Standards

Supported Methods:
- GET (retrieve data)
- POST (create resource)
- PATCH (update resource)
- DELETE (remove resource)

All API calls must include:
- Authentication handling
- Response validation
- Error routing branch
- Retry mechanism
- Timeout configuration

---

## 9. Monitoring & Optimization

Each workflow must include:

- Execution logging
- Error logging
- Failure alerts (Slack / Email)
- Token usage monitoring (AI calls)
- Performance review checkpoints

Optimization Guidelines:
- Minimize unnecessary GPT calls
- Cache repetitive lookups
- Batch operations when applicable
- Place conditional logic early

---

## 10. Documentation Standard

Each workflow must include metadata:

Workflow Name:
Trigger Type:
External APIs Used:
AI Prompt Reference:
Data Schema Mapping:
Error Handling Logic:
Version:
Last Updated:

---

## 11. Security Standards

- Store credentials in environment variables
- Never hardcode API keys
- Enable webhook authentication
- Validate inbound payload schema
- Implement role-based access control
- Log abnormal behavior
- Enforce HTTPS endpoints

---

## 12. Scalability Strategy

- Modular workflow separation
- Reusable sub-workflows
- Queue-based processing for high volume
- Horizontal scaling via Docker
- Stateless webhook design
- Clean separation between AI logic and business logic

---

## 13. System Philosophy

This automation architecture is designed to:

- Reduce operational bottlenecks
- Eliminate repetitive manual work
- Improve response consistency
- Enable scalable growth
- Maintain clean and structured logic

The objective is not quick automation.

The objective is durable automation infrastructure.

---

## 14. Author Statement

I design AI-driven automation infrastructures that convert business operations into structured, scalable systems.

My approach prioritizes:

- Deterministic AI logic
- Clean API integrations
- Scalable workflow architecture
- Production-grade reliability
- Clear documentation

I build systems that last.
