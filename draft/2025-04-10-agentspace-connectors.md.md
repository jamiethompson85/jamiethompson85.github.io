---
layout: post
title: "Agentspace Connectors and Actions: Secure Integration Explained"
subtitle: "Understanding how Agentspace integrates with enterprise systems and respects data permissions"
#description: ""
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/agentspace/agentspaceacl.png
share-img: /assets/img/agentspace/agentspaceacl.png
readtime: true
share-title: "Agentspace Connectors and Actions: Secure Integration Explained"
#share-description: "TXXXXX"
share-img: /assets/img/agentspace/agentspaceacl.png
tags: [Google Cloud Agentspace, Agentspace Connectors, Agentspace Data Sources, Agentspace Actions, Google Cloud, AI Assistant, Enterprise Search, Generative AI, Agentspace]
---

In my [last blog post](https://www.cloudbabble.co.uk/2025-04-08-AgentspaceUI/ "Click to read previous Agentspace blog post"), I explored the potential of Google Cloud Agentspace through its user interface and enterprise search and summarisation features. Now I'll cover the practical mechanics of integrating Agentspace within an enterprise landscape, focusing on two critical pillars: Connectors and Actions. 

This post explains how Agentspace securely ingests data from diverse data sources using its extensive connector library, paying close attention to Access Control List (ACL) management, and how it enables powerful interactions back into those systems via predefined Actions. 

Read on for a deeper look at configuration, security considerations, and practical examples of connecting and acting on your enterprise data.

# Agentspace Data Source Connectors
A key differentiator and strength of Agentspace is its vast array of connectors for both first party (Google Cloud and Workspace products) and third-party enterprise applications (think Workday, ServiceNow, Jira, MS Outlook, Teams, SharePoint, GitHub, Confluence….). At the time of writing there was over 100 connectors (including many in development).

![Example Agentspace Data Source Connectors for Google Cloud, Workspace and Enterprise Applications](/assets/img/agentspace/agentspaceconnectors.png "Example Agentspace Data Source Connectors for Google Cloud, Workspace and Enterprise Applications") 

*Figure 1: Example Agentspace Data Source Connectors for Google Cloud, Workspace and Enterprise Applications*

From an implementation perspective, the connectors save an incredible amount of time, with zero code required for the basic connection and data ingestion process. For instance, the Google Drive connector simply requires the user to define the shared drive or folder, and create a data store name and Agentspace takes care of the rest.

![Example Agentspace Google Drive Connector Configuration Data Selection](/assets/img/agentspace/agentspaceconnectordrive1.png "Example Agentspace Google Drive Connector Configuration Data Selection") ![Example Agentspace Google Drive Connector Configuration Naming](/assets/img/agentspace/agentspaceconnectordrive2.png "Example Agentspace Google Drive Connector Configuration Naming")

*Figure 2: Example Agentspace Google Drive Data Source Configuration Screenshots*

Whilst first party Google Cloud and Google Workspace connectors are essentially point and click via the Agentspace UI, the third-party connectors require some configuration application side- typically the creation of a token (and securely storing/accessing the token from Google Secrets Manager) and access to the source data. 

That being said, with the support of documentation (for the 3rd party connectors), the configuration wasn’t challenging, and I was able to quickly connect to many data sources including:

- BigQuery
- CloudSQL
- AlloyDB
- Cloud Storage
- Google Drive
- Google Mail
- Google Calendar
- Jira Cloud
- Confluence Cloud
- GitHub
- ServiceNow
- Slack

After the connector is configured, Agentspace starts to ingest the data from the source. This ingested data is then stored as an embedding within a Vertex datastore and indexed for searching.

One of the greatest challenges with AI search applications to date is maintaining data access. Once you have embeddings, you still need to ensure data is only accessible to authorised users. This typically results in two options:

1.  Simply limiting data ingestion to universally accessible or public information starves the application of potentially valuable data, thereby reducing its effectiveness, insight generation, and grounding ability.
2.	The other option involves custom-building data access control logic directly into the AI application itself. This often means trying to synchronise or map user permissions and the source data's ACLs onto the indexed embeddings – a process that adds enormous technical complexity and maintenance burden to the solution.

This complexity escalates significantly when dealing with multiple data sources, each potentially having its own users, permissions structures, and associated agents needing access.

Agentspace connectors address this challenge by respecting the source applications access control lists (ACL). The indexed data retains the ACL’s as defined in the source system, so Agentspace users will only be returned data to which they have access in the source system. This enables Agentspace to ingest a wider scope of data, maximizing the insights available to the assistant whilst at the same time ensuring only authorised users can surface data to which they could access on the source system. This unified approach allows Agentspace to combine insights from as many configured sources as you choose within a single application, all while respecting individual permissions.

Many of the connectors also allow tailoring of the data ingested to meet your requirements by filtering the content during ingestion e.g. Jira connectors can be limited to ingest specific projects and a subset of entities only e.g. issues and comments, excluding attachments and worklogs. 

![Agentspace ACL Replication](/assets/img/agentspace/agentspaceacl.png "Agentspace ACL Replication") 

Figure 3 *Agentspace Maintaining Embedding ACL with Connector*

Connectors typically have a variety of options for synchronisation, allowing one time synchronisation, or periodic synchronisation. There is also the option to manually synchronise data sources on an ad hoc basis.
Connectors regularly synchronising data also include a health state within the console. This quickly alerts Agentspace administrators to any issues during the previous synchronisation.

In the event you are unable to find a connector for an application/data source, custom connectors can also be developed to ingest data via API. However, it is worth noting that Google is continuing development of connectors so in the first instance, I would recommend discussing your requirements with Google or your Google partner to determine if an existing connector is in development. Whilst they may not be generally available, the time and effort saved developing and securing your own custom connector could be spent testing and influencing the features of Google’s development.

# Actions
While data source connectors primarily handle connectivity and data ingestion into Agentspace out-of-the-box, Actions provide the crucial capability to interact with the source systems.

During private preview, the predefined actions ranged from sending emails based on curated content, creating meetings in your calendar, to raising requests for time off in Workday, or creating and updating Jira tickets. 
Like connectors, the library of predefined Actions is under development, so if you are looking for a particular action, reach out to Google or your Google partner to check what is on the roadmap (some may be available for private preview).

![Example Agentspace Actions Configuration- Jira Actions](/assets/img/agentspace/agentspacejiraaction.png "Example Agentspace Actions Configuration- Jira Actions") 

*Figure 4: Example Agentspace Jira Action Configuration Screenshot*

Users typically invoke actions via conversational chat with Agentspace. As shown in the following diagram, a user enters a prompt invoking the action e.g. "I want to create a Jira story, with the title 'Implement Jira actions in Agentspace'. This is part of the project ABC. The description should be 'Configure Agentspace Action to enable Jira stories to be created and updated via the Agentspace UI.' Assign the story to Jamie@cloudbabble.co.uk. The component should be Agentspace. Give it a Medium priority."

Agentspace then extracts the relevant information from the prompt, adding it to the corresponding fields for the Jira card template. The user can then review the draft, amend as desired directly or via subsequent prompts and then hit send to create the Jira story. A link to the created Jira is then returned to the user. Crucially, actions operate under the permissions of the logged in user for the target application, ensuring users can only initiate actions they are authorised to perform in the source system (in this scenario, Jira).

![Example Agentspace Jira Action Invocation using Natural Language](/assets/img/agentspace/agentspaceactioninvocation.png "Example Agentspace Jira Action Invocation using Natural Language") 

*Figure 5: Example Jira Action Story Creation Invocation via Agentspace Chat with Natural Language*

These interactive actions also form an optional building block for more complex automation within Agentspace Agents. Look out for the next post in this Agentspace series, where I will explore Agentspace Agents in more detail.

Thanks for taking the time to read this blog, I hope you find it useful understanding Google Cloud Agentspace. Please feel free to share, [subscribe](https://www.cloudbabble.co.uk/subscribe) to be alerted to future posts, follow me on [LinkedIn](https://linkedin.com/in/jamiethompson85), and react/comment below! 
