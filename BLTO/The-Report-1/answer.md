# The Report 1

*You are working in a newly established SOC where still there is lot of work to do to make it a fully functional one. As part of gathering intel you were assigned a task to study a threat report released in 2022 and suggest some useful outcomes for your SOC.*

# Questions

## 1. Name the supply chain attack related to Java logging library in the end of 2021.

As mentioned in the question, this attack is located in **Supply Chain Attack** page 15. Throughout reading the Supply Chain Attack, I noticed that only **Log4j** is a Java logging library that was hit with a remote code execution vulnerability in December 2021.

**Answer: Log4j**

## 2. Mention the MITRE Technique ID which effected more than 50% of the customers.

MITRE Technique starts from page 72, where we can find various types of top technique used to help detect malicious activity. I'll write the table below:

| **Technique ID** | **Name** | **Technique Rank** | **% Of Customers Affected** |
| ---------- | -------- | ------------------ | --------------------------- |
| T1059 | Command and Scripting Interpreter | 1 | 53.4% |
| T1218 | Signed Binary Proxy Execution | 2 | 34.8% |
| T1047 | Windows Management Instrumentation| 3 | 15.4% |
| T1003 | Credential Dumping | 4 | 18.3% |
| T1105 | Ingress Tool Transfer | 5 | 20.4% |
| T1055 | Process Injection | 6 | 21.7% |
| T1053 | Scheduled Task/Job | 7 | 14.7% |
| T1027 | Obfuscated Files or Information | 8 | 19.4% |
| T1036 | Masquerading | 9 | 22.1% |
| T1574 | Hijack Execution Flow | 10 | 8.4% |

Now we can see that only 1 technique has more than 50% customers affected and that is **T1059**.

**Answer: T1059**

## 3. Submit the names of 2 vulnerabilities belonging to Exchange Servers.

Vulnerabilities starts on page 17, and in the beginning paragraphs, we can already get the answer for this question: 

> *"Several high-profile vulnerabilities made it into the collective consciousness of the security community in 2021. ProxyLogon and ProxyShell targeted Microsoft Exchange servers and affected a massive number of systems, sometimes leading to ransomware deployment."*

**Answer: ProxyLogon, ProxyShell**

## 4. Submit the CVE of the zero day vulnerability of a driver which led to RCE and gain SYSTEM privileges.

Reading throughout the **Vulnerabilities** section, I noticed one vulnerability which is **PrintNightmare** that exploits a printer spooler service which  fails to properly authenticate users attempting to load a printer driver dynamic link library (DLL) and allowing code execution with local SYSTEM- level privileges.

So the CVE for **PrintNightmare** is **CVE-2021-34527**.

**Answer: CVE-2021-34527**

## 5. Mention the 2 adversary groups that leverage SEO to gain initial access.

Since the question is about SEO (Search Engine Optimization), I navigate to page 29 where I found **User-initiated initial access**. From there, I read the articles and found out that **Gootkit and Yellow Cockatoo** abuse search engine optimization (SEO) to lure victims.

**Answer: Gootkit, Yellow Cockatoo**

## 6. In the detection rule, what should be mentioned as parent process if we are looking for execution of malicious js files. [Hint: Not CMD]

For answering this question, we have to find attacks that are using the execution of malicious js files. We can find the Threats starting from page 44. After I thoroughly read the Threats, I found one attack that matches the question and that is **Gootkit**. Inside it, I also found a snippet of code that will execute the Javascript:

 ```
process == wscript.exe
&&
file_path_includes ( %APPDATA% )
```
From the snippet, we can conclude that it uses ```wscript.exe``` as the parent process.

**Answer: wscript.exe**

## 7. Ransomware gangs started using affiliate model to gain initial access. Name the precursors used by affiliates of Conti ransomware group.

This question is quite easy as we can just go to page 11 to see the lists of affiliate models of Ransomware:

| Malware Family (Precursor) | Ransomware Group |
| -------------- | ---------------- |
| Qbot | Egregor |
| Qbot | Sodinokibi/REvil |
| Qbot | Conti |
| Bazar | Conti |
| IceID | Conti |

Now we can see that we have 3 malware family.

**Answer: Qbot, Bazar, IceID**

## 8. The main target of coin miners was outdated software. Mention the 2 outdated software mentioned in the report.

This question is about Linux coinminers which is in page 33. There I have to read the whole article and I found the answer on the **Take Action** Block that says:

>  *"Many of the coinminers we saw exploited flaws in outdated applications like **JBoss and WebLogic**, so keeping systems updated will deter adversaries who are simply scanning for applications with known vulnerabilities."*

Therefore the answer for this is clear.

**Answer: JBoss, WebLogic**

## 9. Name the ransomware group which threatened to conduct DDoS if they didn't pay ransom.

The answer for this is in page 12 under Ransomware attack. In the second paragraph of ```Beyond encryption``` part which is:

> *"Adversaries realized they could demand payment for more than just the threat of a data leak or encryption. An adversary known as **Fancy Lazarus** (no affiliation with Fancy Bear or Lazarus Group) extorted victims by threatening to conduct a distributed denial of service (DDoS) intrusion if they didn’t pay."*

**Answer: Fancy Lazarus**

## 10. What is the security measure we need to enable for RDP connections in order to safeguard from ransomware attacks?

Still on the same article as the previous question, we can take a look on the **Take Action** Block, specifically on the last sentence of first paragraph that says:

> *"Additionally, internet-facing remote desktop protocol (RDP) connections without **multi-factor authentication (MFA)** are a common ransomware vector, making MFA for any accounts that can log in via RDP a high priority."*

**Answer: MFA**

# Summary

Rating: ★★★★☆ | Difficulty: ★☆☆☆☆

This practice doesn't really need a lot of knowledge as we are being tasked to read an article in order to answer the questions. It just take times to find all of the answers, but that's the point in this practice. 