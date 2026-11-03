---
layout: post
title: "Google Cloud Professional Agentic Architect Exam Guide: Passing the Exam & Challenge Labs"
excerpt: "My journey becoming officially certified as a Google Cloud Professional Agentic Architect. A complete breakdown of Google's first hybrid exam: passing the 3-hour theory proctored exam and clearing the hands-on challenge labs."
subtitle: "From Theoretical Architecture to Hands-On Lab Implementation"
description: "A comprehensive, architect-level guide for the Google Cloud Professional Agentic Architect certification. Details the full journey across the 3-hour theory exam (beta), passing the hands-on challenge labs on skills.google, and key architectural domains across ADK, Antigravity, and Gemini Enterprise."
thumbnail-img: /assets/img/pcaa/pcaa.png
share-img: /assets/img/pcaa/pcaa.png
readtime: true
share-title: "How to Pass the Google Cloud Professional Agentic Architect Certification (Exam Theory & Hands-on Challenge Labs Guide)"
share-description: "Field notes and hands-on guide for Google Cloud's new Professional Agentic Architect hybrid certification. Practical insights on passing the theory exam, and completing the hands-on challenge labs on skills.google."
tags: [Google Cloud, PCAA, Agentic AI, ADK, Antigravity, Gemini Enterprise, Agent Studio, Agent Gateway, Model Armor, Challenge Labs, Certification, Exam Guide]
---

# Google Cloud Professional Agentic Architect Exam Guide

In September, I sat the brand-new beta for Google Cloud’s latest credential: the **Professional Agentic Architect**. 

Google has taken a fundamentally new direction with this track. Rather than relying solely on traditional multiple-choice questions, this is Google Cloud’s first **hybrid certification**. Earning the badge requires clearing two distinct stages: a proctored theoretical exam (Part 1), followed by a hands-on lab assessment delivered through Google Skills (Part 2).

Having built applications using Google’s Agent Development Kit (ADK), working daily across the Gemini Enterprise ecosystem in my day job, and using Antigravity regularly in my own workflows, I wanted to see how Google approached evaluating enterprise agent architecture. 

After completing the proctored exam and subsequently clearing the challenge labs, I am now **officially certified Google Cloud Professional Agentic Architect**, taking me to **14 active Google Cloud certifications** in total. 

Here is the breakdown of how the hybrid format works, the OnVUE testing experience, navigating the transition from Part 1 to Part 2, and what to expect when you step into the live challenge labs.

---

## The Remote Proctoring Setup: OnVUE vs. Kryterion Webassessor

With no local test centres nearby, remote proctoring has been my default for years. If you’ve taken Google Cloud certifications previously, you’ll be well accustomed to Kryterion’s Webassessor portal and Sentinel software. Sitting Part 1 of this exam was my first experience with Pearson VUE’s OnVUE platform following Google’s delivery migration, and the operational differences were noticeable from the start:

* **Mobile-first check-in flow:** OnVUE offloads identity and environment verification directly to your phone. Once you launch the session on your laptop, you scan a QR code to capture high-res photos of your ID, snap a verification selfie, and submit four clear angle shots of your workspace (front, back, left, right) before placing the phone out of arm's reach.
* **Rescheduling flexibility:** Client deliverables ramped up right before my initial test date, forcing me to push my slot back. OnVUE’s rescheduling was remarkably painless compared to Webassessor—there was wide availability across alternative time slots, and the system let me adjust the booking right up to the start time without friction.
* **The queue and proctor sweep:** I logged in 15 minutes ahead of my scheduled window to run automated system, mic, and webcam checks. Once my phone photos were submitted, I entered a queue at position 13, taking just under 15 minutes for a proctor to connect. While Webassessor leaned heavily on background biometric profiles, OnVUE proctors are much more hands-on—requiring me to lift my laptop for an active 360-degree sweep of the entire room, including the space underneath the desk and behind the laptop screen, before unlocking the test.
* **The clean-desk reality:** While the delivery platform has changed, the remote testing discipline hasn't. The strict clean-desk policy hasn’t changed: second monitors must be unplugged and turned away, paper and clutter completely cleared, and your workspace kept entirely bare throughout the session.

---

## Part 1: The Proctored Exam & The Beta Dynamic

Because this was a beta, the format differed slightly from what the final General Availability (GA) exam will look like:

| Component | Beta Version | General Availability (GA) |
| :--- | :--- | :--- |
| **Part 1 Exam Duration** | **3 hours (180 minutes)** | **2 hours (120 minutes)** |
| **Question Count** | 75 questions | 50–60 questions |
| **Part 2 Challenge Labs** | 3 options presented (must pass 2) | 3 options presented (must pass 2) |
| **Registration Fee** | $120 USD (40% beta discount) | $200 USD (standard retail) |
| **Part 1 Result Notification** | Log into CertMetrics directly | Expected within 7–10 business days |
| **Credential Validity** | **1 year** | **1 year** |

