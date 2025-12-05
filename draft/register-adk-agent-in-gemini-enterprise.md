---
layout: post 
title: "How to Register and Use ADK Agents with Gemini Enterprise (2025 Guide)" 
excerpt: "Built a custom agent with the Google Agent Development Kit? Here is a step-by-step breakdown of how to register it with Gemini Enterprise, handle the tricky OAuth 2.0 authorization flow, and enable secure user context in your python code." 
subtitle: "A technical guide to connecting backend ADK logic to the Gemini Enterprise frontend." 
description: "Planning to deploy your custom AI agents to your enterprise users? Here is a detailed guide on registering ADK agents with Gemini Enterprise, covering OAuth configuration, resource registration, and user context handling." 
thumbnail-img: /assets/img/Gemini Enterprise/adk-registration-guide.png 
share-img: /assets/img/Gemini Enterprise/adk-registration-guide.png 
readtime: true 
share-title: "Guide: Registering ADK Agents with Gemini Enterprise" 
share-description: "I successfully connected my custom ADK agent to Gemini Enterprise. Here are my notes, curl commands, and tips for handling OAuth tokens securely." 
tags: [Google Cloud, Gemini Enterprise, ADK, AI Agents, Python, OAuth, Vertex AI]
---
# How to Register and Use ADK Agents (on Agent Engine) with Gemini Enterprise
So, you’ve built a custom agent using Google's Agent Development Kit (ADK). It’s deployed on Vertex AI's Agent Engine platform, and it’s ready to work. But right now, it’s just code sitting in the cloud. How do you get it into the hands of your users?

The answer is Gemini Enterprise (formerly known as Agentspace).

Connecting your backend logic to the frontend Gemini Enterprise UI requires precise configuration, involving various resource IDs, security checks, and authentication flows. But don't worry. This guide will walk you through registering your ADK agent, handling the "OAuth dance," and getting your agent ready for prime time.

📝 **A Note on Documentation:** If you have struggled to find clear instructions on this process, you are not alone. The official documentation has lagged slightly behind the actual product releases- no doubt due to the  pace at which these products are being developed at Google! This guide aims to bridge that gap and get you up and running today based on my experiences working with Gemini Enterprise, ADK and Agent Engine.

# The Deployment Dilemma: Custom UI vs. Managed Platform
Before we dive into the configuration, it is worth addressing a common question: “Why don’t I just build my own UI?”

Technically, you can. The "Do It Yourself" approach involves wrapping your agent in a custom web app (like Streamlit or React), deploying it to Cloud Run, and securing it with Identity-Aware Proxy (IAP). While this offers pixel-perfect control, it comes with a heavy operational tax:

- **Developer Overhead:** You move from building agents to maintaining software products. You are now responsible for session management, frontend bug fixes, and security patching.
- **Scalability & Sprawl:** If you have 20 agents, you end up with 20 different Cloud Run services and 20 different URLs for users to bookmark. This fragmentation kills adoption.
- **Governance Blind Spots:** Custom UIs are harder to audit. It becomes difficult to maintain a centralized view of "who is using what" across the organization.

# The Gemini Enterprise Advantage 
Gemini Enterprise is designed to solve these scalability issues. It acts as a centralized "App Store" for your organization's agents. It handles the UI, authentication, and governance automatically, allowing you to focus strictly on the agent's logic. 

## Why it solves the scale problem:

**One Interface for All Agents:** Users go to one URL. They see a catalog of all agents available to them (HR, IT, Sales) based on their IAM permissions.
**Zero UI Code:** You deploy the logic (the ADK backend), and Gemini Enterprise renders the UI automatically. You never have to write a React component or fix a CSS bug again.
**Unified Context:** Because the agents live in the same "space" as Google Workspace, they have native access to Drive/Docs/Gmail context without you writing complex OAuth handshakes for every single agent.Centralized **Governance:** Admins can turn off specific agents, audit logs, and enforce data residency policies globally, rather than chasing down individual Cloud Run deployments.

## Summary Recommendation

| Feature | Custom UI (Cloud Run + IAP) | Gemini Enterprise |
| :--- | :--- | :--- |
| **Setup Effort** | High (DevOps, Frontend, Auth) | Low (Register & Go) |
| **Maintenance** | High (Patching UI, fixing bugs) | Zero (Managed by Google) |
| **Discoverability** | Low (Emailing links) | High (Central Catalog) |
| **Use Case** | **Niche:** Highly specialized visual needs (e.g., an agent that renders interactive 3D CAD models). | **Standard:** 95% of internal business agents (Chat, Text, Charts, File Analysis). |

# What is the goal?
The goal is to take a "headless" agent deployed on Vertex AI Agent Engine and register it so that:

1. Users can discover and chat with it in the centralized Gemini Enterprise Web App.
2. The agent can securely act on behalf of the user (e.g., sending emails or querying private data).

# Prerequisites
Before we start sending curl commands, let's make sure your environment is ready.

- **Admin Access:** You need the agents.manage permission (usually part of the Discovery Engine Admin role) to register agents.
- **Service Account Roles:** Ensure your discoveryengine service account has Vertex AI User and Vertex AI Viewer roles. This is required for Gemini Enterprise to actually call your agent.
- **Deployed Agent:** We assume you have already deployed your agent using the ADK and have your ADK_DEPLOYMENT_ID handy.

