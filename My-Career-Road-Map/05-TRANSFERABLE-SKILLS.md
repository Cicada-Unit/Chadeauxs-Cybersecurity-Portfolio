## Practical Technical Experience — Homelab Design, Deployment, and Administration

### Overview

My homelab serves as a practical environment for learning infrastructure administration, networking, containerized services, storage management, access control, service monitoring, and self-hosted application deployment.

Rather than relying exclusively on coursework or isolated exercises, I have designed and assembled a small, multi-node environment that supports services used by my household. This creates opportunities to work with real configuration decisions, interconnected services, operational dependencies, troubleshooting, and ongoing maintenance.

The environment combines a custom 10-inch network rack, a managed network switch, multiple Raspberry Pi systems, Docker-based applications, and a separate laptop used as the main administrative workstation.

The goal is not simply to run individual applications. It is to build an organized environment in which services work together, users have appropriate access, and the infrastructure remains understandable and maintainable.

### 1. Infrastructure Design and Network Organization

I designed a compact infrastructure layout centered around a custom 10-inch rack and a managed network switch. The network distributes connectivity and, where supported, Power over Ethernet (PoE) to connected devices. An additional unmanaged switch extends connectivity for part of the environment, while the higher-power NAS uses a separate power arrangement.

This setup has provided practical exposure to:

- Physical infrastructure planning and cable organization.
- Network-device interconnection and topology.
- Managed versus unmanaged switching.
- Power requirements and PoE considerations.
- Separating administrative access from ordinary service use.
- Understanding how physical connectivity affects service availability.

Building a physical environment reinforces that infrastructure is more than software configuration. Power, cabling, network links, device placement, and hardware limitations all influence reliability.

### 2. Multi-Node Raspberry Pi Environment

The homelab uses three Raspberry Pi nodes with distinct responsibilities.

#### Node 1 — Raspberry Pi 5: Storage and Media Services

This node provides network-attached storage and related household services.

The configuration includes:

- OpenMediaVault for storage administration.
- A RAID 6 storage arrangement.
- Samba/SMB network file sharing.
- Individual user accounts and access separation for household members.
- A container-based image backup service for family device backups.
- Jellyfin for self-hosted media streaming with individual accounts.

This node provides practical experience with storage architecture, network shares, user permissions, media services, and backup workflows.

It also highlights an important operational distinction: RAID can help maintain storage availability after certain drive failures, but it does not replace independent backups. Recovery planning requires considering accidental deletion, corruption, hardware failure, and other scenarios that RAID alone cannot address.

#### Node 2 — Raspberry Pi 4B: Service Dashboard and DNS Filtering

This node hosts a Homepage dashboard that acts as a centralized portal for accessing household services and shared bookmarks.

The environment also uses two weather APIs to provide weather information through the dashboard and runs a primary Pi-hole DNS filtering instance.

This setup provides practical exposure to:

- Deploying and configuring self-hosted web applications.
- Creating a central service-access interface.
- Integrating information from APIs.
- Managing DNS-based filtering.
- Maintaining blocklists and understanding their effect on DNS resolution.
- Making infrastructure services accessible through a more user-friendly interface.

Pi-hole provides a practical introduction to DNS behavior and the role of DNS filtering in reducing access to known unwanted or potentially malicious destinations. Its effectiveness depends on configuration, list quality, and the limits of DNS-level filtering.

#### Node 3 — Raspberry Pi 4B: Help Desk and Secondary DNS

The third node hosts Zammad, an open-source help-desk and ticketing platform, alongside a secondary Pi-hole instance.

Zammad provides a structured way to record questions, requests, issues, and bugs instead of relying entirely on informal conversations.

The second Pi-hole uses a different subset of filtering lists and provides an additional filtering instance. This offers experience with maintaining multiple service instances and considering how network services can be distributed across devices.

A secondary DNS instance does not automatically guarantee failover or high availability. Client configuration, DNS settings, and service health must also be considered.

### 3. Containerization and Service Management

