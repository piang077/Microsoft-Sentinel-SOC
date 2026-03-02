# Microsoft Sentinel SOC Investigation Lab

## Incident Management & Threat Hunting Case Study

---

## Project Overview

This project simulates the real-world workflow of a Security Operations Center (SOC) Analyst using **Microsoft Sentinel** to investigate, triage, enrich, and respond to security incidents.

The objective was to practice incident ownership, investigation, threat hunting, automation, and incident documentation following SOC operational procedures.

---

## Objectives

* Investigate security incidents using Microsoft Sentinel
* Perform log analysis and incident enrichment
* Conduct threat hunting using KQL queries
* Identify affected assets and Indicators of Compromise (IOC)
* Apply incident response and documentation procedures
* Simulate SOC handover to another operational team

---

## Tools & Technologies

* Microsoft Sentinel (SIEM)
* Log Analytics Workspace
* Kusto Query Language (KQL)
* Sentinel Workbooks
* Automation Rules & Playbooks
* Threat Intelligence Management
* Cisco Umbrella DNS Logs (ASIM normalized)

---

## Scenario 1 — Suspicious Sign-ins to Disabled Accounts

### Incident

**Alert:** Sign-ins from IPs attempting authentication to disabled accounts

---

### Step 1: Incident Triage

* Navigated to Sentinel **Incidents**
* Reviewed incident severity and entities involved
* Assigned incident ownership
* Changed status from **New → Active**

SOC Practice:

* Ensures accountability
* Prevents duplicate investigations

![Incident Triage](screenshots/step1-incident-triage.png)

*Figure 1 — Reviewing incidents and assigning ownership in Microsoft Sentinel*

---

### Step 2: Log Investigation

* Accessed raw alert events via **Log Analytics**
* Reviewed authentication logs including:

  * Source IP address
  * User accounts targeted
  * Login outcomes
  * Timestamp patterns

Observed repeated authentication attempts from external IP.

---

### Step 3: Incident Enrichment

Executed Sentinel Playbook:

**Get-GeoFromIpAndTagIncident**

Actions performed:

* Retrieved geographic intelligence of IP
* Automatically tagged incident
* Added investigation context

Result:
Suspicious IP traced to **North Korea**.

---

### Step 4: Investigation Using Workbook

Used **Investigation Insights Workbook** to pivot investigation.

Findings:

* Multiple successful logins linked to user account
* Failed logins targeting disabled accounts
* Activity confirmed across several timestamps

User validation confirmed activity belonged to an internal **Red Team exercise**.

---

### Step 5: Response Action

To reduce analyst fatigue during testing:

* Created **Automation Rule**
* Allow-listed Red Team IP
* Set rule expiration (48 hours)

---

### Step 6: Incident Closure

Incident classified as:

✅ **Benign – Authorized Security Testing**

Status updated:
Active → Closed

---

## 🧩 Scenario 2 — Solorigate Network Beacon Investigation

### Incident

Detection of domain IOC related to **SolarWinds / Solorigate attack campaign**.

Domain identified:
avsvmcloud.com

---

### Step 1: Incident Ownership

* Assigned incident to analyst
* Reviewed DNS telemetry normalized via ASIM

---

### Step 2: Threat Hunting

Executed Sentinel Hunting Query:

**Solorigate Inventory Check**

Purpose:
Identify hosts containing malicious DLL indicators.

Results:

* 3 potentially affected endpoints discovered
* Evidence bookmarked for tracking

---

### Step 3: Evidence Correlation

* Added bookmarks to existing incident
* Expanded affected asset visibility
* Identified additional compromised hosts

---

### Step 4: Containment Recommendation

Recommended operational response:

* Endpoint isolation by Operations Team
* Further forensic investigation

(In production SOC environments this step may be automated via Playbooks.)

---

### Step 5: Threat Intelligence Integration

Added malicious IP to Sentinel **Threat Intelligence** store.

Configuration:

* Indicator Type: IP Address
* Validity Period: 60 days

Outcome:
Future detections automatically correlated across logs.

---

### Step 6: Incident Documentation & Handover

Documented:

* Investigation steps
* Hunting results
* Affected assets
* Recommended containment actions

Incident prepared for escalation to:

* Incident Response Team
* Digital Forensics Team

---

## SOC Skills Demonstrated

* Incident Triage & Ownership
* Log Analysis
* Threat Hunting
* IOC Management
* Security Automation
* Incident Documentation
* Cross-team Handover Procedures
* SIEM Investigation Workflow

---

## Key Learning Outcomes

This lab strengthened practical SOC analyst capabilities including:

* Structured incident investigation methodology
* Evidence-based decision making
* Use of enrichment and automation
* Realistic SOC operational workflow

---

## Conclusion

This project demonstrates hands-on experience performing end-to-end incident investigation using Microsoft Sentinel, closely reflecting enterprise SOC operations including detection validation, threat hunting, response coordination, and incident closure.