*Note: Unlike most Google Cloud professional certifications which carry a 2-year validity, this one is valid for **1 year**. Given the rapid evolution of agentic protocols, security tooling, and the fact that we get a new Gemini model drop almost weekly lately, a 12-month shelf life makes sense.* 

### The Exam Experience: A Tale of Two Difficulties
Beta question pools contain uncalibrated questions, which creates a noticeable dynamic:

1. **The deep scenario questions:** Multi-paragraph architectures covering multi-agent handoffs, data leakage boundaries, evaluation pipelines, and token exhaustion. Map out the flow of data and identity between the client, gateway, runtime, and backend tool carefully.

2. **The obvious distractors:** On many questions, two or three options represent glaring anti-patterns you can eliminate right away. For example, ruling out options that:
   * Rely on natural language prompt instructions to enforce hard business or transaction limits, rather than implementing deterministic egress controls in Agent Gateway or IAM boundaries.
   * Grant an agent broad administrative service account roles to "simplify" tool execution, bypassing least privilege.
   * Disable execution sandboxing to speed up dynamic code execution.

Pacing felt comfortable. With 75 questions across 180 minutes, you have roughly 2.4 minutes per question. I wrapped up Part 1 with about 40 minutes remaining, even after reviewing flagged questions.
---

## The Transition: From Part 1 to Part 2 via CertMetrics

While I expect automated email notifications will be in place once the certification rolls out to General Availability, that certainly wasn't the case during my beta run- I never actually received an email confirming I had cleared the theoretical exam. 

If you've completed Part 1 and find yourself waiting around for an inbox, don't wait on it. Head straight to the source:

1. Log directly into the **Google Cloud CertMetrics** portal.
2. Check your exam history to see if your result has updated to a pass.
3. Once your passing status is recorded, you will see the option to launch Part 2 of the certification.
4. Clicking that link routes you straight into your assigned hands-on assessment track on **skills.google**.

---

## Part 2: The Hands-On Challenge Labs

Once you launch Part 2 on skills.google, you enter the practical evaluation phase. 

### Lab Structure & Rules
* **3 Challenge Labs Presented- Pass Any 2:** You are presented with a selection of three distinct challenge labs. To achieve certification, you need to successfully **pass two of them**.
* **100% Completion Bar:** Just like standard Google Cloud challenge labs, there is no partial credit. Passing a lab requires achieving a **100% score**, progressing through all milestone assessment checks.
* **Lab Durations:** Google’s estimated completion times ranged from **45 minutes up to 1 hour 30 minutes** depending on the lab complexity. However, the actual allotted lab timer is greater than this, giving you plenty of time if you need to troubleshoot or wait for services to initialize (although this wasn’t an issue for my labs)..
* **Standard Challenge Lab Format:** If you have completed challenge labs on skills.google before, the mechanics will feel immediately familiar: an objective brief, architecture constraints, and an automated tracking script that evaluates your environment as you complete each phase.

### Practical Tips for the Challenge Labs
* **Exact Naming Is Non-Negotiable:** Like every challenge lab on skills.google, the automated background grading scripts look for exact string matches. Whether you are provisioning services in the console or running scripts, copy and paste the resource names, IDs, and variables directly from the lab brief. A single typo will fail a milestone check even if the underlying build is functioning.
* **Respect Propagation Time:** Avoid hitting "Check My Progress" the millisecond a resource shows as created. Cloud control planes and service bindings can take a minute or two to settle across the environment. Rushing the verification check can result in a false-negative score.
* **Read the Whole Brief First:** It's tempting to jump straight into the first objective, but later tasks often impose constraints on earlier setups. Spend the first five minutes reading through all phases of the scenario so you don't build yourself into a corner that requires re-deploying resources on the clock.
* **Console and SDK Familiarity:** Because there are no step-by-step guides, you don't have time to browse reference documentation looking for basic UI paths or command syntax. Practical speed comes from knowing where tools sit in the console and being comfortable working through standard build workflows.

---

## Official Exam Guide Domains & Weightings

