---
layout: post
title: "Google Cloud Professional Agentic Architect Exam Guide: Passing the Exam & Challenge Labs"
excerpt: "My journey becoming officially certified as a Google Cloud Professional Agentic Architect. A complete breakdown of Google's first hybrid exam: passing the 3-hour theory proctored exam and clearing the hands-on challenge labs."
subtitle: "From Theoretical Architecture to Hands-On Lab Implementation"
description: "A comprehensive, architect-level guide for the Google Cloud Professional Agentic Architect certification. Details the full journey across the 3-hour theory exam (beta), passing the hands-on challenge labs on skills.google, and key architectural domains across ADK, Antigravity, and Gemini Enterprise."
thumbnail-img: /assets/img/paa/professional-agentic-architect-certification.png
share-img: /assets/img/paa/professional-agentic-architect-certification.png
readtime: true
share-title: "How to Pass the Google Cloud Professional Agentic Architect Certification (Exam Theory & Hands-on Challenge Labs Guide)"
share-description: "Field notes and hands-on guide for Google Cloud's new Professional Agentic Architect hybrid certification. Practical insights on passing the theory exam, and completing the hands-on challenge labs on skills.google."
tags: [Google Cloud, PAA, Agentic AI, ADK, Antigravity, Gemini Enterprise, Agent Studio, Agent Gateway, Model Armor, Challenge Labs, Certification, Exam Guide]
---

# Google Cloud Professional Agentic Architect Exam Guide

In September, I sat the beta exam for Google Cloud’s latest credential: the **Professional Agentic Architect**.

Google has taken a fundamentally new direction with this track. Rather than relying solely on traditional multiple-choice questions, this is Google Cloud’s first hybrid certification. Earning the badge requires clearing two distinct stages: a proctored theoretical exam (Part 1), followed by a hands-on lab assessment delivered through Google Skills (Part 2).

Between building applications with Google’s Agent Development Kit (ADK), working across the Gemini Enterprise ecosystem in my day job, and using Antigravity regularly, I was keen to see how my hands-on experience stacked up against Google's expectations.

After completing the proctored exam and subsequently clearing the challenge labs, I am now **officially certified as a Google Cloud Professional Agentic Architect**, taking me to **14 active Google Cloud certifications** in total.

Here is the breakdown of the OnVUE testing setup, what the Part 1 question dynamic felt like, the core architectural domains you need to master, and what to expect when you transition into the live challenge labs for Part 2.

---

## The Remote Proctoring Setup: OnVUE vs. Kryterion Webassessor

With no local test centres nearby, remote proctoring has been my default for years. If you’ve taken Google Cloud certifications previously, you’ll be well accustomed to Kryterion’s Webassessor portal and Sentinel software. Sitting Part 1 of this exam was my first experience with Pearson VUE’s OnVUE platform following Google’s delivery migration, and the operational differences were noticeable from the start:

- **Mobile-first check-in flow:** OnVUE offloads identity and environment verification directly to your phone. Once you launch the session on your laptop, you scan a QR code to capture high-res photos of your ID, snap a verification selfie, and submit four clear angle shots of your workspace (front, back, left, right) before placing the phone out of arm's reach.
- **The queue and proctor sweep:** I logged in 15 minutes ahead of my scheduled window to run automated system, mic, and webcam checks. Once my phone photos were submitted, I entered a queue at position 13, taking just under 15 minutes for a proctor to connect. While Webassessor leaned heavily on background biometric profiles, OnVUE proctors are much more hands-on, requiring me to lift my laptop for an active 360-degree sweep of the entire room, including the space underneath the desk and behind the laptop screen, before unlocking the test.
- **The clean-desk reality:** While the delivery platform has changed, the remote testing discipline hasn't. You still need an entirely cleared workspace: second monitors unplugged and turned away, paper and clutter completely cleared, and your desk kept entirely bare throughout the session.
- **Rescheduling flexibility:** Client deliverables ramped up right before my initial test date, forcing me to push my slot back. OnVUE’s rescheduling was remarkably painless compared to Webassessor- there was wide availability across alternative time slots, and the system let me adjust the booking right up to the start time without friction.

---

## Exam Structure & The Beta Dynamic

Because this was a beta, the format differed slightly from what the final General Availability (GA) exam will look like:

