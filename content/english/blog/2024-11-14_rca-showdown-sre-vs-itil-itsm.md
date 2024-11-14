---
title: "RCA Showdown: SRE vs. ITIL/ITSM, and Why We Should All Just Get Along"
date: 2024-11-14T16:00:00+00:00
# watermark text
watermark: "Tech Blog"
# page header background image
page_header_image: "https://github.com/user-attachments/assets/35fd3701-e7d0-40ac-a6a1-6958a0abbd5d"
# meta description
description: "SRE and ITIL/ITSM don’t have to be adversaries. When combined thoughtfully, they can produce an RCA process that is greater than the sum of its parts."
# post image
image: "https://github.com/user-attachments/assets/35fd3701-e7d0-40ac-a6a1-6958a0abbd5d"
# post author
author: "Carlos Manuel Soares"
# post categories
# post categories
categories: ["Site Reliability Engineering", "IT Service Management", "Incident Management", "Root Cause Analysis", "System Reliability", "IT Operations", "DevOps Practices", "IT Governance", "Tech Collaboration", "Engineering Best Practices"]
# post tags
tags: ["Site Reliability Engineering", "SRE", "ITIL", "ITSM", "Root Cause Analysis", "RCA", "Incident Management", "Postmortem", "Blameless RCA", "System Reliability", "Process Improvement", "Service Level Agreements", "SLAs", "Technical Debt", "Automation", "Change Management", "Collaboration", "Preventive Actions", "Metrics and Reporting", "Continuous Improvement", "DevOps", "Engineering Practices", "IT Governance", "Incident Response"]
# type
type: "post"
license: <a rel=\"license external nofollow noopener noreffer\" href=\"https://creativecommons.org/licenses/by-nc/4.0/\"
  target=\"_blank\">CC BY-NC 4.0</a>
comment: true
medium_repost_url: ""
---

# RCA Showdown: SRE vs. ITIL/ITSM, and Why We Should All Just Get Along

Ah, the humble RCA (Root Cause Analysis). On the surface, it’s a simple concept: something went wrong, so let’s figure out why and make sure it doesn’t happen again. But when you bring together teams from the **SRE** camp and the **ITIL/ITSM** world, things can get… lively. These two camps have different philosophies, goals, and even jargon. If left unchecked, this can lead to misunderstandings, frustration, and possibly the kind of workplace tension that makes the weekly stand-up feel like a Shakespearean tragedy.

But here’s the kicker: SRE and ITIL/ITSM don’t have to be adversaries. In fact, when combined thoughtfully, they can produce an RCA process that’s greater than the sum of its parts. Let’s break this down, shall we?

---

## What’s an RCA Anyway? 

For those new to the world of acronyms, RCA stands for **Root Cause Analysis**. It's the process of identifying what went wrong, why it went wrong, and what can be done to prevent it from happening again. Think of it as a post-mortem for incidents, only without the creepy medical overtones.

At its core, RCA is about learning and improving. But how you approach it depends heavily on whether you're wearing an SRE or ITIL/ITSM hat.

---

### The SRE Way: Blameless, Automated, and Always Learning

Let’s start with the SREs. Born out of Google’s engineering philosophy, **Site Reliability Engineering** focuses on system reliability, automation, and reducing toil (i.e., repetitive, soul-crushing manual work). When something breaks, SREs conduct **blameless RCAs**. The goal? Identify what went wrong without pointing fingers, so the team can focus on system improvements.

#### Key features of SRE RCAs:
- **Blamelessness**: Incidents are viewed as opportunities to learn, not to assign blame.
- **Data-Driven**: Metrics and logs are examined to paint a clear picture of what happened.
- **Automation-Centric**: Preventive actions often include automating tests, monitoring, or recovery processes.

SRE RCAs aren’t just about fixing the immediate problem. They’re about making the entire system more resilient. If a manual process failed, the solution might be to automate it. If monitoring didn’t catch an issue, new alerts are created.

---

### The ITIL/ITSM Way: Process-Oriented and Customer-Focused

Now let’s look at **ITIL/ITSM** (Information Technology Infrastructure Library / IT Service Management). While ITSM refers to the overall discipline of managing IT services, ITIL is one of the most popular frameworks within ITSM, known for its focus on structured processes and risk management. These frameworks are all about process discipline, risk management, and service delivery. In the ITIL world, incidents and problems are carefully documented, and RCAs are conducted to ensure **service continuity** and compliance with **SLAs (Service Level Agreements)**.