The technical requirements for both parts map directly across five documented domains from the [Professional Agentic Architect Exam Guide](https://services.google.com/fh/files/misc/professional_agentic_architect_exam_guide_english.pdf):

| Section | Focus Area | Exam Weighting |
| :--- | :--- | :--- |
| **Section 1** | Building agents using low-code tools | ~13% |
| **Section 2** | Using coding agents for application development | ~17% |
| **Section 3** | Developing custom agents | ~33% |
| **Section 4** | Evaluating and deploying agentic workflows | ~17% |
| **Section 5** | Securing and governing agentic workflows | ~20% |

---

## Core Technical Themes to Master

Whether you are answering architectural questions in Part 1 or implementing resources in Part 2, the following technical themes form the backbone of the credential:

### 1. The Gemini Enterprise Ecosystem & Low-Code Agents (~13%)

To clear this domain, you should be comfortable with:

* **End-to-End Architectural Integration:** Understand how user-facing interfaces (like the Gemini Enterprise app or custom web front-ends) hand off requests down into the managed agent layer, and know where the demarcation line sits between low-code configuration and custom code implementations.
* **Conversational Flow & CX State Management:** Review how state-based multi-turn dialogues are structured in Agent Studio / CX consoles. Be clear on how pages, transition routes, conditional event handlers, and fallback routes operate when guiding user intent.
* **Enterprise Grounding & Data Stores:** Know how to configure managed data stores using Vertex AI Search across both structured and unstructured repositories. Understand how chunking strategies, semantic search, and metadata filtering prevent hallucinations and ensure enterprise answers remain strictly grounded.
* **Tool Extensions & API Contracts:** Understand how low-code agents invoke external business logic. Review how OpenAPI schemas define tool contracts, how authentication is passed to downstream APIs, and how Agent Gateway enforces ingress/egress policies around tool invocation.



* **End-to-End Architecture:** Understand how the front-end application layer links into the agent runtime. Know how conversational agents, tool extensions, and grounded search collaborate to surface enterprise data safely.
* **Agent Studio & CX Workflows:** Review how state-based conversation flows (pages, transition routes, and event handlers) are structured in Customer Experience (CX) Agent Studio and Gemini Enterprise Agent Designer.
* **Enterprise Grounding:** Understand how Agent Search indexes and grounds responses in structured and unstructured internal repositories, including multimodal inputs (documents, audio, video).

### 2. Coding Agents & Development Platforms: Google Antigravity (~17%)

* **ADK vs. Antigravity:** ADK is the programmatic code framework used to build and wire agent logic in your application. **Google Antigravity** is Google’s agentic development platform where autonomous agents plan, write, execute, and verify software.
* **Rules vs. Skills:** In Antigravity, know how to guide agent behavior. **Rules** are project constraints and invariants (often defined in `AGENTS.md` or `.agents/rules/` to enforce coding styles and architectural boundaries), while **Skills** are reusable, multi-step procedural task workflows.

> **Antigravity Rule Pattern (`AGENTS.md`):**
> ```markdown
> # Project Invariants
> - Execution Boundary: Shell commands and dynamic tests must run exclusively in containerized sandboxes.
> - Tool Calling: Never invoke external mutation APIs without explicit human confirmation.
> - Schema Contract: All MCP tool parameter payloads must be strictly validated before dispatch.
> ```

* **Scoping:** Understand how configurations apply across different boundaries—locally within a specific directory, across an entire workspace, or globally across a development environment.
* **Sandboxing & Model Context Protocol (MCP):** Know when coding agents must execute inside secure sandboxes (such as Cloud Workstations or GKE Agent Sandboxes) to isolate untrusted shell scripts. Understand how MCP standardizes the way agents interface with external file systems, databases, and developer tools.

### 3. Custom Agent Architecture & ADK (~33%)
Section 3 represents a third of the entire syllabus. You need to know how to structure and code multi-agent systems using the **Agent Development Kit (ADK)**.

* **Multi-agent topologies:** Understand the architectural differences between a centralized orchestrator (supervisor delegating tasks to specialized sub-agents) and decentralized handoffs using Agent-to-Agent (A2A) protocols across different domain teams.
* **State management and keys:** Know how state flows through an agent runtime. Review how **output keys** and **state prefixes** are configured so that parallel sub-agents don’t accidentally overwrite shared context or stomp on conversational history.
* **Session state vs. long-term memory:** Be clear on the operational boundary between short-term conversational turns (sessions) and durable user context. Understand how **Memory Bank** extracts and persists semantic facts across distinct user interactions.
* **Agent workload identity:** Review how cryptographic identities are assigned to autonomous runtimes. Understand where **SPIFFE-based identities** and Principal Access Boundaries (PAB) fit when an agent needs to prove its identity to access backend cloud infrastructure.

### 4. Security, Gateways, and Governance (~20%)
Security is the most critical design constraint when moving agents from internal prototypes to production systems.

* **Agent Gateway topology:** Understand where Agent Gateway sits in your network architecture. Know how to configure ingress (protecting your agent from untrusted client calls) and egress (restricting which external APIs, databases, or MCP tools the agent can invoke).
* **Model Armor & Content Safety:** Study how Model Armor hooks into the gateway pipeline. Understand how to configure templates to catch prompt injection, detect jailbreak attempts, and block unsafe content before user inputs reach the model.
* **Sensitive Data Protection (SDP):** Know how SDP combines with Model Armor to dynamically mask, tokenize, or redact PII before it gets logged in telemetry or forwarded to downstream tools.
* **Delegated authorization (User OAuth vs. Service Account):** Pay close attention to credential delegation. When an agent calls an external API, it should rarely use a broad, ambient service account identity. Instead, it should execute the tool using the **end user's delegated OAuth token**, ensuring the agent cannot execute actions the calling user does not have permission to perform.

### 5. Evaluations, Observability, and Token Optimization (~17%)
Traditional software assertions break down when dealing with non-deterministic LLMs. You need to know how to measure agent behavior systematically.

* **Tool trajectory evaluation:** Evaluating the final text response of an agent is insufficient. You must evaluate the **trajectory**—verifying that the agent invoked the correct sequence of tools, passed valid argument schemas, and reached the resolution without entering looping cycles.
* **Handling live data drift in evals:** A frequent challenge with agent evaluation suites is that testing against live APIs causes tests to fail due to changing production data rather than logic bugs. Understand how to design resilient evaluation pipelines using mock data layers, synthetic fixtures, or LLM-as-a-judge patterns to evaluate decision-making independently of live API churn.
* **Context caching:** Long system prompts, complex tool schemas, and multi-turn histories balloon latency and costs. Review how **context caching** dramatically reduces inference costs and time-to-first-token by caching shared, immutable prompt prefixes.
* **OpenTelemetry (OTel):** Know how to instrument agent runtimes with distributed tracing to track end-to-end latency across reasoning loops, vector retrieval, and external tool calls.

### 6. Edge and Hybrid Models (Gemma)
While Gemini handles large-scale cloud reasoning, understand when to deploy lightweight open models like **Gemma** at the edge or on local hardware. Focus on how to secure local runtimes, protect model weights, and enforce local tool-execution boundaries.

---

## Final Thoughts

I actually really liked the format of this exam. Pairing a comprehensive theory test with time-constrained, hands-on challenge labs makes total sense for this domain. It shifts the credential away from high-level slide architecture and anchors it squarely in the gritty details of implementing and productionising agentic solutions on Google Cloud from a true engineering perspective.

While having a solid grasp of the theory is obviously important, the sheer breadth of topics covered means you simply cannot fluke your way through on whitepapers alone. You need real, hands-on experience across the entire stack. That means writing custom agents and multi-agent topologies in ADK, getting comfortable with enterprise security controls like Agent Gateway and delegated auth, and understanding the practical realities of moving an agent into production. 

Above all, don't overlook evaluations. Knowing how to systematically measure tool trajectories, catch hallucinations or looping behaviours, and implement resilient evaluation patterns is critical before you let an autonomous system anywhere near an enterprise environment.

If you sat the beta as well, or you’re gearing up to take the exam once it lands in General Availability, let me know your thoughts or drop any questions in the comments below!

---

Thanks for reading! Please feel free to share, [subscribe](https://www.cloudbabble.co.uk/subscribe) for updates, or follow me on [LinkedIn](https://linkedin.com/in/jamiethompson85).

**Other Guides:**
If you are planning your Google Cloud certification journey or deciding which track to pursue next, check out my other exam breakdowns:

- [Google Cloud Professional Cloud Developer Exam Guide (2026 Renewal)](https://www.cloudbabble.co.uk)
- [Google Cloud Professional Database Engineer Exam Guide](https://www.cloudbabble.co.uk)
- [Google Cloud Generative AI Leader Certification (GAIL)](https://www.cloudbabble.co.uk/2025-05-14-GoogleCloudGenerativeAILeaderCertification/)
- [Google Cloud Professional Cloud Architect (PCA) Renewal Certification](https://www.cloudbabble.co.uk/2025-11-18-Google-Cloud-Professional-Cloud-Architect-Exam-Guide-Renewal/)
- [Google Cloud Professional Cloud DevOps Engineer](https://www.cloudbabble.co.uk/2025-12-05-GoogleCloudDevOpsEngineerExamGuide/)
- [Google Cloud Professional Network Engineer Certification (PNE)](https://www.cloudbabble.co.uk/2024-02-01-GoogleCloudProfessionalCloudNetworkEngineerCertification/)
- [Google Cloud Associate Data Practitioner Certification (ADP)](https://www.cloudbabble.co.uk/2025-01-22-associate-data-practitioner/)
- [Google Cloud Digital Leader Certification (CDL)](https://www.cloudbabble.co.uk/2022-12-06-GoogleCloudDigitalLeaderCertification/)