| Component | Beta Version | General Availability (GA) |
| :--- | :--- | :--- |
| **Exam Duration** | 3 hours (180 minutes) | 2 hours (120 minutes) |
| **Question Count** | 75 questions | 50–60 questions |
| **Challenge Labs** | 3 options presented (must pass 2) | 3 options presented (must pass 2) |
| **Registration Fee** | $120 USD (40% beta discount) | $200 USD (standard retail) |
| **Credential Validity** | 1 year | 1 year |

*\*Note: Unlike standard Google Cloud certifications that grant you two years of peace, this badge is only valid for **1 year**. Given the rapid evolution of agentic protocols, security tooling, and the fact that we get a new Gemini model drop almost weekly lately, an annual renewal makes sense.\**

### Part 1: Question Pool Dynamic

With an uncalibrated beta question pool, the questions largely fell into two styles:

1. **System design problems:** Questions that test genuine design trade-offs across multi-agent handoffs, token management, and evaluation pipelines. The key is methodically stepping through the data path between the caller, gateway, agent runtime, and backend tools.
2. **Obvious eliminations:** Questions where several distractors flagrantly violate basic Google Cloud security principles. You can cross them off immediately if an option suggests controlling hard security via system prompts, assigning excessive service account roles, or bypassing code sandboxing.

Pacing felt comfortable. With 75 questions across 180 minutes, you have roughly 2.4 minutes per question. I wrapped up the exam with about 40 minutes remaining, even after reviewing flagged questions. For GA, Professional Certification exams are usually ~50 questions across 120 minutes.

---

## Official Exam Guide Domains & Weightings

