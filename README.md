# URL Playbook

## Overview

I recently completed the design for a URL Playbook in Splunk Phantom SOAR. While I haven't fully implemented it yet, I've successfully set up alerts from Splunk with artifacts to Phantom SOAR, along with the ability to perform queries from Phantom back to Splunk. I'm excited to share the structure and workflow I've laid out!
## Table of Contents

- [Playbook Workflow](#playbook-workflow)
- [Diagram](#diagram)
- [Tools Used](#tools-used)
- [How to Use](#how-to-use)

## Playbook Workflow

The playbook operates through the following steps:

1. **Initial URL Checks**
   - Query VirusTotal
   - Query MetaDefender Sandbox
   - Query Joe Sandbox
   - Query Falcon Sandbox

2. **If URL is Malicious**:
   - Check if the URL is allowed on the proxy:
     - If **Allowed**:
       - Block URL on Proxy
       - Create Incident Ticket
       - Notify SOC via Email
       - Perform a Splunk query to list affected users
       - LDAP Machine Resolution
       - Notify Incident Response Team
       - Scan Machines
       - Acquire Downloads, Browser History ..
       - Wait for Manual Interaction (Isolation Decision)
       - If isolation is needed, quarantine devices.
     - If **Blocked**:
       - Check Referer URL
       - Analyze for Suspicious Activity (User Agent, Traffic, Content-Type, URI Scheme, Category ..)
       - If suspicious, notify SOC and repeat the incident response steps.
       - If all checks are clean, end the process.

3. **If URL is Clean**:
   - Repeat the checks for the Referer URL and assess for suspicious activity.
  
## Diagram
   ![URL Playbook Diagram](https://github.com/Yusuf-Amr/URL_Playbook/blob/main/Diagram/URL%20Playbook%20Diagram.jpg)
   
   ![URL Playbook Diagram](https://github.com/Yusuf-Amr/URL_Playbook/blob/main/Diagram/flow.jpg)

    
## Tools and Technologies Considered:

- VirusTotal
- MetaDefender Sandbox
- Joe Sandbox
- Falcon Sandbox
- Splunk
- LDAP
- Zscaler Proxy
- Microsoft Defender for Endpoint (EDR)
- JIRA to perform ticket management actions
- SMTP for sending emails

## How to Use

1. Download the URL_Playbook.tgz file.
2. Open the Splunk Phantom SOAR interface.
3. Navigate to the Playbooks section.
4. Click on the Upload button and select the downloaded .tgz file.
