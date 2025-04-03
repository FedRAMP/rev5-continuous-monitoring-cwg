# Continuous Monitoring Monthly "1 Page Report" Template

## Table of Contents
- [Overview](#overview)
- [Project Details](#project-details)
   - [Directory Structure](#directory-structure)
   - [File Naming Conventions](#file-naming-conventions)
- [How to Generate KSIs from System-Generated Data](#how-to-generate-ksis-from-system-generated-data)
   - [Inventory Data](#inventory-data)
   - [Configuration Data](#configuration-data)
   - [Vulnerability Scan Data](#vulnerability-scan-data)
   - [Plan Of Action and Milestones and Deviation Data](#plan-of-action-and-milestones-and-deviation-data)
- [Report Details](#report-details)
   - [Overall Risk Score](#overall-risk-score)
   - [KSI 1: Inventory Visibility Coverage Rate](#ksi-1-inventory-visibility-coverage-rate)
      - [6 Month Inventory Trending Graph](#6-month-inventory-trending-graph)
   - [KSI 2: Mean Time To Remediate Vulnerabilities](#ksi-2-mean-time-to-remediate-vulnerabilities)
      - [6 Month Vulnerability Trending](#6-month-vulnerability-trending-graph)
   - [KSI 3: Percent Late CISA Kev Findings](#ksi-3-percent-late-cisa-kev-findings)
   - [KSI 4: Secure Configuration Rate](#ksi-4-secure-configuration-rate)
   - [KSI 5: Mean Time To Investigate Alerts](#ksi-5-mean-time-to-investigate-alerts)
   - [KSI 6: Privileged Access Compliance Rate](#ksi-6-privileged-access-compliance-rate)
   - [KSI 7: Cryptographic Module Compliance Rate](#ksi-7-cryptographic-module-compliance-rate)
   - [KSI 8: Agency Statutory Compliance Rate](#ksi-8-agency-statutory-compliance-support)
   - [New Services Added](#new-services)
- [Significant Changes](#significant-changes)


## Overview
FedRAMP authorized cloud service providers (CSPs) may use this report template as a concise yet thorough briefing document that aligns with FedRAMP continuous monitoring requirements. By highlighting eight key security metrics (KSIs) along with trending visualizations, the report enables agency stakeholders to quickly assess compliance status, identify security gaps, track remediation progress, and make risk-based decisions about the cloud service offerings (CSOs) they consume without requiring technical deep-dives into raw security data.
CSPs can leverage cloud-native or third-party security tools to automatically populate this markdown report template with KSIs derived from aggregate system-generated data, creating a powerful briefing tool for their Federal customers. The report consolidates CSO generated data from vulnerability scanners, inventory and configuration management tools, and compliance monitoring tools to provide agencies with data-driven, ongoing insight into their security posture.

## Project Details

### Directory Structure
The repository structure is reflected below:
```
reports/
├── markdown/
│   ├── monthly-report-template.md        # Monthly continuous monitoring report markdown template
│   └── sig-change-report-template.md     # Significant change report markdown template
├── images/
│   ├── graphs/                           # Place graph images here
│   └── assets/                           # Other images
└── output/                               # Generated reports (.PDF, .PNG, .HTML, etc.)
```

### File Naming Conventions
1. Markdown Files:
   - Include CSO name and ConMon report
   - Use lowercase
   - Use hyphens for spaces
   - Include date in YYYYMMDD format
   - Example: `awesomecloud-conmonreport-20240129.md`

2. Image Files:
   - Use descriptive names
   - Include figure numbers if referenced in text
   - Use lowercase
   - Use hyphens for spaces
   - Include date in YYYYMMDD format
   - Example: `unique-vulns-graph-20240129.png`

3. Output Files:
   - Will automatically include date stamp
   - Example: `awesomecloud-conmonreport-20240129.pdf`

## How to Generate KSIs from System-Generated Data
CSOs are responsible for generating and aggregating system data into quantified metrics that inform the KSIs. Below are the types of data that are required for creating the metrics.

### Inventory Data
Inventory entries reflect each component within the authorization boundary, encompassing the data plane, management plane, and control plane. Unique inventory items should be tracked by a unique identifier. This identifer may vary based on the technology component itself, but should remain static over time. Examples of a component identifier include:
- IP address
- Fully Qualified Domain Name (FQDN)
- Hostname
- Container Registry Image Type Tag (i.e., RHEL 9) 

### Configuration Data
Configuration data reflects the specific configurations of all inventory components deployed within the authorization boundary. Where available, DoD SRG STIGs should be employed as the configuration hardening baseline. The STIGs may be modified if necessary, STIG findings that are not applied should be treated as Operational Requirements (ORs).

### Vulnerability Scan Data
Vulnerability scans target inventory components deployed within the authorization boundary (or identical components in staging, registry, etc.). Scan targets should align with components listed in the inventory based on the unique static identifier. Unique vulnerabilities should be counted per scanner assigned detection identifiers (i.e., Tenable Plugin ID, Qualys QID, Wiz Security Issue, etc.) or by CVE/CWE found on one or more components on a specific date. Authenticated scanning for monthly continuous monitoring should consists of targeted scans rather than simply directing a scan tool at subnets. Scan results are also able validate the detection of newly introduced inventory technologies, identify open ports and protocols, identify cryptographic modules in use, and detect unsupported or end-of-life components.

### Plan of Action and Milestones and Deviation Data
Plan of Action and Milestones (POA&Ms) track late vulnerability findings as well as control deficiencies found during assessment (or self-reported), beginning at the original detection date. Deviations in risk (i.e., risk adjustments), false positives, operational requirements and vendor dependencies apply to individual POA&Ms. Wherever possible, automated risk triage should be applied to justify deviation requests. This may include:
- CVSS Temporal and Environmental Scores
- EPSS
- CISA VEX
- CISA Vulnrichment

## Report Details
The "report-template.md" provides the template that CSPs should use to report continuous monitoring status to their agency customers. The report should be generated and shared with agency customers at least every month. The report consists of 8 Key Security Indicators (KSIs) that reflect core cybersecurity practices, along with trending visualizations. Each KSI is described in detail below.

### Overall Risk Score
The Overall Risk Score is calculated by taking the average of all 8 KSIs, and grading the result. An "A" is 90%-100%, a "B" is 80%-90%, etc.

### KSI 1: Inventory Visibility Coverage Rate
The Inventory Visibility Coverage Rate is calculated by comparing the defined inventory to the scan targets. If there are unauthorized assets found (e.g., there are inventory items not targeted by scans, or scan targets not tracked as inventory components) then the percentage should reflect the difference. For containers, the image types defined in the inventory should be compared to image types for active runtime containers in production. 
Example:
- 3,241 components in inventory
- 10 unauthorized components
- Coverage calculation: 3,241 / (3,241 + 10) * 100 = 99.7%

#### 6 Month Inventory Trending Graph
This graph reflects the historical trending of the Inventory Visibility Coverage Rate over 6 months.

### KSI 2: Mean Time To Remediate Vulnerabilities
The Mean Time To Remediate Critical Vulnerabilities is the average time from discovery to remediation of vulnerabilities (adjusted for deviation if necessary). This should be broken out into Critical, High, Medium and Low. 

#### 6 Month Vulnerability Trending Graph
This graph reflects the historical trending of the mean time to remediate vulnerabilities over 6 months.

### KSI 3: Percent Late CISA KEV Findings
Binding Operational Directive (BOD) 22-01 requires agencies to prioritize and remediate KEV-listed vulnerabilities within prescribed timeframes. Leverage CISA KEV Catalog API to continuously recieve updated list of vulnerabilties that are known to be actively exploited by threat actors and consider automated vulnerability management tools to automatically/immediately address KEV catalog vulnerabilties (strongly recommended by CISA).
Example:
- 5 detected KEV findings
- 3 late KEV findings
- 5 / (5 + 3) * 100 = 62.5%

### KSI 4: Secure Configuration Rate
The Secure Configuration Rate is the percentage of unique component configurations that conform to hardening baselines (e.g., DISA STIG, CIS Benchmarks), accounting for approved deviations and measured through continuous automated assessment.
Example:
- 47 unique component configurations
- 4 unapproved configuration failures
- 47 / (47 + 4) * 100 = 92.1%

### KSI 5: Mean Time To Investigate Alerts
- Average time between security alert generation and analyst investigation, categorized by severity.

### KSI 6: Privileged Access Compliance Rate
Percentage of privileged user accounts and service accounts with multi-factor authentication enabled.

### KSI 7: Cryptographic Module Compliance Rate
Percentage of data encryption implementations using FIPS 140-2/3 cryptographic modules for data at rest and in transit, accounting for approved exceptions.

### KSI 8: Agency Statutory Compliance Support
Percentage representing CSO abliliy to support the following agency statutory requirements:
- IPv6 Support
- Customer configured FIPS 140-2/3 compliance
- Section 508 compliance
- Customer accessible security logging
- Customer configured data retention

Example:
- Total possible score: 5.0
- If offering supports 3/5, percentage would be 60%.

### Services In Scope
This section lists all customer-facing services added to the authorized cloud service offering.

## Significant  Changes
Modern cloud environments often introduce dozens or even hundreds of changes per day. Only changes that are significant must be reported to agency customers. Below is general guidance for determining whether a change is considered significant:
1. Standard patching, maintenance, disposal, and personnel changes for the system

Standard patching and maintenance is considered part of the system software development lifecycle (SDLC) and therefore changes of this type are not considered significant.

2. Responding to Government priorities such as OMB Memos, DHS Binding Operational Directives (BODs), or NIST revisions to SP 800-53

These types of changes typically are associated with prescribed actions and timeframes for implementation that are situational. If warranted, these types of changes should be tracked as POA&Ms but are usually not considered significant unless the CSP is instructed to do so as part of the specific guidance.

3. Introducing new technologies, product features and services, processes, or customer requirements

These types of changes are generally considered significant, especially if they modify existing inventory component configurations or add new technology components into the authorization boundary. For these changes, a completed significant change form (the "sig-change-report-template.md") must be delivered to agency customers.

The following steps provide an example change control process that CSPs may apply to generate the KSIs required in the template:

**Pre-Deployment**
1. Determine whether the change is standard or significant (for example, by comparing the change to the list of example significant changes in NIST SP 800-37 and 800-128). This step may be automated based on data submitted in a ticket for the change request.
2. Determine the type of significant change (i.e. new service, SaaS interconnection, etc). 
3. Determine appropriate testing methodology. Most of the time, this will be implemented via automated DevSecOps.
4. Conduct a Security Impact Analysis (SIA) that includes test results.

**Post-Deployment**
1. Perform production testing and validation of the new components (i.e., vulnerability and configuration scans).
2. Track any POA&Ms associated with the change
3. Ensure customer responsibilities are documented for the new feature or service. There must be a clear path for customers to opt-in of changes if they do wish to accept the risk.

When new changes are introduced, the following additional information should also be incorporated into the monthly report:
### New Service Details

#### Service Name: [New-Service]
This should be the service as it is branded for opt-in customer use.

#### Service ID: [Service-ID]
This should be a unique identifier of the significant change for tracking the applicable change across name changes or consolidation of multiple services.

#### Overview of Significant Change
This should be a brief description of what the service does.

#### Implementation Timeline: [Timeline]
Dates for implementation of the change.

#### Security Impact Analysis
##### Tests In Scope: [Tests]
List of tests performed (i.e., SAST and SCA, vulnerability scans in a staging environment, etc.)

##### Security Tests Status: [Pass-Fail]
Results of the tests in scope that demonstrate adequate security outcomes

#### If PII Introduced:
- PIA Status: [Yes/No/NA]

#If Major Architecture Change:
- Penetration Test: [Yes/No/NA]
- Red Team Exercise: [Yes/No/NA]
- Supply Chain Risk Analysis: [Yes/No/NA]
- Open POA&Ms Related To Change: [Open-POAMs]

#### Customer Responsibilities:
Description of any customer responsibilities associated with the change

Additionally, all in scope customer-facing services must be listed on the regular monthly continuous monitoring report in the appropriate section.