# Step 1: The OAuth Setup (Optional but Critical)
Does your agent need to do things on behalf of the user, like checking their Calendar or querying a private BigQuery table? If yes, you need OAuth. If your agent is just a calculator or a public info bot, you can skip to Step 2.

## i. Configure your Provider
First, register your app with your OAuth 2.0 provider (like Google Cloud) to get a Client ID and Client Secret .

🚨 Critical Step: You must add the following URL to your "Allowed Redirect URIs" list in your OAuth application. Gemini Enterprise handles the callback automatically, but only if you whitelist this address:

https://vertexaisearch.cloud.google.com/oauth-redirect

## ii. Visualize the Flow
It helps to understand what we are building. We are setting up a flow where Gemini Enterprise acts as the middleman between the user and your agent.

# insert image to visualise
   
## iii. Create the Authorization Resource
Now, tell Gemini Enterprise about your OAuth credentials. This creates a resource ID that we will link to the agent later.

Run this command (replacing the capitalised placeholders with your project details):

```Bash
curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-H "X-Goog-User-Project: PROJECT_ID" \
"https://discoveryengine.googleapis.com/v1alpha/projects/PROJECT_ID/locations/global/authorizations?authorizationId=AUTH_ID" \
-d '{
  "name": "projects/PROJECT_ID/locations/global/authorizations/AUTH_ID",
  "serverSide0auth2": {
    "clientId": "OAUTH_CLIENT_ID",
    "clientSecret": "OAUTH_CLIENT_SECRET",
    "authorizationUri": "OAUTH_AUTH_URI",
    "tokenUri": "OAUTH_TOKEN_URI"
  }
}'
```

- **AUTH_ID:** This is an arbitrary ID you define to reference this setup later.
- **Google defaults:** If using Google, the Auth URI is usually https://accounts.google.com/o/oauth2/v2/auth and the Token URI is https://oauth2.googleapis.com/token.

# Step 2: Registering the Agent
This is the main event. We are going to link your ADK deployment to the Gemini Enterprise interface.

You will need to construct a curl request that defines how the agent looks to users and how the LLM should understand it .

## The Key Fields to Know
- **displayName:** The name users see in the UI (e.g., "Invoice Helper").
- **description:** What the user sees in the UI to understand the agent's purpose (e.g., "Extract key information from uploaded invoices").
- **tool_description:** This is for the AI. It is the prompt used by the LLM to route requests to the agent (e.g., "You are an expert invoice data extractor...").
- **provisioned_reasoning_engine:** This points to your actual code running on Vertex AI .

## The Command

```Bash

curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-H "X-Goog-User-Project: PROJECT_ID" \
"https://discoveryengine.googleapis.com/v1alpha/projects/PROJECT_ID/locations/global/collections/default_collection/engines/APP_ID/assistants/default_assistant/agents" \
-d '{
  "displayName": "My Super Agent",
  "description": "Helps you analyze data.",
  "adk_agent_definition": {
    "tool_description": "Use this tool for data analysis tasks...",
    "provisioned_reasoning_engine": {
      "reasoning_engine": "projects/PROJECT_ID/locations/REASONING_LOCATION/reasoningEngines/ADK_DEPLOYMENT_ID"
    },
    "authorizations": [
      "projects/PROJECT_ID/locations/global/authorizations/AUTH_ID"
    ]
  }
}'
```
**Note:** The authorizations block is only needed if you completed Step 1.

# Step 3: Test Drive in Gemini Enterprise
Once the API returns a success message (and a resource name), your agent is live!

**i. Navigate:** Go to the Gemini Enterprise page in the Google Cloud Console.
**ii. Select App:** Choose the Gemini Enterprise app where you added the agent.
**iii. Enable Web App:** In the main menu, select Integration and ensure "Enable the Web App" is toggled on.
**iv. Launch:** Click the web app link provided.
**vi. Find Your Agent:** You will see your new agent listed under the "Agents" section in the navigation menu.

# The User Experience
If you set up OAuth, the first time a user interacts with your agent, Gemini Enterprise will prompt them for authorization. They will see an "Authorize" button, followed by the standard OAuth consent screen. Once granted, your agent can act on their behalf! .

# <insert image of oauth>

##💡 Pro Tips for Developers
**1. Make it Chatty (Status Updates)**
ADK agents can send real-time feedback to the UI. Instead of the user staring at a blank screen while your agent crunches numbers, you can display messages like "Executing code review..." .

In your Python code, you simply update the state dictionary:

```python
callback_context.state["ui:status_update"] = "Starting code generation."
```

**2. Using the User's Identity**
If you used OAuth, your Python agent can access the user's token via tool_context.state. This allows you to make API calls (like searching the user's Google Drive) securely, impersonating the user who is chatting with the bot .

```Python

# Access token is stored in the temp namespace
access_token = tool_context.state[f"temp:{AUTH_ID}"]
```

**3. Updating Your Agent**
If you need to change the description or the underlying reasoning engine, use the PATCH command.

Warning: You must provide displayName, description, tool_settings, and reasoning_engine in the update request, even if they haven't changed.

# Conclusion
The ability to register custom ADK agents turns Gemini Enterprise from a simple chat interface into a powerful enterprise platform. By bridging your custom Python logic with Google's managed UI, you can build tools that are both powerful and user-friendly.

Good luck with your build!

Thanks for reading this guide. If you found it helpful for your Gemini Enterprise deployment, feel free to share and react below!