The technical requirements for both parts map directly across five documented domains from the [Professional Agentic Architect Exam Guide](https://services.google.com/fh/files/misc/professional_agentic_architect_exam_guide_english.pdf):

| Section | Focus Area | Exam Weighting |
| :--- | :--- | :--- |
| **Section 1** | Building agents using low-code tools | ~13% |
| **Section 2** | Using coding agents for application development | ~17% |
| **Section 3** | Developing custom agents | ~33% |
| **Section 4** | Evaluating and deploying agentic workflows | ~22% |
| **Section 5** | Securing and governing agentic workflows | ~15% |

---

## Core Technical Themes to Master

Whether you are answering architectural questions in the exam, or implementing resources in hands-on labs, the following technical themes form the backbone of the credential:

### 1. The Gemini Enterprise Ecosystem & Low-Code Agents (~13%)

To clear this domain, you should be comfortable with:

- **End-to-End Architectural Integration:** Understand how user-facing interfaces (such as the Gemini Enterprise app or custom web front-ends) link down into the agent runtime. Know how conversational agents, tool extensions, and grounded search collaborate, and where the architectural boundary sits between low-code configuration and custom code implementations.
- **Conversational Flow & CX State Management:** Review how state-based multi-turn dialogues are structured in Agent Designer / CX Agent Studio consoles. Be clear on how pages, transition routes, conditional event handlers, and fallback flows operate to guide user intent and handle unexpected inputs.
- **Enterprise Grounding & Data Stores:** Know how to configure managed data stores across structured, unstructured, and multimodal repositories (text documents, audio, and video). Understand how chunking strategies, semantic search, and metadata filtering prevent hallucinations and keep responses strictly grounded.
- **Tool Extensions & API Contracts:** Understand how low-code agents invoke external business logic. Review how OpenAPI schemas define tool contracts, how authentication is passed to downstream APIs, and how Agent Gateway enforces ingress and egress policies around tool invocation.

### 2. Using Coding Agents for Application Development (~17%)

This domain shifts the focus from building user-facing conversational apps to developer tooling and engineering autonomy, specifically using Google Antigravity and Claude Code on Google Cloud to refactor code, optimise execution runtimes, and patch application-layer vulnerabilities.

To clear this section, make sure you understand:

- **Antigravity Customisation (Rules vs. Skills):** Know how to govern agent behaviour across workspace, directory, and global scopes. Rules enforce non-negotiable architectural boundaries and coding constraints (e.g., via `AGENTS.md` or `.agents/rules/`), whereas Skills, plugins, extension hooks, and subagents provide reusable, procedural task workflows.
- **Model Context Protocol (MCP) & Tool Access:** Understand how coding agents connect to external environments, file systems, databases, and enterprise services through standard MCP client/server integrations.
- **Execution Sandboxing & Isolation:** Recognise the security risks of autonomous dynamic execution. Be clear on when and how coding agents must be confined to isolated execution environments, such as GKE Agent Sandboxes, Cloud Workstations, or Antigravity's hosted sandboxes, to run untrusted shell scripts and dynamic tests safely.
- **Enterprise Tooling with Agents CLI:** Understand how to augment Antigravity using the Agents CLI to script, scale, govern, and optimise coding agents consistently across a team.

### 3. Custom Agent Architecture & ADK (~33%)

Section 3 represents a third of the entire syllabus. You need to know how to structure and code multi-agent systems using the Agent Development Kit (ADK).

- **Multi-Agent Topologies:** Understand the architectural differences between a centralised orchestrator (supervisor delegating tasks to specialised sub-agents) and decentralised handoffs using Agent-to-Agent (A2A) protocols across different domain teams.
- **State Management and Keys:** Know how state flows through an agent runtime. Review how output keys and state prefixes are configured so that parallel sub-agents don’t accidentally overwrite shared context or stomp on conversational history.
- **Session State vs. Long-Term Memory:** Be clear on the operational boundary between short-term conversational turns (sessions) and durable user context. Understand how Memory Bank extracts and persists semantic facts across distinct user interactions.
- **Agent Workload Identity:** Review how cryptographic identities are assigned to autonomous runtimes. Understand where SPIFFE-based identities and Principal Access Boundaries (PAB) fit when an agent needs to prove its identity to access backend cloud infrastructure.

### 4. Evaluating and Deploying Agentic Workflows (~22%)

Deterministic unit tests won't cut it when you're evaluating probabilistic model outputs, you need systematic evaluation frameworks

- **Tool Trajectory Evaluation:** Evaluating the final text response of an agent is insufficient. You must evaluate the trajectory, verifying that the agent invoked the correct sequence of tools, passed valid argument schemas, and reached the resolution without entering looping cycles.
- **Handling Live Data Drift in Evals:** A frequent challenge with agent evaluation suites is that testing against live APIs causes tests to fail due to changing production data rather than logic bugs. Understand how to design resilient evaluation pipelines using mock data layers, synthetic fixtures, or LLM-as-a-judge patterns to evaluate decision-making independently of live API churn.
- **Context Caching:** With long system prompts and extensive tool schemas, context caching is essential to keep latency and billable token counts under control. Focus on how immutable prompt prefixes are cached.
- **OpenTelemetry (OTel):** Know how to instrument agent runtimes with distributed tracing to track end-to-end latency across reasoning loops, vector retrieval, and external tool calls.

### 5. Securing and Governing Agentic Workflows (~15%)

Security is the most critical design constraint when moving agents from internal prototypes to production systems.

- **Agent Gateway Topology:** Treat Agent Gateway as your security perimeter. Be ready to configure both ingress (shielding the runtime from untrusted callers) and egress (strictly scoping the external APIs, databases, or MCP tools the agent can reach).
- **Model Armor & Content Safety:** Study how Model Armor hooks into the gateway pipeline. Understand how to configure templates to catch prompt injection, detect jailbreak attempts, and block unsafe content before user inputs reach the model.
- **Sensitive Data Protection (SDP):** Know how SDP combines with Model Armor to dynamically mask, tokenise, or redact PII before it gets logged in telemetry or forwarded to downstream tools.
- **Delegated Authorisation (User OAuth vs. Service Account):** Pay close attention to credential delegation. When an agent calls an external API, it should rarely use a broad, ambient service account identity. Instead, it should execute the tool using the end user's delegated OAuth token, ensuring the agent cannot execute actions the calling user does not have permission to perform.

---

## Recommended Preparation & Study Resources

Because this certification is brand new, the most effective preparation will come from working directly with Google's official materials and getting hands-on in the console and code:

- **The Official Exam Guide:** Start by reviewing the [Professional Agentic Architect Exam Guide](https://services.google.com/fh/files/misc/professional_agentic_architect_exam_guide_english.pdf). Use the five domains as a personal gap analysis to identify which services or runtime patterns you haven't worked with hands-on.
- **Official Sample Questions:** Work through the [official sample questions](https://cloud.google.com/learn/certification/agentic-architect) published on Google Cloud's certification hub. Even though it is a small set, it gives you a clear baseline of how Google frames scenario questions, distractor patterns, and technical tradeoffs.
- **Professional Agentic Architect Learning Path:** Make your way through the [Professional Agentic Architect path on skills.google](https://www.skills.google/paths/4525). I didn't have the time to complete the entire path end-to-end before my beta booking, but I worked through a handful of the core modules beforehand. It is remarkably thorough, goes deep into real implementation patterns, and I highly recommend working through it if you want structured coverage of the full syllabus.
- **Hands-On Code Frameworks:** Spend dedicated time inside the open-source Agent Development Kit (ADK) repository. Build out custom multi-agent topologies, trace how state and memory keys flow between agents, and write local trajectory evaluation tests before sitting Part 1 or tackling the Part 2 labs.

---

## The Transition: From Part 1 to Part 2 via CertMetrics

Once you've cleared the architectural theory, you enter the operational handoff to the hands-on labs. While I expect automated email notifications will be in place once the certification rolls out to General Availability, that wasn't the case during the beta run, I never actually received an email confirming I had cleared the theoretical exam.

If you've completed Part 1 and find yourself waiting around for an email notification, don't wait on it. Head straight to the source:

1. Log directly into the [Google Cloud CertMetrics portal](https://cp.certmetrics.com/google/en/home/dashboard).
2. Check your exam history to see if your result has updated to a pass.
3. Once your passing status is recorded, you will see the option to launch Part 2 of the certification.
4. Clicking that link routes you straight into your assigned hands-on assessment track on [skills.google](https://www.skills.google).

---

## Part 2: The Hands-On Challenge Labs

Once you launch Part 2 on skills.google, you enter the practical evaluation phase.

### Lab Structure & Rules
- **3 Challenge Labs Presented -  Pass Any 2:** You are presented with a selection of three distinct challenge labs. To achieve certification, you need to successfully pass two of them.
- **100% Completion Bar:** Just like standard Google Cloud challenge labs, there is no partial credit. Passing a lab requires achieving a 100% score, progressing through all milestone assessment checks.
- **Lab Durations:** Google’s estimated completion times ranged from 45 minutes up to 1 hour 30 minutes depending on the lab complexity. However, the actual allotted lab timer is greater than this, giving you plenty of time if you need to troubleshoot or wait for services to initialise (although this wasn’t an issue for my labs).
- **Standard Challenge Lab Format:** If you have completed challenge labs on skills.google before, the process is the same: an objective brief, architecture constraints, and an automated tracking script that evaluates your environment as you complete each phase.

### Practical Tips for the Challenge Labs
- **Exact Naming Is Non-Negotiable:** Like every challenge lab on skills.google, the automated background grading scripts look for exact string matches. Whether you are provisioning services in the console or running scripts, copy and paste the resource names, IDs, and variables directly from the lab brief. A single typo will fail a milestone check even if the underlying build is functioning.
- **Respect Propagation Time:** Avoid hitting "Check My Progress" the millisecond a resource shows as created. Cloud control planes and service bindings can take a minute or two to settle across the environment. Rushing the verification check can result in a false-negative score.
- **Read the Whole Brief First:** It's tempting to jump straight into the first objective, but later tasks often impose constraints on earlier setups. Spend the first five minutes reading through all phases of the scenario so you don't build yourself into a corner that requires re-deploying resources on the clock.

---

## Final Thoughts

I really liked the format of this exam. Combining a comprehensive theory test with time-constrained, hands-on challenge labs makes total sense for this domain. Rather than testing purely conceptual designs, it focuses directly on the practical engineering required to build, secure, and productionise agentic systems on Google Cloud.

While a solid grasp of the theory is essential, the breadth of topics covered means you cannot rely on reading documentation alone. You need genuine hands-on experience across the stack. That means writing custom agents and multi-agent topologies in ADK, configuring security controls like Agent Gateway and delegated auth, and working through the operational realities of taking an agent to production.

Above all, pay close attention to evaluations. Understanding how to measure tool trajectories, detect looping behaviours, and implement reliable evaluation patterns is critical before deploying autonomous systems into enterprise environments.

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