Docker is a central component of the environment. I use containerized services to organize applications, manage deployment configurations, and separate application workloads.

Multiple Portainer instances help administer container environments and provide a graphical interface for managing services.

This has provided practical experience with:

- Container deployment and configuration.
- Service ports and network exposure.
- Environment variables and persistent application data.
- Container lifecycle management.
- Troubleshooting startup and runtime failures.
- Understanding dependencies between applications and infrastructure.
- Managing several services without installing every application directly onto the host operating system.

Working with self-hosted services also requires considering application updates, persistent storage, credentials, exposed ports, and the consequences of changing a configuration that other services depend on.

### 4. Identity, Access Control, and Privacy

The homelab supports multiple household users and services. Storage shares and applications are configured with individual accounts where appropriate, helping keep users' files and service access separated.

This provides a practical context for understanding:

- Account management.
- Permission boundaries.
- The principle of least privilege.
- Service-specific access controls.
- The importance of protecting credentials.
- The difference between network reachability and authorized access.

Access controls must be tested rather than assumed to be effective. A properly designed environment should make it possible to verify that a user can access the resources intended for them without gaining unnecessary access to another user's information or administrative functions.

### 5. Troubleshooting and Operational Maintenance

Operating a multi-service environment creates practical troubleshooting scenarios that cannot always be resolved by following a single tutorial.

An application may fail because of a configuration issue, a port conflict, a missing dependency, an unavailable network service, a permissions problem, or an underlying hardware or operating-system issue.

Maintaining the environment has encouraged a methodical approach:

1. Identify the observable failure.
2. Gather relevant logs and configuration information.
3. Separate symptoms from possible causes.
4. Test plausible explanations.
5. Apply a controlled change.
6. Verify the result.
7. Document what changed when useful.

This approach is directly relevant to systems administration and cybersecurity, where accurate diagnosis is more useful than making repeated unverified changes.

### 6. Security-Relevant Lessons

The homelab is a practical learning environment, but operating services does not automatically make an environment secure. Security requires deliberate configuration, validation, maintenance, and an understanding of the system's exposure.

The environment provides a foundation for continuing to study:

- Network segmentation and service isolation.
- DNS filtering and its limitations.
- Authentication and authorization.
- Secure remote administration.
- Container and host security.
- Credential management.
- Log collection and troubleshooting.
- Backup and recovery procedures.
- Patch management and configuration hygiene.
- Availability and service dependencies.

The most important lesson is that security is an ongoing process. A service that works correctly is not necessarily configured securely, and a configuration that is secure today may need to change as the environment evolves.

### 7. Connection to Cybersecurity and Red-Team Development

This environment provides a useful bridge between theoretical security concepts and the practical operation of real systems.

Understanding how services are deployed, connected, authenticated, and maintained helps explain why certain vulnerabilities matter and how they may affect other components.

My homelab experience supports continued development in several areas:

| Technical area | Practical relevance |
|---|---|
| Linux and service administration | Understanding host systems, processes, permissions, and configuration. |
| Networking | Understanding connectivity, DNS, switching, and service exposure. |
| Docker and container management | Learning application deployment, isolation, persistence, and service dependencies. |
| Storage and backups | Understanding data availability, access controls, and recovery considerations. |
| Identity and permissions | Recognizing the importance of account separation and least privilege. |
| Application troubleshooting | Investigating logs, errors, configuration, and dependencies. |
| Infrastructure security | Evaluating how systems are exposed and how defensive controls can reduce risk. |
| Technical documentation | Recording architecture, configuration decisions, and operational procedures. |

For penetration testing, this knowledge helps establish a stronger understanding of the systems being assessed. For defensive roles, it supports practical familiarity with infrastructure operations and the consequences of configuration errors.

The environment is not presented as a production enterprise network or as proof of professional penetration-testing experience. It is a personally designed and operated lab that provides continuing hands-on experience.

### 8. Professional Portfolio Summary

