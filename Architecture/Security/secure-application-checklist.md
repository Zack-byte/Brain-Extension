# Secure Application Checklist
These Notes original from checklist provided at a Microsoft Application Security Challenge done at DoS.

## Acronyms, Terms, and Abbreviations
| Term | Definition |
|---|---|
| CQRS | Command and Query Responsibility Segregation |
| DDoS | Distributed Denial of Service |
| DR | Disaster Recovery |
| IAM | Identity and Access Management |
| MVC | Model-View-Controller |
| MVVM | Model-View-ViewModel |
| PIM | Privileged Identity Management |
| RBAC | Role-Based Access Control |
| SAS | Shared Access Signature |
| SIEM | Security Information Event and Management |
| SOLID | Single Responsibility Principle, Open/Closed Principle, Liskov's Substitution Principle, Interface Segregation Principle, and Dependency Inversion Principle |
| TIC | Trusted Internet Connections |

## Introduction
This paper serves as an addendum to the Great State App Security Training and is intended as a resource that application teams can use to ensure that they have considered nearly all of the things they should when designing and building an application to ensure it is as secure as possible without negatively impacting usability.  The checklist sections are provided in the order that they should be considered, but not necessarily in the order that they would be implemented. Note: The security of the development environment itself is not included in this document, as it is outside the scope of the training and in many cases not something an individual development team would be responsible for.  Any development environment should be maximally secure but not to the point that it inhibits the developers' ability to freely develop their application(s).  The security of centrally managed shared infrastructure including Azure Active Directory, global admin accounts, organizational policies, shared networking, SIEM, and other solutions are outside the scope of this document but are also very important to consider by those central teams

## Overview
Areas that should be considered when designing and building a secure application can be broadly summarized as follows:
- Project Security:
  - Security/Permissions
  - Approval flows 
- Repository:
  - Nothing sensitive hard-coded or stored insecurely
  - Branch policies and pull request approvals
- Secure coding practices
- Avoidance of unnecessary redundancy and complexity
- Consideration for how humans react to things
- Pipeline Configuration
  - Change reviews/approvals
  - Secure handling of secrets via key vault
- Infrastructure Configuration
  - Encryption at rest and in transit
  - Minimized access to modify resources
  - Key rotations
- Data protection
  - Backups and redundancy
  - Disaster Recovery
  - Exfiltration detection/prevention
  - Attack detection/prevention
- Identity Management

## Project Setup, Planning, and Architecture
| :heavy_check_mark: | Activity | Examples/Considerations |
|---|---|---|
|  |  Project: Azure DevOps Project secured | - Only team lead (TL) or designated alternate (DA) are admins. - Only TL/DA can create service connections (or delegated to a trusted external group). |
| | Project: Repository secured | - Git commit comments standardized by team - Git commit email patterns enforced in project. - Only TL/DA can modify the main branch policy. - Team has agreed and adheres to a specific branching strategy. |
| | Project: Pipelines secured | - Backlog includes items to implement code scanning, regression testing, integration testing, unit testing, and load testing prior to initial production deployment. - Backlog includes items to implement backup/recovery and disaster recovery (DR) mechanisms prior to inital production deployment. |
| | Architecture: HA/DR included | - Consider scenario where primary region is suddenly and permanantly unavailable. - Decide on hot, warm, or cold DR configuration. - Consider regional capabilities. Not all services are available in all regions. |
| | Architecture: Backups included | - Backup architecture/strategy for data. - Backup architecture/strategy for infastructure (this is "baked in" if code-based deployments are used). |
| | Architecture: Testing included | - Backlog items created for various tests: unit, integration, regression, load.|
| | Architecture: Zero trust and TIC 3.0 principles included | - App does not rely on network controls exclusively to ensure security - Robust identity controls in place - Encryption in transit and at rest are both used - Applications logically separated from other applications. |
| | Architecture: Adheres to organizational and legal requirements | - Security implemented in the application's architecture is appropriate to the sensitivity of the data and legal requirements.|
| | Architecture: Subscription and resource groups restricted to minimize access | - Application resource groups restricted in what can be deployed and how through a combination of provider registrations, Azure RBAC (IAM), and Azure Policy. - Review RBAC inheritance from higher levels, and work with appropriate group(s) to eliminate access by those who do not truly require it.|
| | Architecture: Identity controls implemented | - Strong MFA required, especially for accounts with access to modify permission or access to sensitive data. - (PIM) Privileged Identity Management used to allow human intervention in production only when approved by a manager and restricted to a limited time window. - Conditional Access Policies used to ensure human intervention in production only comes from trusted locations. - Service principal is the only identity allowed to deploy, modify, or delete application infrastructure. - Application does not use the same service principal in order to run or access application-level data. - Data tier access is restricted to the application and its users. - Managed identities used where possible. |
| | Architecture: Monitoring controls implemented | - Alerting items identified and alerts limited to immediately actionable items to avoid alert fatigue. - Application and resources send logs to Log Analytics workspace. - Application (if web-based) is backed with Application Insights. - Defender for Cloud, Azure Sentinel, and DDoS Protection implemented. |
| | Architecture: Unnecessary Complexity avoided | - Harder to identify and fix vulnerabilities. |
| | Architecture: Unnecessary redundancy avoided | - Duplicate layers increate the risk of outage |

