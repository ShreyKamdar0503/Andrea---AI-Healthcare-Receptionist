# Andrea---AI-Healthcare-Receptionist
Andrea is a production-ready, multi-agent voice AI receptionist for a dental clinic, built using VAPI, GPT-4o-mini, n8n workflows, and an MCP server. It handles real-world phone conversations including appointment scheduling, intake, insurance checks, and call logging with low latency and high reliability.

This project demonstrates how to build **reliable, low-latency voice AI systems** that go beyond simple chatbots and operate successfully in real production environments.

---

## 🚀 Features

- Natural, open-ended voice conversations (no IVR menus)
- Multi-agent architecture with strict scopes
- Appointment booking, updating, and cancellation
- Symptom-based triage for dental concerns
- Insurance confirmation using a knowledge base
- Persistent context across conversation flows
- Automated CRM updates via n8n
- End-of-call (EOC) reporting via webhook
- Production phone number + website widget deployment

---

## 🧠 System Architecture Overview

Andrea is built using a **router + specialist agent model**:

### 🔀 MCP Router Agent
Analyzes caller intent and routes the conversation to the appropriate specialist workflow.

### 🧩 Specialist Agents (7 Total)

1. **Greeting & General Inquiry Agent**  
   Answers high-level questions (hours, services, insurance, doctors) using a knowledge base.

2. **CRM Lookup Agent**  
   Looks up existing patients via n8n using normalized email input.

3. **New Patient Intake Agent**  
   Collects name, email, and phone only when required and creates CRM records.

4. **Appointment Availability Agent**  
   Checks availability via n8n while enforcing clinic operating hours.

5. **Appointment Booking Agent**  
   Performs symptom-based triage, books appointments, assigns doctors, and confirms details.

6. **Appointment Update & Cancellation Agent**  
   Modifies or deletes appointments safely with conflict checks.

7. **Insurance Confirmation Agent**  
   Confirms accepted insurance plans and advises patients on required documents.

---

## 🔌 MCP Server (n8n Integration)

The MCP Server acts as the communication layer between VAPI and n8n:

- Receives structured tool calls from the voice agent
- Routes requests to the correct n8n workflow
- Executes CRM and scheduling logic
- Returns results back to the voice agent in real time

This ensures strict tool boundaries and prevents hallucinated API behavior.

---

## 📞 End-of-Call (EOC) Reporting

After each call, VAPI triggers a webhook that:

- Extracts the call summary and outcome
- Appends a new row to a Google Sheets **Call Log**
- Stores timestamped records for auditing and QA

---

## 🏗️ Tech Stack

- **Voice Platform:** VAPI
- **LLM:** OpenAI GPT-4o-mini (cluster)
- **Speech-to-Text / Text-to-Speech:** VAPI native (μ-law, telephony optimized)
- **Automation:** n8n workflows
- **Integration Layer:** MCP Server
- **CRM & Logs:** Google Sheets
- **Telephony:** Twilio
- **Deployment:** Phone number + website widget

---

## ⚙️ Performance Highlights

- <800ms average response latency
- 7 specialized agents (vs. one monolithic agent)
- 100+ simulated and live test calls
- Persistent context across agent handoffs
- ~97% appointment success rate after guardrails

---

## 🧪 Testing Methodology

The system was stress-tested with 100+ simulated calls including:

- Urgent dental emergencies
- Ambiguous scheduling requests
- Mid-call intent changes
- Long pauses and interruptions
- Background noise and real-world speech patterns

Each failure informed a new guardrail or workflow improvement.