> Designed, deployed, and maintained a multi-node homelab built around a custom compact network rack, managed switching, Raspberry Pi systems, Docker-based services, and centralized administration. Operated self-hosted storage and media services, Samba/SMB file sharing, device backup workflows, a household service dashboard, DNS filtering, and a help-desk platform. Developed practical experience in Linux administration, container deployment, networking, access control, storage, troubleshooting, and service maintenance.

### 9. Resume-Ready Bullets

- Designed and maintained a multi-node Raspberry Pi homelab with managed networking, centralized administration, and containerized services.
- Deployed and administered self-hosted services including OpenMediaVault, Samba/SMB file sharing, Jellyfin, Homepage, Pi-hole, and Zammad.
- Configured individual user accounts and access separation for household file-sharing and application services.
- Managed Docker-based deployments and used Portainer to administer containerized workloads.
- Developed hands-on familiarity with DNS filtering, network services, application troubleshooting, and infrastructure dependencies.
- Implemented a household storage and backup environment while developing awareness of RAID limitations, independent backup requirements, and recovery planning.
- Applied iterative troubleshooting to diagnose service and configuration problems across Linux-based infrastructure.

### 10. Future Development Opportunities

Potential next steps for expanding the homelab's security value include:

1. **Network segmentation:** Separate administrative devices, household clients, servers, and exposed services into appropriately controlled network zones.
2. **Centralized logging:** Collect relevant system and application logs to support troubleshooting and security monitoring.
3. **Vulnerability management:** Establish a routine for inventorying services, applying updates, and documenting known weaknesses.
4. **Backup validation:** Test recovery procedures and maintain independent copies of important data.
5. **Access-control testing:** Verify user permissions and service exposure from the perspective of different accounts and network locations.
6. **Monitoring and alerting:** Introduce tools that help identify service failures and suspicious activity.
7. **Authorized security labs:** Use isolated targets and purpose-built vulnerable applications to practice reconnaissance, vulnerability validation, and reporting without risking household services.

These improvements would allow the homelab to serve not only as an infrastructure project but also as a progressively more structured environment for learning defensive security and authorized offensive testing.


# Lead Pharmacy Technician & Store Trainer: Professional Experience and Cybersecurity Transferable Skills

## Overview

**Role:** Lead Pharmacy Technician and Store Trainer  
**Industry:** Healthcare and retail pharmacy operations  
**Professional background:** Nationally Certified Pharmacy Technician; vaccine-trained pharmacy professional  
**Career objective:** Transition into cybersecurity, with a focus on penetration testing, security operations, and red-team development.

## Summary

My experience as a Lead Pharmacy Technician and Store Trainer has developed a combination of operational discipline, attention to detail, confidentiality awareness, troubleshooting, team coordination, and employee training.

Pharmacy operations require accuracy, adherence to established procedures, responsible handling of sensitive information, and the ability to perform consistently in a regulated environment. These responsibilities have helped develop professional habits that are valuable in cybersecurity, where mistakes can affect data integrity, access security, regulatory obligations, and organizational operations.

My pharmacy background is not a substitute for dedicated IT security experience. Instead, it provides a foundation of transferable professional skills that complement my technical development in Linux, networking, self-hosted infrastructure, ethical hacking, and cybersecurity training.

## 1. Leadership and Operational Responsibility

As a Lead Pharmacy Technician, my professional responsibilities have included contributing to daily pharmacy operations, supporting workflow, and helping maintain consistent standards of work.

Leadership in a demanding operational environment requires more than completing individual tasks. It requires awareness of the larger workflow, communication with colleagues, prioritization, and the ability to help a team maintain standards when workloads and circumstances change.

These experiences translate into several useful professional capabilities.

### Workflow coordination

Effective operations depend on understanding how individual tasks fit into a larger process. Delays, errors, or communication failures in one stage can affect everything that follows.

This perspective is relevant to cybersecurity work involving incident queues, vulnerability assessments, remediation tracking, and operational handoffs.

### Prioritization under pressure

Pharmacy environments can involve competing demands that must be handled without losing sight of safety and accuracy.

