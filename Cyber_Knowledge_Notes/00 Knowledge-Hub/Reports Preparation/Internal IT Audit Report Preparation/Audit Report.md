## 01. Cover Page 
- Client Organization Name
- Name of Report "Internal IT Audit Report - Draft"
- Date of Report Release

## 02. Executive Summary
### 2.1 Introduction
This Internal IT Audit Report presents the observations, findings, and assessment outcomes identified during the review of information, documentation, and evidentiary artifacts provided by the {ORGANIZATION_NAME}. The audit was conducted by {AUDITOR}, following its appointment by {ORGANIZATION_NAME}, to perform an independent and objective assessment of the Authority’s information technology and cybersecurity environment.

The audit was initiated to obtain a clear and reliable understanding of the **current state of IT governance, cybersecurity posture, and operational effectiveness**, and to identify areas where control weaknesses, inconsistencies, or inefficiencies may expose {ORGANIZATION_NAME} to operational, regulatory, or cyber-related risks. In an increasingly complex threat landscape and evolving regulatory environment, the audit serves as a key assurance mechanism to support management in strengthening IT and cybersecurity capabilities and ensuring alignment with organization’s strategic objectives and stakeholder expectations.

### 2.2 Audit Objectives
The primary objective of this Internal IT Audit was to evaluate the **adequacy, design, and operating effectiveness** of {ORGANIZATION_NAME}’s IT and cybersecurity controls, with a focus on risk management, governance, and operational resilience. The audit aimed to assess whether established controls are appropriately designed, consistently implemented, and operating effectively to mitigate current and emerging IT and cyber risks.
Specifically, the audit objectives included:
- Assessing the effectiveness of IT and cybersecurity governance structures, policies, procedures, and oversight mechanisms.
- Evaluating the maturity of risk management practices, including the identification, assessment, treatment, and monitoring of cybersecurity and IT-related risks.
- Reviewing key operational and technical controls implemented to protect information assets, systems, and infrastructure against unauthorized access, data breaches, service disruptions, and cyber threats.
- Identifying control gaps, weaknesses, and areas for improvement that may impact confidentiality, integrity, availability, and resilience of IT and Cybersecurity services.
- Providing practical and risk-based recommendations to enhance {ORGANIZATION_NAME}’s IT operations, cybersecurity posture, and alignment with business objectives, regulatory requirements, and the expectations of internal and external stakeholders.
Through these objectives, the audit supports management in strengthening control effectiveness, improving decision-making, and proactively managing current and future risks.

### 2.3 Audit Scope
The scope of the Internal IT Audit encompassed a comprehensive review of {ORGANIZATION_NAME}’s IT and Cybersecurity Governance, Risk Management, and operational control environment, covering both strategic and technical domains. The audit focused on controls relevant to managing current and emerging IT and cyber risks, and their alignment with business needs and regulatory expectations.
In scope areas included, but were not limited to:
- **IT and Cybersecurity Governance**, including governance frameworks, roles and responsibilities, policies, procedures, standards, and oversight mechanisms. 
- **Risk Management**, including risk assessment methodologies, risk registers, risk treatment plans, and consideration of current and future cybersecurity threats.
- **Identity and Access Management**, including user provisioning and de-provisioning, privileged access, segregation of duties, authentication mechanisms, and access reviews.
- **IT Operations and Infrastructure Security**, including network security, endpoint protection, secure configuration, patch management, logging and monitoring.
- **Vulnerability and Threat Management**, including vulnerability assessments, penetration testing, incident management, and security monitoring capabilities.
- **Data Protection and Resilience**, including data classification, backup and recovery, cryptography, and business continuity and disaster recovery arrangements.
- **Application and Change Management**, including secure system development practices, configuration change control, and project cybersecurity requirements.
- **Third-Party and Vendor Management**, including assessment of vendor risks, contract and SLA management, and oversight of outsourced services.
- **Physical and Environmental Security**, including controls over access to critical IT facilities and infrastructure.
The audit scope was designed to provide reasonable assurance over the effectiveness of controls supporting SCA’s IT operations and cybersecurity posture, while identifying risks that may affect the Authority’s ability to achieve its objectives both now and in the future.

## 03. Summary of Findings

> use the Findings Library to get an idea of Findings and each finding Risk Rating.
## 04. Internal Audit Opinion
#### Four Tier Internal Audit Opinion Guideline – Institute of Internal Auditors (IIA)
![[Pasted image 20260114120725.png]]

