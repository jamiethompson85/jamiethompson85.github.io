---
layout: post
title: Preparing for Google Cloud's New Generative AI Leader Exam
subtitle: "This blog provides an overview of Google Cloud's newest foundational certification: Generative AI Leader and my experience preparing and passing the exam as part of an early adopter pilot group."
#description: ""
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/pcne/googlecloudprofessionalcloudnetworkengineerbadge.png
share-img: /assets/img/pcne/googlecloudprofessionalcloudnetworkengineerbadge.png
readtime: true
share-title: "How to prepare for Google Cloud's newest foundational certification: Generative AI Leader"
share-description: "This blog provides an overview of Google Cloud's newest foundational certification: Generative AI Leader and my experience preparing and passing the exam as part of an early adopter pilot group."
share-img: /assets/img/pcne/googlecloudprofessionalcloudnetworkengineerbadge.png
tags: [Google Cloud Foundation Generative AI Exam, Certification, Exam, Guidance]
---

In April, I joined the Google Cloud Early Adopter program to complete training and sit Google Cloud's newest exam: Google Cloud Generative AI Leader (beta). This is Google's second foundational level certification, following Google Cloud Digital Leader, but this time focussing on GenAI. In this blog I share my experience including recommended training courses, exam tips, thoughts and general guidance to help others planning to take this exam.

* toc
{:toc}

# What is the Google Cloud Foundational Generative AI Leader certification?