Cybersecurity professionals similarly need to distinguish urgent incidents from routine work, assess the consequences of delay, and make sound decisions when time and resources are limited.

### Accountability

Working in a regulated environment reinforces the importance of following procedures, recognizing the limits of one's authority, and taking responsibility for the quality of one's work.

These habits are particularly valuable when handling security findings, sensitive systems, and changes that could affect an organization's operations.

## 2. Training, Knowledge Transfer, and Team Development

My Store Trainer experience has involved helping other employees learn established procedures and perform their work consistently.

Training requires more than knowing how to perform a task. It also requires explaining the reasoning behind a process, recognizing where someone needs additional guidance, and communicating instructions in a way that can be understood and applied.

This experience is relevant to cybersecurity in several ways.

### Explaining technical concepts

Security findings often need to be explained to people with different levels of technical knowledge. A vulnerability may be technically complex, but the underlying risk and recommended response must still be communicated clearly.

### Developing repeatable procedures

Effective training relies on consistency, documentation, and clear expectations. Those same principles support security runbooks, troubleshooting guides, standard operating procedures, and incident-response playbooks.

### Supporting team capability

A strong team becomes more effective when knowledge is shared rather than isolated with individual employees. Training experience supports a collaborative approach to problem-solving and continuous improvement.

## 3. Accuracy, Verification, and Quality Control

Accuracy is fundamental to pharmacy work. Processes must be followed carefully, information must be interpreted correctly, and discrepancies must be recognized rather than ignored.

Cybersecurity also depends on accurate analysis and verification.

Examples include:

- Confirming that a vulnerability is reproducible before reporting it.
- Distinguishing observed evidence from assumptions.
- Checking that a proposed remediation addresses the underlying problem.
- Validating configuration changes before considering a task complete.
- Documenting findings in a way that another professional can review.

My pharmacy experience has reinforced the importance of methodical work and checking details rather than relying solely on memory or intuition.

These habits are directly relevant to responsible security assessment and technical reporting.

## 4. Confidentiality and Responsible Information Handling

Healthcare environments require careful handling of sensitive information. Employees must respect privacy requirements, follow applicable policies, and access information only as appropriate for their responsibilities.

Cybersecurity professionals encounter similar principles when working with credentials, logs, customer records, vulnerability reports, and internal business information.

The transferable principles include:

- Limiting access to information according to legitimate responsibilities.
- Avoiding unnecessary disclosure of sensitive information.
- Following established policies and procedures.
- Recognizing that authorized access does not imply unrestricted permission.
- Handling records and evidence carefully.

My experience in healthcare supports a professional mindset centered on confidentiality, controlled access, and responsible information handling.

This is transferable experience, not a claim that pharmacy work itself constitutes formal cybersecurity or privacy-audit experience.

## 5. Troubleshooting and Problem-Solving

Operational environments rarely run perfectly at all times. Problems must be identified, assessed, and resolved while maintaining appropriate standards.

A disciplined troubleshooting process involves understanding the symptoms, gathering relevant information, considering possible causes, testing explanations, and verifying the outcome.

That approach closely complements technical troubleshooting.

In cybersecurity and systems administration, the same reasoning can be applied to:

- Investigating unexpected system behavior.
- Identifying configuration problems.
- Reviewing logs and error messages.
- Reproducing application failures.
- Distinguishing symptoms from root causes.
- Confirming that a fix resolves the original issue.

My broader technical experience with Linux, Docker, networking, self-hosted services, and application development gives me opportunities to apply this problem-solving mindset directly to IT environments.

## 6. Procedure Compliance and Risk Awareness

Pharmacy work takes place within a regulated environment where established procedures exist to reduce mistakes and protect patients.

Cybersecurity likewise relies on documented procedures, defined authorization, and risk-aware decision-making.

Examples include:

