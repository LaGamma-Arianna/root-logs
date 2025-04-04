---
title: "Project Phishing"
date: 2025-04-04
author: "A"
estimated_reading_time: "8-10 minutes"
---


# How I Caught a Phishing Email — and What It Taught Me About Email Security

The other day, I caught a phishing email right in my inbox.

It wasn’t the first time I’d seen suspicious messages, but this one felt different. It posed as a voicemail notification from "Microsoft Outlook," complete with the familiar branding and a large blue button:

> **"Preview or Download Voice Message"**

For a moment, it looked believable. But experience told me to pause.  
So, I checked the sender’s actual address:

> **techrely99admin@prizemons.com**

Not even close to legitimate.

Trusting my instincts, I reported the email using Outlook’s "Report Message" button. Moments later, I received confirmation:

![Phishing report confirmation](/root-logs/assets/images/phishing-report-confirmation.png)

It turned out this was part of an internal phishing simulation at William & Mary.  
The follow-up message reminded me that **91% of cyber-attacks start with phishing**, and catching these threats early plays a critical role in protecting not just ourselves, but our entire organization.

But I didn’t stop there.

---

## From Inbox to Investigation: Deepening My Understanding with TryHackMe

Encouraged by catching this phishing attempt, I decided to keep going.  
I had been working through TryHackMe’s **SOC Level 1** pathway, and it felt like the perfect opportunity to build on this experience.

In the room on **Phishing Prevention**, the training walked through how defenders can go beyond just reporting suspicious emails. It covered essential strategies like:
- Setting up **SPF, DKIM, and DMARC** records to protect domains.
- Using **spam filters** and **email sandboxing** for attachments.
- Running **internal phishing simulations** (like the one I experienced).
- Leveraging **security awareness training** to empower every user.

What struck me is how all these layers work together.  
Basic vigilance catches many threats, but **email security technologies** catch what human eyes might miss — and vice versa.

The SOC Level 1 training helped me connect the dots between everyday email hygiene and the larger defense strategies used by Security Operations Centers (SOCs). I saw how analysts not only detect and report phishing but also investigate and neutralize these attacks with technical precision.

I realized: **reporting phishing is step one. Understanding why it works, and how to defend against it systematically, is step two.**

This post is my way of sharing what I learned from both experiences.

---

## ✉️ SPF vs. DKIM: Who's Protecting What?

When you think about protecting emails, you might imagine spam filters or antivirus. But email security begins *before* messages hit your inbox.

### ✅ SPF: Sender Policy Framework

SPF is like your domain’s bouncer list.

It tells mail servers, **“Here are the legitimate IP addresses allowed to send mail from my domain.”**

Example SPF record:
v=spf1 ip4:192.168.1.1 include:_spf.google.com -all


➡️ **SPF checks the sender’s mail server, not the email content.**

### ✅ DKIM: DomainKeys Identified Mail

DKIM is about making sure the message **hasn’t been tampered with**.

It attaches a cryptographic signature to the email, and the recipient checks this against a public key published in DNS.

Example DKIM record:
v=DKIM1; k=rsa; p=<public_key>


➡️ **DKIM focuses on integrity and authenticity of the message.**

---

## 🛡️ DMARC: The Enforcer

If SPF and DKIM are the guards, **DMARC** is the policy manager.

It tells mail servers what to do if an email fails authentication — and sends reports so you know who’s trying to impersonate your domain.

Example DMARC record:
v=DMARC1; p=reject; rua=mailto:security@domain.com


➡️ **DMARC ties SPF and DKIM together, adds enforcement, and provides visibility.**

---

## 🔒 S/MIME: Securing the Conversation

While SPF, DKIM, and DMARC work at the delivery level, **S/MIME** (Secure/Multipurpose Internet Mail Extensions) protects the *content* of your emails.

S/MIME ensures:
- **Confidentiality** (encryption)
- **Integrity and authenticity** (digital signature)

Using public-key cryptography, S/MIME encrypts emails and verifies the sender’s identity.

