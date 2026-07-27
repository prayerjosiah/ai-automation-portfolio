# AI Automation Portfolio

AI Automation Engineer building production-grade workflows with 
n8n, Zapier, Make.com, OpenAI, and Pinecone — with a background 
in business operations that shapes how I design these systems 
around real operational bottlenecks, not just technical demos.

Each project below includes the live system, a Loom walkthrough, 
and the workflow architecture.

## Featured Projects

### 🎯 AI Lead Qualification System
Typeform → AI scoring → HubSpot CRM → Slack + email routing, with 
production error handling (API failure alerts, malformed response 
recovery, unified error channel).
→ [Watch Demo](https://www.loom.com/share/fe48863287214eb09d9ed794d0c6e815) | [Workflow JSON](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/lead-qualification/Social%20Media%20Agency%20(Lead%20Qualification).json) | [Error Handler](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/lead-qualification/Spark%20Agency%20-%20Error%20Handler.json)

### 🤖 Maya — AI Receptionist
Conversational AI agent handling lead qualification, booking, and 
returning-client updates via a stateful chat interface, with 
idempotent CRM writes and real-time team alerting.
→ [Watch Demo](https://www.loom.com/share/f07fbf346e264167b02c3ecfcd5f596f) | [Workflow JSON](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/maya-receptionist/AI%20Receptionist%20_%20Social%20Media%20Agency.json)

### 📚 RAG Knowledge Base
Multi-tenant retrieval system with namespace-based access control 
— public-facing FAQ/pricing bot and a separate internal SOP/HR 
assistant, both querying the same Pinecone index.
→ [Watch Demo](https://www.loom.com/share/578d78799aec4e5f9b9b43f6e694662d) | [Ingestion Pipeline](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Ingestion%20Pipeline.json) | [Public Query](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Query%20(Public).json) | [Internal Query](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Query%20(Internal).json)

### ⚡ AI Lead Qualification & Routing (Zapier + GoHighLevel)
Two-workflow system demonstrating human-in-the-loop AI automation. Leads submit through a GoHighLevel form; an AI model scores qualification 0–100 and routes via a four-way split — auto-qualify, auto-disqualify, human-review, and a dedicated malformed-response error path. Mid-band leads pause and escalate to Slack with one-click approve/reject; nothing acts on the lead until a human decides. On approval, a second AI step generates personalized outreach referencing the lead's specific business and challenge.

Engineering highlights: direct GoHighLevel REST API integration (authenticated PUT/GET) where the Zapier connector couldn't target custom fields; a JavaScript transform normalizing GHL's raw custom-field arrays into clean named variables; and an idempotency guard that writes decision state before downstream actions to prevent duplicate processing from double-clicks or link pre-fetching. 
→ [Watch Demo](https://www.loom.com/share/53c3d752986c42bf934b573967d6e6e4)| [Score & Route (Zap 1)](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/Lead%20Qualification%20%26%20Routing/Lead%20Qualification%20%26%20Routing%20%E2%80%94%201.%20Score%20%26%20Route.json) | [Resume on Approval (Zap 2)
](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/Lead%20Qualification%20%26%20Routing/Lead%20Qualification%20%26%20Routing%20%E2%80%94%202.%20Resume%20on%20Approval.json)