| Pharmacy-related professional habit | Cybersecurity application |
|---|---|
| Following established procedures | Adhering to assessment scope and approved testing procedures. |
| Checking details carefully | Validating findings and reviewing technical evidence. |
| Escalating issues appropriately | Reporting incidents or findings to the correct personnel. |
| Protecting sensitive information | Handling credentials, logs, and client data responsibly. |
| Training employees consistently | Supporting security awareness and technical knowledge sharing. |
| Maintaining reliable workflow | Tracking incidents, vulnerabilities, and remediation tasks. |
| Recognizing operational risk | Evaluating the consequences of changes and security testing. |

These are transferable habits rather than equivalent technical qualifications. Their value comes from applying them alongside appropriate cybersecurity knowledge and practical experience.

## 7. Communication and Collaboration

Security work frequently involves collaboration among technical specialists, managers, users, and other stakeholders.

A finding may require a technical explanation for an engineer, a concise risk summary for a manager, and clear remediation instructions for the person responsible for the affected system.

My experience supporting pharmacy operations and training employees has helped develop the ability to communicate procedures, coordinate with colleagues, and adapt explanations to the needs of the person receiving them.

These skills are useful in penetration-testing reports, help-desk and systems-analysis work, vulnerability management, and incident response.

## 8. Connecting My Professional Experience to My Technical Development

My career transition is supported by two complementary areas of development.

### Professional and operational foundation

- Lead Pharmacy Technician experience.
- Store Trainer responsibilities.
- National Certified Pharmacy Technician credential.
- Vaccine-training background.
- Experience working within structured, regulated procedures.
- Team coordination, communication, and operational accountability.

### Technical foundation

- Cisco Certificate in Ethical Hacking (CCEH).
- Cisco ethical-hacking coursework and authorized CTF practice.
- CISA/DHS training in IT and industrial control system cybersecurity.
- Linux and self-hosted infrastructure experience.
- Docker-based service deployment and management.
- Networking, troubleshooting, and application-development experience.
- Local AI model deployment and configuration.

Together, these areas support a professional profile combining operational reliability and people-focused experience with an expanding technical cybersecurity skill set.

## 9. Career Relevance

This background is relevant to entry-level opportunities in areas such as:

- Junior security analyst.
- Security operations center (SOC) analyst.
- IT support or systems support with a security focus.
- Vulnerability management support.
- Junior penetration-testing roles where practical skills and lab evidence meet the employer's requirements.
- Technical support and systems administration.
- Security awareness and technical training.

A pharmacy leadership background does not independently qualify someone for every security role. However, it can distinguish a candidate by demonstrating that technical learning is accompanied by professional discipline, team experience, and an understanding of the importance of controlled processes.

For penetration testing in particular, the next step is to continue building practical evidence through authorized labs, detailed reports, scripting, networking, and increasingly realistic assessment exercises.

## 10. Portfolio Summary

> My experience as a Lead Pharmacy Technician and Store Trainer has developed transferable skills in operational coordination, employee training, quality control, confidentiality, troubleshooting, and procedure compliance. Working in a regulated healthcare environment has reinforced the importance of accuracy, accountability, and responsible information handling. I am building on that foundation through ethical-hacking training, CISA/DHS cybersecurity coursework, Linux administration, self-hosted infrastructure, and hands-on cybersecurity labs as I pursue a career in cybersecurity.

## 11. Resume-Ready Bullets

- Supported pharmacy operations in a lead technician capacity, emphasizing workflow coordination, accuracy, established procedures, and operational reliability.
- Served in a Store Trainer capacity, helping employees learn processes and apply established standards consistently.
- Applied attention to detail, confidentiality awareness, and risk-conscious decision-making in a regulated healthcare environment.
- Developed transferable troubleshooting, communication, and prioritization skills relevant to technical support and cybersecurity operations.
- Complemented professional leadership experience with cybersecurity training, ethical-hacking coursework, Linux, networking, and self-hosted infrastructure projects.

## 12. Professional Positioning

My pharmacy background represents a foundation of transferable professional experience, while my cybersecurity coursework and technical projects demonstrate the direction of my career development.

I intend to build on both: retaining the discipline, accountability, and collaborative habits developed through years of pharmacy work while continuing to strengthen my practical security-assessment skills.

