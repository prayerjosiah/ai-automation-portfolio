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
→ [Watch Demo](YOUR_LOOM_LINK_HERE) | [Workflow JSON](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/maya-receptionist/AI%20Receptionist%20_%20Social%20Media%20Agency.json)

### 📚 RAG Knowledge Base
Multi-tenant retrieval system with namespace-based access control 
— public-facing FAQ/pricing bot and a separate internal SOP/HR 
assistant, both querying the same Pinecone index.
→ [Watch Demo](YOUR_LOOM_LINK_HERE) | [Ingestion Pipeline](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Ingestion%20Pipeline.json) | [Public Query](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Query%20(Public).json) | [Internal Query](https://github.com/prayerjosiah/ai-automation-portfolio/blob/main/workflows/rag-knowledge-base/Spark%20Agency%20_%20RAG%20Query%20(Internal).json)