**Industry standard for good Git commit comments include:**
- The subject starts with a capital letter.
- The subject is writtern in the imperative (e.g "Remove extra disk from the VM").
- The subject is limited to 50 characters with no trailing punctuation.
- The body is separated form the subject with a blank line.
- The body is limited to 72 characters per line.
- The body explains what, why , and how.

It is recommended a dev branch be used for the dev release stage, and the main branch be used for the test, staging, and production release stages. The team should also consider the use of a "squash merge" when merging from personal or temporary branches to shared ones, such as dev or feature branch.

Network controls should be used where appropriate, but compromise should not be possible by simply overcoming network controls, and no connections should be trusted based solely on which network they come from.

Strong MFA comes in several forms, with the strongest including an authenticator application or token with a rotating code. The existence of SIM hijacking means that text-based (SMS) MFA mechanisms and call-based mechanisms without PINs are not nearly as secure and should be avoided when superior means are available.

### Repository and Pipelines
| :heavy_check_mark: | Activity | Examples |
| --- | --- | --- |
| | Repository: Pull requests tied to work items | Pull requests (merges) from dev to main should be tied to work items. |
| | Repository/Pipeline: Secrets stored and handled securely | - No secrets stored in pipeline variables. - No secrets stored in code base ever. Git commit history is "forever". - Secrets should be pulled from Key Vault during pipeline's run; or generated with maximal length and complexity on the fly. |
| | Repository/Pipeline: Three-person integrity for a chnage to make it into production | - Combination of: 1. Pull request approval (technical peer reviews and approves change), and... 2. Pre-deployment approval by TL/DA on production stage. |
| | Build Pipeline: Code scanning implemented | - Template scans - Code scans |
| | Build and Release Pipelines: Tests implemented prior to inital production deployments | - Preferably automated and includes: Unit, Integration, Regression, Load |
| | Release Pipeline: Prod deployment stage requires TL/DA approval | - Release pipelines configured so only team lead or alternate can approve production stage of the deployment or modify who can modify pre-stage deployment conditions. |
| | Release Pipeline: Pipeline variables minimized | - Should only contain bare minimum required, such as target resource groups for a given deployment stage and the service connection name. - All other pipeline variables should be stored in a JSON file in the project's repository and read in as the first step of a pipeline's run. |
| | Release Pipeline: Region-agnostic pipelines | - Pipelines configured to be region-agnostic or easily switched over to a different region. |
| | Release Pipeline: Invariable artifacts used for all stages | - All stages deployed from exact same set of artifacts. The only things that should change are the values that need to, such as URI, tenant ID, subscription ID, resource group, secrets, etc. |
| | Release Pipeline: Use of service principal | - Only a service principal has rights to modify app infrastructure in production--not users. - Service connection used to hold identity and secret of service principal used to deploy application resources. |

**Three person integrity can be accomplished with the following:**
- One person initiates pull request from the Dev branch to the main branch.
- A second person, prefereably a peer developer, is required to review and approve the pull request.
- The release pipelin is configured so that only the Main branch code can be deployed to the Test, then Staging, then Prod stages.
- Prod stage is configured with a pre-deployment approval requirement for team lead or designated alternate.

