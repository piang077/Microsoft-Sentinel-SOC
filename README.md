# Microsoft Sentinel Incident Management Lab

## SOC Investigation Case Study

---

## Overview

This lab simulates the daily workflow of a Security Operations Center (SOC) Analyst using Microsoft Sentinel incident management capabilities.

The exercise focuses on how analysts review incidents, investigate alerts, enrich evidence, perform threat hunting, and prepare incidents for response or handover.

Estimated completion time: 60 minutes
Level: Intermediate (Level 300)

---

## Prerequisites

This lab assumes that Sentinel data connectors, analytics rules, and sample datasets were already deployed in a previous lab.

---

# Exercise 1 — Reviewing Microsoft Sentinel Incident Tools

## Task: Accessing the Incident Queue

### Action Performed

* Opened Microsoft Sentinel workspace
* Navigated to the **Incidents** page
* Reviewed incidents generated within the default 24-hour window

Analysts used filtering options to:

* Modify investigation time range
* View incidents by severity
* Include Closed, Active, or New incidents

### Purpose

The Incidents page acts as the primary working queue for SOC analysts. Filtering helps analysts prioritise alerts based on urgency and investigation scope.

---

## Task: Reviewing Incident Details

### Action Performed

* Located incident titled
  **“Sign-ins from IPs that attempt sign-ins to disabled accounts”**
* Opened incident preview panel
* Reviewed surfaced entities and alert summary

### Purpose

Initial review provides high-level understanding of:

* affected users
* source IP addresses
* detection reason

This allows analysts to quickly assess potential risk before deeper investigation.

---

## Task: Incident Ownership Assignment

### Action Performed

* Changed Owner from **Unassigned** to **Assign to me**
* Updated incident Status from **New** to **Active**

### Purpose

Assigning ownership ensures accountability and prevents multiple analysts from duplicating investigation work. Changing status to Active confirms investigation has officially started.

---

## Task: Reviewing SOC Operational Metrics

### Action Performed

Opened **Security Operations Efficiency Workbook** through:

* Incident action bar, or
* Direct link within the incident view

Reviewed:

* Incident statistics
* Investigation lifecycle metrics
* SOC performance overview

### Purpose

The workbook provides visibility into overall SOC health, including investigation workload and response efficiency. Analysts use this information to understand operational trends and incident handling performance.

---

# Exercise 2 — Handling Incident: Suspicious Sign-ins to Disabled Accounts

---

## Task 1: Initial Incident Investigation

### Action Performed

* Opened incident from Incidents dashboard
* Reviewed entities displayed in preview pane
* Confirmed ownership and Active status
* Selected **View full details**

### Purpose

Full incident view allows analysts to access alerts, timelines, and investigation evidence required for validation.

---

## Task 2: Reviewing Raw Alert Events

### Action Performed

* Expanded alerts within Incident Timeline
* Opened **Link to Log Analytics**
* Examined authentication event data

Reviewed fields included:

* Source IP address
* Target accounts
* Authentication results
* Event timestamps

### Purpose

Raw log analysis helps determine whether activity matches known attack techniques such as password spraying or unauthorized access attempts.

---

## Task 3: Incident Enrichment Using Playbook

### Action Performed

* Executed playbook:
  **Get-GeoFromIpAndTagIncident**
* Retrieved geographic intelligence
* Added tags and contextual data to incident

### Purpose

Enrichment adds external intelligence to investigation data. Geographic information assists analysts in determining whether login activity originates from expected locations.

---

## Task 4: Investigation Using Workbook

### Action Performed

* Opened **Investigation Insights Workbook**
* Verified subscription and workspace selection
* Switched investigation type to **Entity**
* Investigated IP address: 175.45.176.99

Workbook analysis revealed:

* Successful logins associated with user Adele
* Failed authentication attempts against disabled accounts

User validation confirmed activity belonged to an internal Red Team exercise.

### Purpose

Workbook investigation enables correlation across multiple log sources to determine whether behaviour represents compromise or authorised activity.

---

## Task 5: Creating Automation Rule

### Action Performed

* Created Incident Automation Rule
* Allow-listed Red Team IP address
* Configured expiration period of 48 hours

### Purpose

Automation rules reduce unnecessary alert generation during authorised testing activities while maintaining detection capability after testing ends.

---

## Task 6: Incident Closure

### Action Performed

* Updated incident status from Active to Closed
* Classified incident as **Benign**

### Purpose

Proper classification ensures accurate reporting, audit tracking, and prevents future re-investigation of validated authorised activity.

---

# Exercise 3 — Handling Incident: Solorigate Network Beacon

---

## Task 7: Incident Review and Ownership

### Action Performed

* Located **Solorigate Network Beacon** incident
* Assigned incident ownership
* Reviewed detection description

Domain IOC identified:
avsvmcloud.com

### Purpose

Incidents linked to known threat campaigns require immediate validation due to potential organisational exposure.

---

## Task 8: Reviewing Detection Source

### Action Performed

* Inspected alert timeline
* Opened raw logs via Log Analytics
* Confirmed events originated from Cisco Umbrella DNS logs normalized using ASIM

### Purpose

Understanding telemetry source helps analysts validate detection reliability and understand how data was normalized across security tools.

---

## Task 9: Threat Hunting for Additional Evidence

### Action Performed

* Opened Hunting blade
* Executed query: **Solorigate Inventory Check**
* Viewed query results

Results identified three potentially affected endpoints.

### Purpose

Threat hunting expands investigation scope beyond the original alert to identify additional compromised systems.

---

## Task 10: Evidence Bookmarking and Correlation

### Action Performed

* Bookmarked identified hosts
* Added bookmarks to existing Solorigate incident

### Purpose

Centralising evidence within a single incident improves visibility and supports coordinated response planning.

---

## Task 11: Containment Recommendation

### Action Performed

Recommended isolation of affected hosts by Operations team.

### Purpose

Host isolation prevents possible attacker communication, lateral movement, or persistence while further investigation occurs.

---

## Task 12: Adding Indicator to Threat Intelligence

### Action Performed

* Copied malicious IP address from incident
* Added new indicator in Sentinel Threat Intelligence
* Configured validity period of two months

### Purpose

Adding Indicators of Compromise enables automatic detection correlation if the threat reappears within organisational telemetry.

---

## Task 13: Incident Documentation and Handover

### Action Performed

* Documented investigation activities in Incident Comments
* Prepared incident for transfer to Operations or Forensics teams
* Shared incident link or reassigned ownership

### Purpose

Clear documentation ensures investigation continuity and enables downstream teams to proceed with response or forensic analysis efficiently.

---

## Skills Demonstrated

* Incident triage and ownership
* Log investigation
* Incident enrichment
* Threat hunting
* Evidence correlation
* Automation rule configuration
* Threat intelligence management
* Incident documentation and handover

---

## Conclusion

This case study demonstrates practical SOC analyst experience using Microsoft Sentinel to manage incidents from initial detection through investigation, validation, response recommendation, and operational handover. The workflow reflects real enterprise SOC investigation procedures and incident lifecycle management.