| Opinion Rating           | Definition                                                                                                                                                                                                              |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Effective                | Controls evaluated are adequate, appropriate, and effective to provide reasonable assurance that risks are being managed and objectives should be met.                                                                  |
| Some Improvement Needed  | A few specific control weaknesses were noted; generally however, controls evaluated are adequate, appropriate, and effective to provide reasonable assurance that risks are being managed and objectives should be met. |
| Major Improvement Needed | Numerous specific control weaknesses were noted. Controls evaluated are unlikely to provide reasonable assurance that risks are being managed and objectives should be met.                                             |
| Unsatisfactory           | Controls evaluated are not adequate, appropriate, or effective to provide reasonable assurance that risks are being managed and objectives should be met.                                                               |
## 05. Definition of Risk Rating
Each finding/ issue arising during our engagement has been assigned a rating, using the definitions provided below. These ratings address the significance of the risk and the likelihood that it could occur in the business environment, as well as the urgency of implementation. This should be taken as a reference to the management and used as a tool to determine the level of attention and effort that should be given to each observation and recommendation provided in this report.

| Risk   | Definition                                                                                                                                                                                                                                                                                                                       | Action Required                                                                                                                                                                                  |
| :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| High   | Issue represents a control weakness, which could cause or is causing major adverse effect on the daily ability to achieve process objectives.                                                                                                                                                                                    | Urgent treatment required; and<br><br>A detailed plan of action to be approved by Management with resolution within no later than 90 days.                                                       |
| Medium | A weakness in control which, although not fundamental, relates to shortcomings that expose individual business systems to a less immediate level of threatening risk or poor value for money. Such a risk could impact operational objectives and should be of concern to senior management and requires prompt specific action. | Treatment required;<br><br>Action within a reasonable time period; and<br><br>Timeframe for action is subject to competing priorities and cost benefit analysis, but should not exceed 6 months. |
| Low    | Areas that individually have no significant impact, but where management would benefit from improved controls and/or have the opportunity to achieve greater effectiveness and/or efficiency.                                                                                                                                    | No urgent treatment required:<br><br>Issue should be managed within a reasonable time                                                                                                            |


![[Pasted image 20260114122835.png]]

## 06. Internal Audit Methodology 
![[Pasted image 20260114123510.png]]
We developed our internal audit approach In accordance with the professional standards of internal auditing. Our methodology includes the following:
#### Engagement Planning:
- Develop a broad understanding of the auditable entity (business Processes, Supported IT Infrastructure, IT Applications, and legislative considerations).
- Develop engagement scope of work and objectives.
- Agree on engagement scope and objectives with the client.

#### Understanding, and Assessment of Risk & Control:
- Develop a detailed understanding of the auditable entity/area as defined in the scope.
- Identify the risks and controls in the auditable entity/area.
- Perform a walkthrough, and assess internal control design effectiveness.

#### Testing:
- Evaluate controls through detailed testing using appropriate testing methods.
- Assess the outcome of the testing and identify any control gaps or weaknesses.
- Provide recommendations for improving the controls.

#### Reporting:
- Issue draft internal audit report to relevant area/department manager, documenting work performed and recommendations for management comment.
- Obtain management responses and action plans to recommendations, in addition to estimated implementation dates and issue final report.
- Track the implementation of audit recommendations.

## 07. Detailed Observations
###### Observation 1: 
- Absence of Time Synchronization Controls.

###### Findings:
- During the audit, it was observed that time synchronization controls were not implemented or configured on critical systems, which may lead to inaccurate timestamps, affecting log integrity, event correlation, and forensic analysis.
###### Root Cause
- Lack of configured and continuous monitoring of time synchronization across all SCA Servers and Systems.
###### Risk
- Unsynchronized systems cause inaccurate logs, complicating forensic investigations and compliance.
###### Impact:
- Causes inaccurate logs, obstructing forensic analysis, incident timelines, and compliance.
###### Recommendation:
- It is recommended that SCA should maintain comprehensive logs of device up and down times to ensure effective clock synchronization controls.
- It is recommended that SCA should configure correct and updated time by utilizing NTP servers provided by KSA; (for eg, sa.pool.ntp.org, as mentioned in the NCA ECC Standard)

###### Division’s Response:

###### Responsible Owner/ Entity:

###### Implementation Timing:
this section will be filled and agreed on by after the meeting and discussion with client's management.