### Infrastructure Configuration and deployment
| :heavy_check_mark: | Activity | Examples |
| --- | --- | --- |
| | Infrastructure: Traffic encrypted in transit | - HTTPS with TLS 1.2|
| | Infrastructure: Traffic encrypted at rest | - Default in Azure. - Additional layer of encryption should be considered, depending on sensitivity of application data. - Azure disk encryption using key vault for VMs. - Column encryption for SQL. |
| | Infrastructure: Automated key rotations | - Key vault and storage account configured to automatically rotate storage account keys. |
| | Infrastructure: Scaling appropriate to application | - Horizontal and/or vertical scaling is sized and configured appropriately for likely applicatin usage |
| | Infrastructure: PaaS firewall rules used where they make sense | - Subnet rules with service endpoints. - IP-based rules |
| | Infrastructure: Secure networking used where it makes sense | - Service endpoints (to restrict inbound for storage, key vault, SQL, etc.) - Private endpoints (where service endpoints are insufficient) - VNet integration (outbound traffic for App Servies) - Network security group - Route table (if appliances used for outbound traffic) |
| | Infrastructure: Web Application Firewall font-ends web applications | - App Gateway w/ WAF in "Prevent" mode implemented for web applications|
| | Infrastructure: Data exfiltration risk minimized | - Azure Firewall used for outbound traffic to reduce risk of data exfiltration and filter outbound traffic by URI. - Dynamic data masking and advanced auditing for SQL. |
| | Infrastructure: Load balancing supports availability | - Azure front door, Azure load balancer, or Azure application gateway. - Implemented to improve availability and allow an application to function while front end or back end components are replaced. |
| | Deployment: Dead code eliminated | - Dead code identified and removed from deployment scripts. |
| | Deployment: Input validation implemented | - Parameters for ARM templates and scripts have input validation (length, type, allowed characters, etc.)|
| | Deployment: Secrets stored and handled securely (passwords, keys, SAS tokens, certificates, credentials, etc.) | - No secrets hard coded in code base (templates, scripts, application code, etc.) or stored in pipeline variables. - Secrets retrieved from key vault or dynamically generated. - Secrets passed securely as securestrings to ARM templates and scripts. - Variables holding secrets are cleared as soon as the secret is no longer needed. - Pipeline secrets are stored separately (in a different key vault) from applcation secrets. - Automation is implemented to rotate secrets. |
| | Deployment: Resource Tagging implemented | - Resource tagging for POC and Office, to allow central authorities to quickly identify and contact the owner of an application if an attack or other major issue is detected. |

### Application
| :heavy_check_mark: | Activity | Examples |
| --- | --- | --- |
| | Dead code removed | - Code blocks not referenced elsewhere. |
| | Input validation implemented | - Length, value type, max and min values, rounding, decimal length, etc. |
| | Connection leaks eliminated | - Connections terminated when not needed. |
| | Memory leaks eliminated | - Memory released when not needed |
| | SOLID principles followed | - Single Responsibility Principle - Open/Closed Principle - Liskov Sub Principle - Interface Segregation Principle - Dependency Inversion Principle. |
| | Application team has agreed upon a coding style | - Varable name standards, code block delimiter standards, etc. |
| | Team has settled on an architectural style | - CQRS, MVC, MVVM, etc. |
| | Unnecessary complexity avoided | |
| | Unnecessary redundancy avoided | | 


### Questions to Ask Yourself
1. What if my primary region goes down for a long period of time? 

2. What if connectivity to my primary region goes down? 

3. What if some users lose connectivity to my primary region, but not others?

4. What if a user is secretly working for an adversary? 

5. How are my secret values being stored and accessed? 

6. How much new data can I tolerate losing? 

7. How quickly much my application be recovered following an outage? 

8. What happens if an attacker modifies my data? 

9.  What’s the damage if an attacker exfiltrates my data? 

10. Does this mitigation address a higher priority risk than another mitigation? 

11. What specific risk or vulnerability am I addressing with this mitigation?


### Resources

[Get started guide for Azure developers](https://docs.microsoft.com/en-us/azure/guides/developer/azure-developer-guide)

[Azure Resource Manager overview](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)

[Azure Application Architecture Guide](https://docs.microsoft.com/en-us/azure/architecture/guide)

[Azure Reference Architectures](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures)

[Azure Resource Manager template best practices](https://docs.microsoft.com/en-us/azure/azure-resource-manager/template-best-practices)

[App Service Documentation 1](https://docs.microsoft.com/en-us/azure/app-service)

[App Service Documentation 2](https://docs.microsoft.com/en-us/azure/app-service/overview-compare)

[App Service Documentation 3](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-auth-aad)

[Azure DevOps Server Documentation](https://docs.microsoft.com/en-us/azure/devops/server)

[Dangers of Violating SOLID Principles in C#](https://docs.microsoft.com/en-us/archive/msdn-magazine/2014/may/csharp-best-practices-dangers-of-violating-solid-principles-in-csharp)






