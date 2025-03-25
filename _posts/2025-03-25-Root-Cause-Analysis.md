---
layout: post
title: "Why Root Cause Analysis Matters: Lessons from Security+"
date: 2025-03-26
---

When I was preparing for the CompTIA Security+ exam, one of the questions that stuck with me was:

> **"What is the primary benefit of conducting a thorough root cause analysis?"**

The answer choices were:

A. Media attention  
B. Compliance with industry regulations  
C. Legal protection  
D. Preventing the recurrence of similar incidents

At first glance, option D might sound obvious, but it's a fundamental concept in cybersecurity that often gets overlooked. When an incident occurs — whether it's a phishing email, a data leak, or a misconfigured cloud bucket — identifying *what happened* isn't enough. We need to dig deeper to understand *why* it happened and how to stop it from happening again.

That’s where **Root Cause Analysis (RCA)** comes in.

---

### 🛠️ How to Perform an RCA Step-by-Step

Root cause analysis isn’t flashy. It’s not about big headlines or "aha" moments. It's more like digital archaeology — methodical, layered, and deeply investigative.

Let’s say you're working in a Security Operations Center (SOC), and your SIEM flags some suspicious outbound traffic from an internal workstation.

At first glance, this might look like malware beaconing out. But to perform a solid RCA, you don’t just block the IP and move on — you go step by step.

#### **1. Incident Detection**  
The SIEM alert tells you *something* unusual is happening. That’s your starting point. You check the alert details, maybe a spike in DNS requests or outbound traffic to a known malicious domain.

#### **2. Evidence Collection**  
Now it’s time to dig. You pull logs from the firewall, the workstation, and the proxy. You might export a memory image or check email records to see if the user clicked something suspicious.

#### **3. Timeline Reconstruction**  
You piece together what happened and when. Maybe the user opened a phishing email at 9:02 AM, clicked a link at 9:03, and the malware reached out by 9:05. This timeline becomes your foundation for understanding the whole incident.

#### **4. Root Cause Identification**  
This is where the big picture comes into focus. You realize the user clicked a link in a convincing fake invoice. The macros were enabled in their Word settings. Digging further, you find that their device was set up manually — outside the usual provisioning process — so it missed the standard endpoint protections.

#### **5. Remediation & Documentation**  
You clean the device and close the immediate threat. But more importantly, you update the provisioning checklist, create a detection rule for similar activity, and document the full RCA so your team — and future you — can learn from it.

That’s RCA in action. It’s not just about solving the problem. It’s about solving the *right* problem, and keeping it from happening again.

---

### 🧠 The 5 Whys: A Simple Way to Dig Deeper

One of the techniques I really came to appreciate — and honestly used to overlook — is the **5 Whys** method. It seemed too abstract at first, like a thought exercise rather than a real tool. But once I started applying it in hands-on labs and scenarios, I realized how effective it is for cutting through assumptions and getting to the actual cause.

The idea is simple: keep asking "why?" — usually five times — until you’ve peeled back the layers of what really went wrong.

#### **Example:**

- 🔍 *Why* was malware detected on the workstation?  
  → A user opened a malicious attachment.

- 🔍 *Why* did the attachment execute?  
  → Macros were enabled in the Word document.

- 🔍 *Why* were macros enabled by default?  
  → Group policy didn’t disable them.

- 🔍 *Why* wasn’t the group policy applied correctly?  
  → The device was provisioned manually.

- 🔍 *Why* was the device provisioned manually?  
  → It was a contractor laptop set up in a rush.

What started as "the user clicked something bad" becomes a story about **missing controls in the provisioning process** — and *that’s* the thing that can be fixed long-term.

The 5 Whys is abstract, yes — but powerful. It helps connect technical events to organizational issues, and that’s often where the real solutions live.

---

Root cause analysis is more than a multiple choice answer. It’s a mindset — one that pushes us to learn, adapt, and make systems more resilient. For me, it’s one of the most powerful skills I’ve started developing as I go through TryHackMe rooms and build up my SOC-level knowledge.

I’ll be writing more posts like this — from forensic walkthroughs to real RCA breakdowns — and using this space to track what I’m learning.

The logs are open. Trace the path, dig around, and follow along if you're navigating this space too.

— see you on the wire,  
**Arianna**