#### Key features of ITIL RCAs:
- **Structured and Formal**: Every incident has a clear process for investigation, typically with assigned roles and responsibilities.
- **Process Compliance**: The focus is often on ensuring that proper processes were followed (or identifying where they weren’t).
- **Customer-Centric**: RCAs consider the business and customer impact, ensuring service levels are maintained.

ITIL RCAs are thorough and methodical, but they can sometimes feel rigid to those used to SRE’s more dynamic, engineering-driven approach.

---

### Philosophical Differences: SRE vs. ITIL/ITSM

Here’s where it gets interesting. SRE and ITIL/ITSM are rooted in different philosophies:

- **SRE** focuses on **system reliability** and **continuous improvement** through automation and engineering practices.
- **ITIL/ITSM** prioritises **process adherence** and **risk management**, ensuring services are delivered consistently and meet business expectations.

In other words, SREs want to fix systems and automate away problems, while ITIL practitioners want to ensure processes are followed to prevent risk. These aren’t contradictory goals, but they can lead to misunderstandings if not properly aligned.

---

## The Elephant in the Room: Separating Technical and Process Root Causes

One of the most effective ways to bridge the gap between SRE and ITIL/ITSM is to **separate technical root causes from process root causes** during RCA. Why? Because each team has a different focus, and lumping everything together can lead to confusion.

### **Why Bother?**

1. **Clarity and Focus**  
   SREs focus on **technical reliability**: Was there a bug? Did monitoring fail? Meanwhile, ITIL folks care about **process compliance**: Did someone bypass the change management process? Separating these discussions ensures that both technical and process issues get the attention they deserve.

2. **Tailored Preventive Actions**  
   Different problems need different solutions. Technical issues might require automation or improved testing, while process gaps may call for updated workflows or better training. By separating root causes, you ensure that preventive actions are specific and actionable.

---

### **How to Do It**

Here’s how to make this work in practice:

1. **Define Categories in Your RCA Template**  
   Create distinct sections in your RCA template:
   - **Technical Root Causes**: Focus on system failures, such as bugs, misconfigurations, or infrastructure issues.
   - **Process Root Causes**: Focus on procedural gaps, such as skipped approvals or miscommunication.

   Example table:

   | **Root Cause Type** | **Details**                                     |
   |---------------------|-------------------------------------------------|
   | Technical            | Outdated monitoring rule missed the alert.      |
   | Process              | Change request bypassed approval process.       |

2. **Ask Targeted Questions**  
   Guide your RCA discussions with specific questions:
   - **For Technical Issues**: What failed in the system? Were there gaps in testing or monitoring?  
   - **For Process Issues**: Were proper procedures followed? Was there a communication breakdown?

3. **Collaborative RCA Sessions**  
   Hold RCA meetings that include both SREs and ITIL practitioners. Start with technical root causes (led by SREs), then move to process root causes (led by ITIL). This structure ensures that both areas are covered without stepping on each other’s toes.

4. **Track and Review**  
   Use a shared platform to track preventive actions for both technical and process issues. Regularly review their effectiveness and adjust as needed.

---

### The Best of Both Worlds: Combining SRE and ITIL/ITSM RCAs

Now that we’ve covered separating technical and process root causes, how do we bring everything together into a unified RCA process? Here’s the trick: **communication and collaboration**.

1. **Unified RCA Framework**  
   Design an RCA process that caters to both SRE and ITIL needs:
   - **Technical Analysis (SRE)**: Dig into logs, metrics, and code.
   - **Process Analysis (ITIL)**: Review workflows, approvals, and SLA impacts.

2. **Blameless Culture for All**  
   Blame is off the table for both technical and process issues. The goal is learning and improving, not finger-pointing.

3. **Collaborative Preventive Actions**  
   Preventive actions should cover both worlds:
   - **SRE**: Automation, better monitoring, more robust testing.
   - **ITIL**: Workflow updates, enhanced documentation, training.

4. **Unified Metrics and Reporting**  
   Use combined metrics:
   - **SRE Metrics**: System uptime, MTTR (Mean Time to Recovery).
   - **ITIL Metrics**: SLA adherence, incident resolution times.

---

## Why Collaboration Is Key

Here’s the bottom line: SRE and ITIL/ITSM don’t have to clash. In fact, when they work together, they can create an RCA process that’s both **robust** and **flexible**. Separating technical and process root causes while fostering communication ensures everyone knows what’s being discussed and why. This not only improves the RCA process but also builds a stronger, more collaborative culture.

So next time you’re in an RCA meeting, remember: SREs and ITIL/ITSM practitioners aren’t enemies. They’re just two sides of the same coin, working together to ensure our systems and services run smoothly. And that’s a mission we can all get behind.
