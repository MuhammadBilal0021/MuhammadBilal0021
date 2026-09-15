<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=24&pause=1000&color=00D9FF&center=true&vCenter=true&width=620&height=50&lines=Hi+%F0%9F%91%8B%2C+I%27m+Muhammad+Bilal;AI+Engineer+%E2%80%94+Agentic+Systems;LangGraph+%C2%B7+RAG+%C2%B7+Voice+Agents+%C2%B7+Python;Open+to+new+roles+%C2%B7+EU+relocation" alt="Typing SVG" />

### I build multi-agent systems that take real actions — and the guardrails that make that safe

[![Portfolio](https://img.shields.io/badge/PORTFOLIO-Live_Demos-00D9FF?style=for-the-badge&logo=vercel&logoColor=black)](https://portfolio-mocha-xi-90.vercel.app/)
[![GitHub](https://img.shields.io/badge/GitHub-MuhammadBilal0021-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/MuhammadBilal0021)
[![Email](https://img.shields.io/badge/Email-muhammdbilal759021%40gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:muhammdbilal759021@gmail.com)
[![Phone](https://img.shields.io/badge/WhatsApp-%2B92_325_5185049-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/923255185049)

</div>

---

## 👨‍💻 About

```yaml
name:         Muhammad Bilal
role:         AI Engineer — Agentic Systems
location:     Islamabad, Pakistan 🇵🇰  ·  open to relocation (EU) and remote roles
experience:   ~2 years across INVogue Solutions, HA Solutions and Zaptal, plus ongoing freelance
education:    BS Software Engineering, SZABIST Islamabad
              Spring 2022 – Fall 2025 · degree conferred Feb 2026
              4-year programme, 8 semesters, 130+ credit hours · HEC-recognised · NCEAC-accredited
focus:        [LangGraph, multi-agent orchestration, RAG, voice agents, agent control layers, FastAPI]
currently:    AI Engineer (Agentic Systems) at Zaptal — production multi-agent + voice AI
fun_fact:     Grandmaster-certified chess player ♟️ (National Chess Federation of Pakistan)
```

I moved from classical NLP → full-stack client delivery → production agentic AI in under two years. Most of the agentic depth below is **self-directed**: the projects section is independent work I built outside employment, with the commit history public.

---

## 🏭 What I ship at work — Zaptal

Production systems, not demos. The numbers are measured, not estimated.

| | |
|---|---|
| **Multi-agent orchestration** | LangGraph — tool-calling loops, checkpointed state, interrupt/resume handling, Pydantic-validated structured output. Shipped end-to-end across Next.js, FastAPI and PostgreSQL. |
| **Agent control layer** | Tool allow-lists enforced in **application code** · human-approval gates on destructive actions · loop detection · per-task cost guards. See [how I think about agents](#-how-i-think-about-agents) below. |
| **Voice agents** | Autonomous outbound agents on Vapi + Deepgram + ElevenLabs over Twilio telephony — **sub-800 ms first-response latency**, with barge-in handling. |
| **Streaming RAG** | Serving **6 internal APIs**. Cut hallucination **~35%** via citation-grounded generation + Cohere re-ranking. |
| **Delivery** | Own CI/CD and Docker deploys to AWS (EC2 + ECS). Took releases from **manual weekly → automated daily**. |

---

## 🧭 How I think about agents

Anyone can make an agent that works in a demo. The hard part is making one that is safe to point at real systems, cheap enough to run, and debuggable when it goes wrong at 2am. These are the design commitments behind everything I build:

**1. The prompt is not a security boundary.**
Instructions in a prompt can be overridden by anything that reaches the model — user input, a retrieved document, a tool result. So permissions never live in the prompt. They live in application code as an explicit **tool allow-list**: the agent can only invoke what the runtime permits, regardless of what it was told or what it read.

**2. Destructive actions require a human, by default.**
Anything that mutates state irreversibly — sending, deleting, paying, publishing — routes through a **human-approval gate**. The agent prepares the action and the payload; a person authorises it. Read-only operations run free, because gating everything makes the system useless.

**3. Loops are a failure mode, not a personality quirk.**
Agents get stuck: the same tool call, the same error, the same retry. So there's **loop detection** (repeated call signatures, no-progress detection) and a **step budget**. On breach, the run terminates with a structured reason rather than burning tokens until someone notices.

**4. Cost is a first-class design constraint.**
Every task carries a **cost guard** — a ceiling per run. Token spend per task is instrumented, not guessed. An agent that is 3% more accurate and 8× more expensive is usually the wrong agent.

**5. Structured output is validated at the boundary, not trusted.**
Every tool argument and every agent response passes a **Pydantic schema** before anything acts on it. An LLM returning plausible-looking malformed JSON is the most common way these systems fail quietly in production.

**6. Retrieval quality is measured, not vibes.**
RAG pipelines get an **evaluation set** and are re-run as a regression gate. Hallucination reduction is reported against that set, not against a handful of eyeballed answers.

### 🚫 What I refuse to let an agent do — and why

This is the part most agent projects skip, and the part I get asked about most:

| I don't let it… | Because… |
|---|---|
| **Call a tool that isn't on the allow-list** | Capability should be granted by the runtime, not negotiated with the model. |
| **Take an irreversible action without a human gate** | The cost of one wrong send/delete/pay is unbounded; the cost of one approval click is not. |
| **Treat retrieved text as instructions** | A document that says "ignore previous instructions" is data, not a command. Retrieval is an untrusted input channel. |
| **Retry indefinitely** | Persistence without a budget is just an expensive way to be stuck. |
| **Report confidence it doesn't have** | If retrieval returned nothing relevant, the answer is "I don't know," grounded in what was searched. |
| **Write outside its own output schema** | Downstream systems should never have to defend themselves against the model. |

---

## 🚀 Featured projects

<table>
<tr>
<td width="50%">

### 🧠 [OmniAgent](https://github.com/MuhammadBilal0021/multi-platform-agent)
Multi-platform autonomous agent — **persistent memory, task scheduling and tool use** across platforms. Full state machine with a tool-use loop, interruption handling and schema-validated output.

`LangGraph` `FAISS` `FastAPI` `APScheduler`

</td>
<td width="50%">

### 🛰️ [GeoFloodAgent](https://github.com/MuhammadBilal0021/GeoFloodAgent)
Satellite flood damage assessment — **SegFormer semantic segmentation over Sentinel imagery**, feeding an agentic layer that produces structured damage reports. CV + LLM + real-world geospatial data.

`SegFormer` `Sentinel` `Computer Vision` `Agentic reporting`

</td>
</tr>
<tr>
<td width="50%">

### 📊 [AUTO_ml_eda](https://github.com/MuhammadBilal0021/AUTO_ml_eda)
Upload a CSV → automated EDA → AutoML benchmarking across **4 model families** → plain-English insights via Llama 3.3 70B as the agentic decision layer.
**Churn AUC 0.94 · Sentiment F1 0.89**

`scikit-learn` `XGBoost` `NumPy` `Pandas` `Llama 3.3`

</td>
<td width="50%">

### 📄 [Secure RAG Agent](https://github.com/MuhammadBilal0021/rag-document-assistan)
Production retrieval-augmented Q&A. Real-time retrieval with **streaming under 300 ms**, third-party integration via **6 FastAPI endpoints**, containerised and latency-optimised.

`FastAPI` `Docker` `Vector DB` `Streaming`

</td>
</tr>
<tr>
<td width="50%">

### 🎯 [LeadFlow AI](https://github.com/MuhammadBilal0021/leadflow-ai)
AI-driven lead generation and qualification pipeline.

`Python` `LLM automation`

</td>
<td width="50%">

### 🔊 Voice agent work — production, Zaptal
Autonomous outbound agents: **sub-800 ms first response**, barge-in handling, streaming ASR/TTS over Twilio. The rarest line on my CV — most applicants have never put a voice agent in front of a real user.

`Vapi` `Deepgram` `ElevenLabs` `Twilio`

</td>
</tr>
</table>

**On my portfolio (live demos, not published as repos):**
**AI Conversational Data Agent** — natural-language → SQL over a live database with summarised insights on top of the result · `NL2SQL` `LLM` `SQL`
**HealthTailor** — full-stack app, end-to-end ownership of schema, API, UI and deploy · `Next.js` `Gemini` `Firebase` `TypeScript`

<div align="center">

**🔗 Live demos and walkthroughs:** [portfolio-mocha-xi-90.vercel.app](https://portfolio-mocha-xi-90.vercel.app/) · source: [`Portfolio`](https://github.com/MuhammadBilal0021/Portfolio) (TypeScript)

</div>

---

## 🛠️ Stack

<div align="center">

**Agentic AI / LLM**

![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-Agents-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?style=for-the-badge&logo=openai&logoColor=white)
![Hugging Face](https://img.shields.io/badge/HuggingFace-Transformers-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![Groq](https://img.shields.io/badge/Groq-Llama_3.3-F55036?style=for-the-badge&logo=groq&logoColor=white)

**Voice AI**

![Deepgram](https://img.shields.io/badge/Deepgram-Streaming_ASR-13EF93?style=for-the-badge&logoColor=black)
![ElevenLabs](https://img.shields.io/badge/ElevenLabs-TTS-000000?style=for-the-badge&logoColor=white)
![Twilio](https://img.shields.io/badge/Twilio-Telephony-F22F46?style=for-the-badge&logo=twilio&logoColor=white)
![Vapi](https://img.shields.io/badge/Vapi-Voice_Agents-00D9FF?style=for-the-badge&logoColor=black)

**Backend & data**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

**Frontend**

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)

**ML & retrieval**

![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Model_Benchmarks-A81620?style=for-the-badge&logoColor=white)
![FAISS](https://img.shields.io/badge/FAISS-Vector_Search-00D9FF?style=for-the-badge&logoColor=black)
![Pinecone](https://img.shields.io/badge/Pinecone-Vector_DB-000000?style=for-the-badge&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

**Cloud, delivery & testing**

![AWS](https://img.shields.io/badge/AWS-EC2_·_ECS_·_S3-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![CI/CD](https://img.shields.io/badge/CI%2FCD-Automated_Daily-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-Eval_Harness_+_CI_Gate-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white)

</div>

<details>
<summary><b>Also in daily use</b></summary>

**Models & providers:** Claude · Gemini · Llama 3.3 · Cohere (re-ranking) · Tavily (search)
**Retrieval:** ChromaDB · hybrid retrieval · chunking strategies · citation grounding
**Agents:** CrewAI · MCP · structured output (Pydantic / JSON schema) · human-in-the-loop gating · LLM evaluation
**Voice:** streaming ASR/TTS · barge-in handling · telephony flows
**AI-assisted development:** daily power-user of Claude Code and Cursor. Agents write a large share of my code, so I've built review checklists and eval gates for their output — the same control-layer thinking, pointed at my own workflow.

</details>

---

## 📚 Research & writing

- 📄 **"Automated Resume Screening Using NLP Techniques"** — published research paper. The INVogue production screening pipeline (200+ interactions/week, 89%+ accuracy, ~60% reduction in manual screening) grew out of this work. Early prototype: [`ATS-System`](https://github.com/MuhammadBilal0021/ATS-System).
- 🎓 **Deep Learning Specialization** — Coursera
- 📝 I write up what I learn in project READMEs — architecture, the control layer, metrics, and what I got wrong.

---

## 📈 Activity

<div align="center">

![Muhammad's github activity graph](https://github-readme-activity-graph.vercel.app/graph?username=MuhammadBilal0021&theme=tokyo-night&hide_border=true)


</div>

---

## 🌍 Open to work

I'm looking for **AI Engineer / LLM Engineer / Agentic Systems** roles — and I'm also open to **Python backend** and **Forward Deployed Engineer** positions where the work is client-facing and end-to-end.

**Open to relocation across the EU, and to remote roles.** I'd need work-permit sponsorship, and I've done the homework on it: software development is a recognised shortage occupation for the **EU Blue Card**, and my degree is from an **H+** institution on the German Anabin register. In practice that means sponsorship is a documented, fast process rather than an open-ended risk — happy to send any team the specific route, thresholds and timelines for their country.

📫 **muhammdbilal759021@gmail.com** · 📱 +92 325 5185049 (WhatsApp) · 🔗 [portfolio-mocha-xi-90.vercel.app](https://portfolio-mocha-xi-90.vercel.app/)

---

<div align="center">

♟️ **Chess:** Grandmaster-certified, National Chess Federation of Pakistan — the same patience for long positions that debugging an agent loop requires.

**If any of this is useful, a star on the repo is appreciated.**

</div>
