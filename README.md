# Phishing-Incident-Analysis
This project demonstrates core skills in the "Analyze" stage of the Security Operations Center (SOC) workflow. The objective was to methodically triage a suspicious email, reverse-engineer its origination using technical headers, identify social engineering tactics, and produce actionable Indicators of Compromise (IOCs) for immediate mitigation.

### Skills Learned

- Email Header Analysis: Proficiently tracing the path of an email via Received headers and identifying the true sender IP address.
- Email Authentication: Interpreting SPF, DKIM, and DMARC results to validate sender legitimacy and spot spoofing attempts.
- Threat Intelligence: Utilizing open-source tools (e.g., URLScan.io, VirusTotal) to safely analyze malicious URLs and domains.
- Social Engineering Recognition: Documenting and classifying the psychological tactics (urgency, fear, branding) used by attackers.
- Incident Response Documentation: Formulating a structured report that identifies the attack vector, analysis findings, and clear mitigation steps.

### Tools Used

- Online Email Header Analyzer ( MXToolbox,AbuseIpDB)
- URL Analysis Service (e.g., URLScan.io, VirusTotal)
- Raw Email Source (Phishing Pot GitHub)

## Steps

Example below.

*Ref 1: Email Body/Content*
<img width="1914" height="871" alt="ref1" src="https://github.com/user-attachments/assets/b8f175bc-39a3-44fd-9208-a6327eb67872" />

- the email appears to be a security alert of an unusual sign-in actvity for an enduser's Microsoft account.
-  the email is branded as a legitimate company to create a false sense of trust.
-  the enduser is instructed to click a button that will "report the user".

*Ref 2a: Raw Email Source Analysis*
<img width="1514" height="978" alt="image" src="https://github.com/user-attachments/assets/55f65b1f-a094-4ebc-8365-2aeb926c042f" />
- The raw email source was submitted to the header analyzer, which simplified the Received headers.
-  The return path is bounce@thcultarfdes.co.uk but the sender address is Microsoft Account team no-reply@access-accsecurity.com generating an inconsistency.
-  Spoofing is being performed to trick the enduser into thinking the email came from Microsoft Account Team

*Ref 2b: Raw Email Source Analysis*
<img width="1501" height="928" alt="Screenshot 2025-10-23 104500" src="https://github.com/user-attachments/assets/af8f41fb-6c05-4ce6-aba0-cb85c478d74b" />

- Using the find feature within the text editor, i searched for spf (Sender Policy Framework), results displayed none which is alarming due to most legitimate domains will configure this record to specify which IP addresses and servers are authorized to send email on behalf of that domain.


*Ref 3: Header Analyzer Output*
<img width="1884" height="627" alt="Screenshot 2025-10-23 110443" src="https://github.com/user-attachments/assets/ced26a23-09d8-48b8-bf4a-c5168ab1c80e" />

- Using mxtoolbox I analyzed the email header.
-  The authentication checks revealed a none for spf and a failed for dkim.
-  These results indicate the sender was unauthorized  to use the domain confirming a spoofing attempt

*Ref 4: Sender IP Analysis*
<img width="1401" height="883" alt="Screenshot 2025-10-23 111408" src="https://github.com/user-attachments/assets/36a505e2-f6f6-4bd8-9e72-f3d563bc583d" />

# Using AbuseIPDB I performed analysis of the sender's original ip address and uncovered the following:
-  Hosting Provider Misalignment: The IP is hosted by a generic Data Center/Web Hosting provider (GHOSTNET GmbH), which is suspicious because legitimate corporate emails do not typically originate from this type of infrastructure, strongly suggesting malicious staging.
-  Significant Historical Abuse: The record shows the IP has been reported 30 times by 10 different sources, indicating a history of being used for abusive or questionable activities, which elevates its inherent risk profile.
-  Naming Coincidence: The association with the ISP name GHOSTNET (even if coincidental to the historic APT) will immediately trigger high vigilance and scrutiny from analysts due to the known threat actor nomenclature.

 # Mitigation and Containment
  <img width="951" height="267" alt="image" src="https://github.com/user-attachments/assets/8ad615a7-2d32-4bb1-957e-bc4842809273" />


# Final Reflections

This hands-on lab successfully demonstrated key SOC triage skills. We confirmed a phishing attempt by identifying social engineering (false branding and fear) and spoofing through failed SPF/DKIM authentication. Technical analysis of the sending IP exposed its origin in a high-risk data center with a history of abuse. This structured workflow, combining content review with deep technical inspection, was effective in generating high-confidence Indicators of Compromise (IOCs) essential for rapid organizational mitigation.