## Eagle Scout — Leadership, Service, and Long-Term Commitment

**Achievement:** Eagle Scout  
**Year Earned:** 2018  
**Organization:** Scouting America (formerly the Boy Scouts of America)

### Overview

Earning the rank of Eagle Scout in 2018 represents a significant personal achievement built on years of participation, advancement, learning, and commitment to the principles of Scouting.

Unlike an accomplishment earned through a single examination or short-term course, Eagle Scout represents sustained effort toward a long-term goal. It requires a Scout to progress through established advancement requirements, demonstrate leadership and responsibility, serve others, and complete an Eagle Scout service project.

For me, this achievement represents more than a title. It reflects a foundation of perseverance, accountability, service, and personal development established over an extended period of time.

### Long-Term Commitment and Perseverance

Reaching Eagle Scout requires maintaining progress toward a demanding goal while balancing other responsibilities. The achievement reflects the ability to work toward defined standards over time rather than relying solely on short bursts of motivation.

This mindset is relevant to cybersecurity, where developing competence requires continuous study, repeated practice, troubleshooting, and the willingness to learn from failure.

Security professionals must often work through complex problems that do not have immediate solutions. Persistence, structured learning, and a willingness to keep improving are essential qualities when investigating vulnerabilities or developing new technical skills.

### Leadership and Accountability

Scouting emphasizes leadership through responsibility, preparation, cooperation, and service.

These principles translate into professional environments where individuals must communicate clearly, contribute to a team, follow through on commitments, and accept responsibility for their decisions.

In cybersecurity, technical ability is only one component of effective performance. Teams also depend on people who document their work, respect authorization boundaries, communicate risks, and act responsibly when unexpected problems arise.

### Service and Community Responsibility

A central principle of Eagle Scout is service to others. The achievement reflects an understanding that leadership is not solely about individual advancement; it also involves contributing to something beyond oneself.

That principle aligns with the responsible practice of cybersecurity. Security work protects systems, information, services, and the people who depend on them. Ethical security professionals use their knowledge within authorized boundaries and consider the consequences their actions may have on others.

### Planning and Project Execution

The Eagle Scout advancement process includes demonstrating leadership and completing a qualifying service project. The project component provides experience with organizing work toward a defined objective and accepting responsibility for its completion.

Those general project-management principles are useful in technical work, including planning infrastructure deployments, coordinating tasks, maintaining documentation, and troubleshooting projects through completion.

This does not imply that the Eagle Scout project itself was a cybersecurity project; its relevance is the transferable experience of working toward an objective with responsibility and structure.

### Relevance to Cybersecurity

The qualities represented by this achievement complement my technical development in several areas:

- **Persistence:** Continuing through difficult technical problems and unfamiliar concepts.
- **Discipline:** Maintaining progress toward long-term learning and career goals.
- **Accountability:** Taking responsibility for decisions, results, and commitments.
- **Leadership:** Contributing to teams and helping others work toward shared objectives.
- **Service:** Applying knowledge in ways that benefit others.
- **Ethical responsibility:** Recognizing that capability must be paired with sound judgment.
- **Project execution:** Organizing work around defined requirements and a desired outcome.

### Professional Portfolio Summary

> Earned the rank of Eagle Scout in 2018, reflecting sustained commitment, leadership development, service, and personal accountability. The achievement represents a long-term investment in perseverance and responsible leadership—qualities I continue to apply to professional development, technical projects, and my pursuit of a career in cybersecurity.

### Personal Significance

Eagle Scout is a milestone that represents years of effort rather than a single moment of success. It serves as evidence of an early commitment to personal growth, service, and responsibility.

As I continue developing my career in cybersecurity, I view those principles as a foundation for the professional I intend to become: someone who continues learning, follows through on difficult work, supports others, and uses technical knowledge responsibly.


The objective is to become a cybersecurity professional who can investigate technical problems methodically, communicate findings clearly, respect operational constraints, and contribute reliably to a team.