Google Cloud's Foundational Generative AI Leader certification is Google Cloud's second foundational level certification, alongside Google Cloud Digital Leader. As per [Google's definition:](https://rsvp.withgoogle.com/events/genaileader_beta/examguide) 

*"A Google Cloud Certified Generative AI Leader is a visionary professional with comprehensive knowledge of how generative AI (gen AI) can transform and be used within a business. This individual has business-level knowledge of Google Cloud's gen AI products and services. They recognize how Google's AI-first approach and cutting-edge products and solutions can lead their organizations toward innovative and responsible AI adoption. They can engage in meaningful conversations with both technical and non-technical teams, fostering collaboration and influencing gen AI-powered initiatives. They can identify potential use cases for gen AI across various business functions and industries, using their knowledge of Google Cloud's enterprise-ready offerings to accelerate innovation. Their expertise is in strategic leadership and influence, not technical implementation, though they have a conceptual understanding of gen AI concepts and technology.*"

![Google Cloud Professional Cloud Network Engineer Badge](/assets/img/pcne/googlecloudprofessionalcloudnetworkengineerbadge.png "Google Cloud Professional Cloud Network Engineer Badge")

*Google Cloud Foundational Generative AI Leader Badge*

# Who is the Google Cloud Foundational Generative AI Leader certificaiton aimed at?

In short, everyone within an organisation that is looking to embrace Generative AI would benefit from the associated training materials and certification. The certification is aimed at validating broad knowledge of Generative AI concepts, products, services and tools available on Google Cloud. There are no technical prerequisites for the course and as part of a corporate training program, it sets a strong foundation across the workforce, highlighting the value Generative AI can bring to an organisation and ultimately helping increase GenAI adoption.

# How difficult is the Google Cloud Foundational Generative AI Leader certification?

Google Cloud has 3 levels of certifications starting at the entry level with Foundational certifications (Cloud Digital Leader and Generative AI Leader), Associate certifications (Cloud Engineer, Workspace Administrator, and Data Practitioner) and a range of Professional level specialist certifications (Cloud Architect, Database Engineer, Data Engineer, DevOps Engineer, Developer, Security Engineer, Network Engineer, and Machine Learning Engineer). 

Given the exam is a foundational certification, it isn't as challenging as Associate and Professional certifications. However, it does cover a broad scope of Generative AI practices, so if you have very little experience working with Generative AI or Google Cloud, you may struggle. If you're working at a technical level with Generative AI and familiar with Google Cloud's products including Vertex AI, Agentspace, NotebookLM, Google AI Studio, Google's Gemini/Gemma/Imagen/Veo models etc., Google Cloud various data related products, and more broader industry terminology, you may find the exam less challenging. However, even for those fairly new to Google Cloud, there are various  materials available that canget you up to speed as covered below.

# How to prepare for and pass the Google Cloud Foundational Generative AI Leader exam

## Exam Guide
The best way to prepare for any Google Cloud exam is to review the exam guide. If you are running through all the topics covered on the exam guide, and have a good understanding of each, then you may not need to do too much study. With the exam being foundational, you don't need to understand the technical complexities of some exam topics, or how to implement them, you simply need to understand what they are, when they should be used, when they shouldn't be used, and what Google Cloud products would be most appropriate. After reviewing the exam guide, you can baseline yourself against it and tailor your trianing requirements accordingly.

The Generative AI Leader exam guide breaks down exam content into four main areas, providing a weighted percentage for each. These areas are:

- Fundamentals of generative AI (~30% of the exam)
- Google Cloud’s generative AI offerings (~35% of the exam)
- Techniques to improve AI model output (~20% of the exam)
- Business strategies for a successful gen AI solution (~15% of the exam)



Whilst I clearly got questions across all of these sections, it felt like a large portion of the exam focussed heavily on section 4: implementing hybrid interconnectivity. I had a lot of questions related to:

-	High availability VPN configuration, performance and best practice.
-	Dynamic routing, route-based routing and policy-based routing.
-	Dedicated and partner interconnect connections and VLAN attachments.
-	Cloud Router- BGP peering, route priority, MED, custom routes.

These areas are not my daily grind. My present role as a Google Cloud Architect is more typically involved in app modernisation and data migrations for large enterprise organisations, so I don’t get involved day to day in deploying and configuring network connectivity with Cloud VPN, Cloud Routers and interconnects. However, I recalled these topics being a key area in previous versions of this exam, and so I spent a lot of my preparation reading Google Cloud docs on each of these areas. Any whitepapers, blogs, best practices I could find on the topic I read! This definitely paid off as a lot of the exam focussed on them, and some questions specifically required knowledge of the performance of each solution, how and when to scale out for increased performance and what Google recommended best practices are for each.

It's also essential you understand how BGP routing works, and what alternative options exist if you have legacy infrastructure that doesn’t support BGP.

I’d also suggest focusing on VPC architecture options- understanding when to use standalone vs shared VPC, regional vs multi regional VPCs, peering, routing, and connecting to managed services like Cloud SQL.

The exam also covers Google Kubernetes Engine networking requirements, so understanding Kubernetes networking, cluster modes, subnet sizes, master authorised network access to the control plane and how these are configured are essential if you don’t have much day-to-day experience working with GKE.

From a security perspective, you need to:

- Understand how VPC service controls can help strengthen your overall security posture.
- Understand how Cloud Armour can provide protection against DDoS attacks and other threats.
- Leverage private Google access to avoid routing traffic over the internet.
- Configure Cloud DNS, knowing when to use Private zones vs Public zones and how to forward back to on premise DNS servers.
- Understand the added security benefits of DNSSEC and how it can be enabled.
- Grasp the distinct roles of traditional VPC firewall rules and hierarchical firewall policies.
- Identify what firewall rules take priority over others, and how to enable logging.

You will also need to delve into the intricacies of Google Cloud's Load Balancing options from External TCP/UDP Network Load Balancers, Internal TCP/UDP Load Balancers, External HTTP(S) Load Balancers, to Internal HTTP(S) Load Balancers and ensuring you select the optimal solution for your application's requirements. The exam also validates your understanding of configuring these load balancers including how to perform health checks, configuring firewall rules to permit the required flows and configuring backend services that effectively scale.

# Recommended training material and courses for Google Cloud Foundational Generative AI Leader certification including practice exam question sources.

https://www.cloudskillsboost.google/paths/1952

- Google Cloud Skills Boost learning path: Generative AI Leader
- Google Cloud Documentation
- Google Cloud Solutions
- Priyanka Vergadia aka The Cloud Girl

## Google Cloud Skills Boost Learning Path: Generative AI Leader

[Google Cloud Skills Boost Generative AI Leader Learning Path](https://www.cloudskillsboost.google/paths/1952) is an online self-paced training course. The content is presented in a series of five courses, over approximately 8 hours. The content for each is predominently instructor led video material, with a few quizzes thrown in along the way to test your understanding of the concepts covered.

- **Module 01 Gen AI: Beyond the Chatbot:** 1hr 30mins: This course aims to move beyond the basic understanding of chatbots to explore the true potential of generative AI for your organization. You explore concepts like foundation models and prompt engineering, which are crucial for leveraging the power of gen AI. The course also guides you through important considerations you should make when developing a successful gen AI strategy for your organization.
- **Module 02 Gen AI: Unlock Foundational Concepts:** 1hr: In this course, you unlock the foundational concepts of generative AI by exploring the differences between AI, ML, and gen AI, and understanding how various data types enable generative AI to address business challenges. You also gain insights into Google Cloud strategies to address the limitations of foundation models and the key challenges for responsible and secure AI development and deployment.
- **Module 03 Gen AI: Navigate the Landscape:** 1hr 15mins: Gen AI is changing how we work and interact with the world around us. But as a leader, how can you harness its power to drive real business outcomes? In this course, you explore the different layers of building gen AI solutions, Google Cloud’s offerings, and the factors to consider when selecting a solution.
- **Module 04 Gen AI Apps: Transform Your Work:** 1hr 45mins: This course introduces Google's gen AI applications, such as Gemini for Workspace and NotebookLM. It guides you through concepts like grounding, retrieval augmented generation, constructing effective prompts and building automated workflows.
- **Module 05 Gen AI Agents: Transform Your Organization:** 2hr 15mins: Gen AI Agents: Transform Your Organisation is the fifth and final course of the Gen AI Leader learning path. This course explores how organizations can use custom gen AI agents to help tackle specific business challenges. You gain hands-on practice building a basic gen AI agent, while exploring the components of these agents, such as models, reasoning loops, and tools.

## Google Cloud Documentation

I'm a big fan of [Google Cloud Documentation](https://cloud.google.com/docs). There are documentation pages for each Google product, providing overviews, getting started guides, code samples, and the Cloud Architecture Framework and Cloud Architecture Center for further guidance and best practices. Reading the associated product documentation pages after completing training courses helps to further embed your knowledge and clarify any points you may still be struggling with.

- [Google Cloud Generative AI documentation is available here](https://cloud.google.com/docs/generative-ai)

## Useful Links
- [Google Cloud Vertex AI](https://cloud.google.com/vertex-ai?hl=en)
- [Google AI Studio](https://aistudio.google.com/prompts/new_chat)
- [Vertex AI Studio](https://cloud.google.com/generative-ai-studio?hl=en)

## Google Cloud Solutions

[Google Cloud Solutions](https://cloud.google.com/docs/tutorials) provides a vast range of QuickStart’s and tutorials to guide you through, and provide hands on experience with Google Cloud's products and services. These tutorials prove invaluable providing additional experience working with some of the services you may be less familiar with. You can simply filter by GenAI to relevant solutions, although these are more advanced and not essential for this certification.

## Priyanka Vergadia aka The Cloud Girl

For those who benefit more from visual learning- Priyanka Vergadia aka The Cloud Girl has created an excellent collection of [sketchnotes](https://thecloudgirl.dev/sketchnote.html) covering a wide range of Google Cloud products, services, and concepts in an easy to digest format. There are various [Machine Learning and GenAI sketches](https://www.thecloudgirl.dev/data-science-ml-ai) that are easy to digest which will help build the foundational knowledge required for the certification, including familiarisation with the different Google Cloud products and services. Priyanka also has various blogs again with graphical explainations for core concepts like [Eliminating hallucinations with RAG](https://www.thecloudgirl.dev/blog/rag-eliminating-hallucinations-in-llms) and [What is Agentic RAG vs Traditional RAG](https://www.thecloudgirl.dev/blog/what-is-agentic-rag-simplest-explanation).

![Why LLM's Hallucinate from Priyanka Vergadia](/assets/img/genaileader/why-.jpg "Example sketchnote for Google Cloud Load Balancer options from Priyanka Vergadia")

*Example sketchnote for Google Cloud Load Balancer Options from [Priyanka Vergadia]( https://thecloudgirl.dev/CLB.html)* 

The sketchnotes have been released as a book titled [Visualising Google Cloud](https://thecloudgirl.dev) which is a handy reference for getting to grips with Google Cloud's products and concepts for the Professional Cloud Architect and subsequent associate and professional exams. It is also a handy reference to have for day-to-day use as you are learning more about Google Cloud’s offerings.

Priyanka regularly posts videos on her social media channels including various [Cloud Bytes](https://youtube.com/playlist?list=PLIivdWyY5sqIQ4_5PwyyXZVdsXr3wYhip)  videos covering Google Cloud products in under a minute, and has her own blogs on [Medium](https://pvergadia.medium.com).

## Review the exam guide (yes, again!)
{:.no_toc}

Once you have completed all the training materials, review the exam guide again. This time you should feel more confident in your level of knowledge for each topic. If there are still topics in the guide you don't feel comfortable with, spend more time focussing on these, revisiting the content in the training courses, or researching the content in Google docs, and YouTube videos etc.

# Take the Google Cloud Foundational Generative AI Leader practice exam
{:.no_toc}

Once you are feeling confident you understand all the concepts covered in the exam guide, it's time to do a practice test. Google provides a [free practice test](https://docs.google.com/forms/d/e/1FAIpQLServ0tNGkr-dYAfmez_Gdk74dmVypZjzUKrkVFtFcArzhmPow/viewform) consisting of 15-20 questions to mimic the type of question you may see on the exam. 

Complete the practice exam as a closed book exam- don’t allow yourself to search for answers, or review study material prior to answering. It’s key to see how well you are performing and highlight areas of weakness you may need to improve prior to booking the real exam.

At the end of the practice exam, review all the questions including those you have got right and read the feedback provided by Google for each answer. This feedback clarifies why a particular answer is correct, and why others are incorrect, further consolidating your understanding of the subject. For any answers you are still unclear about, or if you feel the feedback doesn’t help you to understand why a particular answer is correct, spend more time revisiting the associated topic on one of the available training platforms or YouTube videos.

# Google Cloud Foundational Generative AI Leader Exam Strategy and Tips

Perform the first iteration of the exam quickly, answering the questions you are confident you know the answer for. If you don’t know the answer to a question, mark it for review at the end and try to rule out any incorrect answers from those available. Typically, there are a couple of answers that may be correct, however a subtle word within the question usually makes one of the answers a better fit than the others.

Once you complete your first iteration, review your marked questions, and spend more time on them accordingly. By taking this approach you can determine how long you can spend your remaining time on these tougher questions as you know how many you marked for review. You may also get lucky and find a later question on the exam helps you to identify the answer to a previous question you were unsure on either directly or indirectly by triggering a memory of some detail that earlier escaped you!

Upon completion of the exam, a provisional pass or fail is displayed on the screen. Look out for it, if it’s your first Google Cloud certification you can quite easily miss it as for whatever reason, it's not highlighted particularly well! Google subsequently confirms the pass/failure within 7-10 days' time (although it's often sooner!).

# How to book the Google Cloud Foundational Generative AI Leader exam
{:.no_toc}

The Google Cloud Foundational Generative AI Leader exam can be booked via Kryterion test centres on the [webassessor website](https://www.webassessor.com/googlecloud/). The exam can be taken in a test centre, or via a remote proctored exam monitored via a web camera and microphone.

![Kryterion logo](/assets/img/cdl/kryterionlogo.png "Kryterion logo")

*Kryterion Test Centres Logo*

Since covid I have been taking advantage of the remote proctored exams for convenience. The nearest test centre to me was around 1 hour away. There are a various [system requirements](https://kryterion.force.com/support/s/article/Online-Testing-Requirements?language=en_US) for online proctoring. This includes installing a secure browser application, and disabling various components that may interfere with the remote proctoring such as firewalls, anti-virus, pop up blockers etc. For this reason, Kryterion recommends you use a personal device for the exam. There is a system checker available to test internet speed, microphone, and webcam functionality [here](https://www.kryterion.com/systemcheck/).

Kryterion requires you to enrol in biometrics and create a biometrics profile which is used to identify yourself digitally based on facial characteristics. Each time you launch an exam, a biometric check is performed to validate you match your biometric profile. You can launch the remote proctored exam 10 minutes before your scheduled exam time. However, during busy times you may find you are waiting around for up to 30 minutes for a proctor to join and ‘secure the testing environment.’ This consists of displaying your government issued ID to the proctor, and then providing a 360-degree view of the room, and your clear desk to the proctor.

Once they are happy the room is secure, your exam is started. The proctor monitors you via the webcam and microphone and will pause the exam if there are any issues and contact you via the secure browser chat functionality. This has happened to me once when the proctor advised my video stream had stopped working mid-exam. The exam was paused whilst my laptop restarted, and the proctor verified the stream was working again. 

On a second occasion, the proctor advised my video stream wasn't working before the exam had started- a reboot failed to resolve the issue and I was advised to contact Kryterion support. This wasn't the greatest start to the exam, as I was now past my scheduled start time, however support were able to reschedule the exam to begin as soon a i had finished troubleshooting the issue with them, or I could book it for another day if it was no longer convenient.

It is best to book your exam ahead of time, as this gives you a date to work towards completing study and revision and helps ensure you get to choose a date/time that suits you best. If you leave booking the exam until after you finish your studying, you may find there aren’t as many convenient times available as you would like. If you find yourself in this position, check back regularly as I've seen a lot of times that were not available when checking the previous day, become available a day or two later. Provided you give at least 24 hours' notice, you are free to reschedule your exam to another time if for any reason you are not ready.

# How long is the Google Cloud Professional Cloud Network Engineer exam?
{:.no_toc}

The Professional Cloud Network Engineer exam is a two-hour exam during which you will need to answer 50-60 multiple choice and multiple select questions. 
I find for many of the professional certifications, I typically complete my first pass of the answers within an hour, however on the latest Professional Cloud Network Engineer exam I recall being 50% through the exam and having hit the one-hour mark. This got me rather worried that I wouldn't have time to review my questions and potentially may need to rush answering some of the later questions! Fortunately, the second half of questions were shorter and/or quicker for me to answer leaving me with 15 minutes to review and revisit any questions I was unsure on.

# How long is the Google Cloud Professional Cloud Network Engineer certification valid?
{:.no_toc}

All Google Cloud Professional certifications are valid for 2 years. You can recertify 60 days prior to certification expiration.

# How much does the Google Cloud Professional Cloud Network Engineer exam cost?
{:.no_toc}

The Google Cloud Professional Cloud Network Engineer exam costs $200 USD.

Thanks for taking the time to read this blog, I hope you find it useful in preparing for the Google Cloud Professional Cloud Network Engineer certification. Please feel free to share, [subscribe](https://www.cloudbabble.co.uk/subscribe) to be alerted to future posts, follow me on [LinkedIn](https://linkedin.com/in/jamiethompson85), and react/comment below! 

If you're new to Google Cloud certifications, or you're deciding what certification to do next, check out my other blog posts covering:

- [Google Cloud Professional Cloud Architect Certification](https://www.cloudbabble.co.uk/2023-02-28-Google-Cloud-Professional-Cloud-Architect/)
- [Google Cloud Digital Leader Certification](https://www.cloudbabble.co.uk/2022-12-06-GoogleCloudDigitalLeaderCertification/)

