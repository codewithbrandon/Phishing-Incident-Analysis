# Phishing-Incident-Analysis
This project demonstrates core skills in the Analyze stage of the Security Operations Center (SOC) workflow. The objective was to methodically triage a suspicious email, reverse-engineer its origination using technical headers, identify social engineering tactics, and produce actionable Indicators of Compromise (IOCs) for immediate mitigation.

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
<img src="fishlab/ref1.png" />

- the email appears to be a security alert of an unusual sign-in actvity for an enduser's Microsoft account.
-  the email is branded as a legitimate company to create a false sense of trust.
-  the enduser is instructed to click a button that will "report the user".

*Ref 2a: Raw Email Source Analysis*
<img src="fishlab/ref2.png"/>
- The raw email source was submitted to the header analyzer, which simplified the Received headers.
-  The return path is bounce@thcultarfdes.co.uk but the sender address is Microsoft Account team no-reply@access-accsecurity.com generating an inconsistency.
-  Spoofing is being performed to trick the enduser into thinking the email came from Microsoft Account Team

*Ref 2b: Raw Email Source Analysis*
<img src="fishlab/ref3.png" />

- Using the find feature within the text editor, i searched for spf (Sender Policy Framework), results displayed none which is alarming due to most legitimate domains will configure this record to specify which IP addresses and servers are authorized to send email on behalf of that domain.


*Ref 3: Header Analyzer Output*
<img src="fishlab/ref4.png" />

- Using mxtoolbox I analyzed the email header.
-  The authentication checks revealed a none for spf and a failed for dkim.
-  These results indicate the sender was unauthorized  to use the domain confirming a spoofing attempt

*Ref 4: Sender IP Analysis*
<img src="fishlab/ref5.png" />

# Using AbuseIPDB I performed analysis of the sender's original ip address and uncovered the following:
-  Hosting Provider Misalignment: The IP is hosted by a generic Data Center/Web Hosting provider (GHOSTNET GmbH), which is suspicious because legitimate corporate emails do not typically originate from this type of infrastructure, strongly suggesting malicious staging.
-  Significant Historical Abuse: The record shows the IP has been reported 30 times by 10 different sources, indicating a history of being used for abusive or questionable activities, which elevates its inherent risk profile.
-  Naming Coincidence: The association with the ISP name GHOSTNET (even if coincidental to the historic APT) will immediately trigger high vigilance and scrutiny from analysts due to the known threat actor nomenclature.

 # Mitigation and Containment
  <img src="fishlab/ref6.png" />


# Final Reflections

This hands-on lab successfully demonstrated key SOC triage skills. We confirmed a phishing attempt by identifying social engineering (false branding and fear) and spoofing through failed SPF/DKIM authentication. Technical analysis of the sending IP exposed its origin in a high-risk data center with a history of abuse. This structured workflow, combining content review with deep technical inspection, was effective in generating high-confidence Indicators of Compromise (IOCs) essential for rapid organizational mitigation.