➡️ **S/MIME is crucial for sensitive communications within organizations.**

---

## 🕵️ Wireshark: Peering Into Email Traffic

The SOC Level 1 room also covered traffic analysis — and it made me appreciate **Wireshark** even more.

### 🎯 Filter SMTP Status Codes:
smtp.response.code

This helps you spot:
- **220**: Service ready
- **354**: Start mail input
- **550**: Mailbox unavailable

### 🧩 Source vs. Destination Ports Explained

| | Sender (Client) | Receiver (Server) |
|---|---|---|
| **Source Port** | Random high port (e.g., 51000) | Typically port 25 (SMTP) |
| **Destination Port** | Port 25 (SMTP standard) | Sender’s random port |

➡️ **If traffic is headed to port 25, it’s likely email outbound.  
If it’s coming *from* port 25, it’s likely a server response.**

Understanding this helped me see how attackers might use normal-looking email traffic to hide their malicious communications.

---

## 🚨 Adversaries Use Email for Command and Control (C2)

One eye-opening part of the SOC Level 1 training was learning about how attackers **abuse email protocols for C2** communications.

According to MITRE ATT&CK’s technique **T1071.003**, attackers use protocols like SMTP and POP3 to:
- Send commands to infected systems
- Exfiltrate stolen data
- Blend in with normal email traffic

Real-world example: **Zebrocy malware** — it communicates via email protocols to evade detection.

### Defense Tips:
- Use **intrusion detection systems (IDS)** to monitor traffic patterns.
- Investigate unusual SMTP or POP3 flows.
- Block suspicious IPs and domains via **threat intelligence feeds**.

➡️ **Phishing prevention isn’t just about spam filters. It’s about spotting attackers using legitimate protocols for malicious goals.**

---

## 🧰 Building a Resilient Email Security Stack

Here's my current toolkit for defending against phishing and email-based attacks, inspired by the THM room experiences.

| Tool | Purpose |
|------|----------|
| SPF, DKIM, DMARC | Email authentication & enforcement |
| S/MIME | Secure sensitive communications |
| Wireshark | Deep traffic analysis |
| Spamhaus, Talos | Reputation-based blocking |
| Any.Run, VirusTotal | Analyzing suspicious attachments |
| Intrusion Detection Systems (IDS) | Detect stealthy C2 communications |

---

## Final Thoughts

What started as a simple phishing simulation turned into a deep exploration of the systems that protect our inboxes every day.

Catching that fake voicemail email felt like a small victory — but understanding **why it worked**, and how defenders respond to these threats at scale, was even more powerful.

From SPF to S/MIME, from network packet analysis to attacker C2 tactics, every layer of email security plays a role. And as defenders, it’s our job to know how they work — not just rely on tools, but understand the "why" behind them.

If this post sparked your curiosity, stay tuned! I’ll be sharing more soon:
- Building custom Wireshark filters for threat hunting
- Automating SPF/DKIM/DMARC checks
- Crafting a phishing incident response playbook

Until then — stay curious, stay cautious, and don’t stop learning.

---

## 📝 Quick Quiz: Test Your Knowledge!

Before you go, see how much you remember:

1. **What does SPF validate in an email?**
   - A) The sender's IP address  
   - B) The email body  
   - C) The email subject line

2. **Which protocol ensures the contents of an email aren’t tampered with?**
   - A) DKIM  
   - B) SPF  
   - C) SMTP

3. **What does DMARC do when an email fails SPF and DKIM?**
   - A) Encrypts the email  
   - B) Applies the configured policy (none/quarantine/reject)  
   - C) Sends it automatically to the user’s inbox

4. **What Wireshark filter helps you see SMTP response codes?**
   - A) `smtp.response.code`  
   - B) `ip.addr == 25`  
   - C) `http.response.code`

5. **What type of malware is known to use SMTP and POP3 for C2 communications?**
   - A) Zebrocy  
   - B) Emotet  
   - C) Wannacry

*Answers:*  
1. A | 2. A | 3. B | 4. A | 5. A

---

