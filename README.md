# Microsoft Sentinel SOC Investigation Lab

## Incident Management & Threat Hunting Case Study

---

## Project Overview

This project simulates the real-world workflow of a Security Operations Center (SOC) Analyst using Microsoft Sentinel to investigate, triage, enrich, and respond to security incidents.

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

## Tools and Technologies

* Microsoft Sentinel (SIEM)
* Log Analytics Workspace
* Kusto Query Language (KQL)
* Sentinel Workbooks
* Automation Rules and Playbooks
* Threat Intelligence Management
* Cisco Umbrella DNS Logs (ASIM normalized)

---

## Scenario 1 — Suspicious Sign-ins to Disabled Accounts

### Incident

Alert: Sign-ins from IPs attempting authentication to disabled accounts

---

### Step 1: Incident Triage

* Navigated to Microsoft Sentinel Incidents page
* Reviewed incident severity and associated entities
* Assigned incident ownership
* Updated status from New to Active

SOC Practice:

* Ensures investigation accountability
* Prevents duplicate analyst effort

![Incident Triage](screenshots/step1-incident-triage.png)

*Figure 1 — Reviewing incidents and assigning ownership in Microsoft Sentinel*

#### Analyst Thought Process

The initial objective was to determine whether the alert represented malicious activity or normal operational behaviour. Assigning ownership ensured responsibility for investigation, while updating the status to Active indicated that triage procedures had formally begun within the SOC workflow.

---

### Step 2: Log Investigation

* Accessed alert events through Log Analytics
* Reviewed authentication activity including:

  * Source IP address
  * Targeted user accounts
  * Login outcomes
  * Timestamp patterns

Observed repeated authentication attempts originating from an external IP address.

![Log Investigation](screenshots/step2-log-analysis.png)

*Figure 2 — Authentication log analysis performed in Log Analytics*

#### Analyst Thought Process

Repeated login attempts against disabled accounts may indicate password spraying or credential abuse attempts. Log analysis was performed to validate attack patterns and determine whether activity appeared automated or user-driven.

---

### Step 3: Incident Enrichment

Executed Sentinel playbook:

Get-GeoFromIpAndTagIncident

Actions performed:

* Retrieved geographic intelligence
* Tagged incident automatically
* Added contextual investigation data

Result: Suspicious IP traced to North Korea.

![Playbook Execution](screenshots/step3-playbook.png)

*Figure 3 — Geo-IP enrichment playbook execution*

#### Analyst Thought Process

IP enrichment provides contextual intelligence that assists in risk evaluation. Activity originating from an unexpected geographic region increased the initial threat assessment and justified further investigation.

---

### Step 4: Investigation Using Workbook

Used Investigation Insights Workbook to pivot analysis based on the suspicious IP address.

Findings:

* Multiple successful logins identified
* Failed authentication attempts against disabled accounts
* Activity correlated across several timestamps

User validation confirmed activity was part of an authorised internal Red Team exercise.

![Workbook Investigation](screenshots/step4-workbook.png)

*Figure 4 — Investigation Insights workbook analysis*

#### Analyst Thought Process

Workbook analysis enabled correlation across multiple data sources to determine whether broader compromise existed. Behaviour patterns aligned with controlled testing rather than adversarial activity.

---

### Step 5: Response Action

* Created automation rule
* Allow-listed authorised Red Team IP
* Configured rule expiration for 48 hours

![Automation Rule](screenshots/step5-automation-rule.png)

*Figure 5 — Automation rule configuration*

#### Analyst Thought Process

Since the activity was verified as authorised testing, automation was implemented to suppress repeated alerts. This reduces analyst workload while preserving detection capability after testing concludes.

---

### Step 6: Incident Closure

Incident classified as Benign – Authorised Security Testing.

Status updated from Active to Closed.

![Incident Closure](screenshots/step6-closure.png)

*Figure 6 — Incident closure in Microsoft Sentinel*

#### Analyst Thought Process

Proper incident closure ensures audit traceability and provides historical reference for similar alerts. Documentation confirms that investigation actions were completed and validated.

---

## Scenario 2 — Solorigate Network Beacon Investigation

### Incident

Detection of domain IOC associated with the SolarWinds Solorigate campaign.

Domain identified: avsvmcloud.com

---

### Step 1: Incident Ownership

* Assigned incident ownership
* Reviewed DNS telemetry normalized using ASIM

![Solorigate Incident](screenshots/step7-solorigate-incident.png)

*Figure 7 — Solorigate incident overview*

#### Analyst Thought Process

Given the association with a known supply-chain attack, the incident required immediate validation to determine potential organisational exposure.

---

### Step 2: Threat Hunting

Executed hunting query: Solorigate Inventory Check

Purpose:
Identify hosts containing malicious DLL indicators.

Results:

* Three potentially affected endpoints discovered
* Evidence bookmarked for investigation tracking

![Threat Hunting](screenshots/step8-hunting-query.png)

*Figure 8 — Threat hunting query results*

#### Analyst Thought Process

Threat hunting was conducted to determine whether compromise extended beyond the initially detected system and to assess the overall scope of impact.

---

### Step 3: Evidence Correlation

* Added bookmarks to incident
* Expanded affected asset visibility
* Identified additional impacted hosts

![Bookmarks](screenshots/step9-bookmarks.png)

*Figure 9 — Bookmarking investigation evidence*

#### Analyst Thought Process

Centralising investigation evidence improves visibility and supports coordinated containment decisions across affected systems.

---

### Step 4: Containment Recommendation

Recommended actions:

* Endpoint isolation
* Further forensic investigation

![Affected Hosts](screenshots/step10-entities.png)

*Figure 10 — Identified affected endpoints*

#### Analyst Thought Process

Indicators suggested potential host compromise. Isolation was recommended to prevent lateral movement or command-and-control communication while forensic analysis proceeds.

---

### Step 5: Threat Intelligence Integration

Added malicious IP address to Sentinel Threat Intelligence repository.

Configuration:

* Indicator Type: IP Address
* Validity Period: 60 days

![Threat Intelligence](screenshots/step11-threat-intel.png)

*Figure 11 — IOC added to Threat Intelligence store*

#### Analyst Thought Process

Adding indicators to Threat Intelligence enables automatic correlation with future telemetry, strengthening detection capability across the environment.

---

### Step 6: Incident Documentation and Handover

Documented:

* Investigation steps
* Hunting outcomes
* Affected assets
* Recommended response actions

Incident prepared for escalation to Incident Response or Digital Forensics teams.

![Incident Documentation](screenshots/step12-comments.png)

*Figure 12 — Investigation documentation and handover notes*

#### Analyst Thought Process

Thorough documentation ensures continuity when incidents transition between SOC tiers or specialised response teams.

---

## SOC Skills Demonstrated

* Incident triage and ownership
* Log analysis
* Threat hunting
* IOC management
* Security automation
* Incident documentation
* Cross-team handover procedures
* SIEM investigation workflow

---

## Key Learning Outcomes

This lab strengthened practical SOC analyst capabilities including structured investigation methodology, evidence-based decision making, enrichment usage, and realistic SOC operational workflow.

---

## Conclusion

This project demonstrates hands-on experience performing end-to-end incident investigation using Microsoft Sentinel, reflecting enterprise SOC operations including detection validation, threat hunting, response coordination, and incident closure.
