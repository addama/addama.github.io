---
layout: default
title: "Security Policy"
permalink: /security-policy/
---

# Security Policy {#top}






## Purpose {#purpose}

The purpose of this document is to establish policy governing how physical, network, server, and software security is handled, as well as what expectations are levied against these areas and the people that operate within them.






## Scope {#scope}

The scope of this document applies to all:

* **Locations:** Buildings, rooms, lots, and areas owned and/or operated within by Xtract Solutions
* **Servers:** Servers and standalone service computers owned, leased, or maintained by Xtract Solutions
* **Networks:** Networks or network systems, and network-adjacent systems and tools created, maintained, or relied upon by Xtract Solutions
* **Software:** Software written, utilized, or contracted by Xtract Solutions
* **Employees:** Employees, contractors, third party entities, and affiliates of Xtract Solutions






## General {#general}

### Awareness and Reporting {#awareness-reporting}

It is the responsibility of Xtract Solutions employees to be on the look out for and to report any potential or actual security weaknesses or breaches, even if the potential or the impact is small. 

All potential and actual security breaches must be evaluated with high priority until both of these conditions is satisfied, if possible:

* The threat or impact is neutralized 
* The threat or impact is documented, with a plan in place to prevent the breach in the future

Additionally, all employees must treat client, affiliate, networked, and associated locations, servers, networks, and software with the same level of heightened security awareness and reporting acumen as our own unless specified otherwise by the owners/operators of those entities.

It doesn't matter how small, and it doesn't matter if it might turn out to be nothing, nor does it matter who you report to - **just report it!**

### Personal Security {#personal-security}

In addition to organizational security expectations, employees must exercise good personal security practices. These are, but are not limited to:

* Locking computers when not in use
* Maintaining high password complexity
* Being smart about their downloads, uploads, and what they plug into company computers
* Avoiding suspicious websites, services, and people
* Deflecting and reporting any attempt to gain information about the company or our clients by outside people or entities
* Not conducting business over unsecure networks or suspicious "free" wifi
* Limiting sensitive information communicated over social media, as well as to family and friends

### Email and Communication {#email-communication}

Xtract Solutions business email will not be used to transmit confidential data outside of the organization or its clients. Recipients of emails containing confidential data must be verified as being the appropriate contact for that kind of data within that organization.

Employees must be wary of email scams and social engineering. These can include:

* Unsolicited product or consultation offers
* Unsolicited attachments of any kind - not just executables!
* Messages from previously unknown people claiming to be from one of our clients, especially if we haven't done business with that client in a while. Always verify at the source.
* Obvious clickbait or sensationalist titles or wording, especially if accompanied by a request or demand to open an attachment, follow a link, respond, or watch a video
* Emails that appear to be from other employees or clients, but do not reflect that person's writing style, or seem sudden, urgent, too casual/personal, or overly specific. 

Employees are encouraged to show (not forward, just show) any suspicious emails to their supervisor if they are uncertain if it's trustworthy or not.

### Passwords {#passwords}

Password security is often talked about, but one of the easiest ways to completely invalidate what would otherwise be a sound security strategy. Loss of the control of any given account could potentially lock us out of our entire system, or worse, our clients' systems. Our clients trust us to maintain the sanctity of their security, and password management is a key part of that.

Employees must consider the following in relation to passwords:

* Choose passwords longer than 8 characters, that are reasonably complex and not guessable. You're going to want to be lazy, but don't. Pick a good password instead.
* Memorize passwords rather than writing them down
* Exchange credentials only when absolutely necessary, and verbally when possible
* Regularly change passwords, particularly when an employee leaves the company

### Training {#training}

Xtract Solutions employees must receive yearly training in the security topics expressed in this document. All employees must review this document once per year, acknowledging this training via email to their supervisor or their delegate.

Remedial training must be conducted by employees that cause, fail to report, or worsen security breaches or impacts. Remedial training will consist of more thorough explanation of potential security problems in all areas, and will be administered by the employee's supervisor.






## Physical Security {#physical-security}

### General {#physical-security-general}

All Xtract Solutions employees are expected to maintain the physical security of our offices, rooms, and general areas, as well as the premises in which our solutions are deployed to the satisfaction of those areas' owners. 

General physical security practices include:

* Verifying, vouching for, and escorting any visitors immediately upon their entering the facility
* Locking exterior doors when the office is closed
* Turning on the alarm when the office is closed
* Maintaining and reporting-for-repair the physical integrity of windows, doors, locks, barricades, etc
* Being aware of and reporting potential intruders on or around the property that exhibit suspicious behavior
* Securing keys and other physical access components

### Locks and Alarm {#locks-alarm}

All Xtract Solutions buildings, and rooms containing confidential information or assets, must be locked using a key, key card, or other physical access component. 

Exterior doors and windows must be locked when the office is closed.

The Xtract Solutions main office must be guarded by an intrusion alarm, which is armed by the last person to leave the office for the day. 

### Garbage and Recycling {#garbage-recycling}

Confidential information on paper media must be shredded before throwing out or recycling. 

CDs, hard drives, thumb drives, and other storage media for general use must be wiped to a reasonable degree, if possible, before disposing of them.

Storage media that has held PII, PHI, or HIPAA data must be handled in the following ways according to necessity: 

* Overwritten (using a tool or service to overwrite fields in the storage), or 
* Purged (by degaussing or otherwise ruining the media's ability to hold information), or
* Destroyed (physically destroying the media by disintegrating, pulverizing, melting, incinerating, or shredding)






## Network/Server Security {#network-security}

### General {#network-security-general}

??? Data flow diagrams
??? Network diagrams
??? Server passwords
??? VPN required
??? What about these? 
	Dynamic Scans: Nessus, OpenVAS, ZAP, Burp Suite
	Static Scans: Any report from a professional grade static analysis tool such as HP Fortify, IBM AppScan, CheckMarx, or equivalent.
	SSLLabs SSl/TLS Security Testing, at least "A" grade, no "weak ciphers"
??? Wifi passwords? Do we have guest wifi?

### Firewall {#firewall}

??? Do we have a firewall? Do we mandate each PC have a firewall?

### DNS {#dns}

??? Do we do anything with DNS that is standardized enough to write rules out of it? How do we manage routing internally? Do we have static IP addresses?

### Logging {#network-logging}

??? Do we have logs (either that we've made or that come from some service) that can be audited to see who accesses our servers/network?
??? How often are logs checked? How often SHOULD they be checked? 

### Backups {#backups}

??? How do we do backups? How often? Incremental or total? Are the backups on separate drives and/or rundandant drives? What do we make backups of? What security is necessary to access backups? Can clients request their backups? How do we deliver them?

### Remote Access {#remote-access}

??? What remote access tools do we use? How are they used? How are accounts created/removed? What servers/networks are accessible this way?






## Software Security {#software-security}

### General {#software-security-general}

All software produced by Xtract Solutions must be created and maintained with security in mind. Any security breach could result in loss of money, assets, or trust for us or our clients, or loss of life for our clients' patients. It is encumbent on our programmers to ensure the highest standards of security are in place.

In general, we must acknowledge that the frontend of our application is written in Javascript, which is inherently insecure, as all information is available to the browser, and therefore to the user. This is done to protect browser users against malicious Javascript, but it does also affect our ability to be secure to protect ourselves and our data. Xtract Solutions can mitigate the risk from this by moving any important settings and decisions to a backend API layer that independently controls and checks all inputs, permissions, and settings.

### Vulnerability Scans {#vulnerability-scans}

??? SonarQube?

??? What about these? 
	Dynamic Scans: Nessus, OpenVAS, ZAP, Burp Suite
	Static Scans: Any report from a professional grade static analysis tool such as HP Fortify, IBM AppScan, CheckMarx, or equivalent.
	SSLLabs SSl/TLS Security Testing, at least "A" grade, no "weak ciphers"

### Secure Programming {#secure-programming}

In order to ensure the security of our data and systems, Xtract Solutions employs a range of secure programming standards, tools, and technology in both the front and back ends of our software.

Frontend security measures include:

* Patient data is only stored for as long as it is needed by the components that use it, and only the minimum amount of data for those components is stored
* Man-in-the-middle attacks are mitigated by enforcing a SHA512 integrity hash of all included/expected Javascript assets that ensures the scripts that are intended to run are actually being run. This hash can further be used to pinpoint the release used should a breach occur
* Frontend routes are individually protected so that unauthorized users cannot access other parts of the application
* Passwords are compared against a service or tool to determine if they are unsecure
* Individual elements of the app are assigned configurable privileges that the user must be given by an administrator

Backend/API security measures include:

* An ORM library is used to create prepared statements to protect from SQL injections
* OAuth2 is used to securely manage user logins using an App ID, Secret, username, and password, as well as a 5 minute authorization token for the frontend and a 4 minute authorization token for the API
* Only salted password hashes are stored in the database using the most secure encryption standard available
* Individual API routes are assigned privileges that the user must be given by an administrator
* Cross-Origin Resource Sharing (CORS) technology is used to limit the origins that API requests come from, and the assets that can be shared 

### Logging {#software-logging}

Xtract Solutions software must include a click log functionality, which minimally records clicks by user, where the click happened, the patient ID and/or prescription ID if applicable, and the timestamp. This click log provides an auditable accountability resource to trace malicious or accidental misuse of the app by its users.

API requests are logged in a similar fashion, include the route, http method, parameters, IP address, user ID, response code, and timestamp.

### Third Party Software {#third-party-software}

Effort must be made to verify the security posture and risks of any third-party tools, libraries, services, and references used in Xtract Solutions software. This verification can include:

* Reading through the source code, if available, to identify any security vulnerabilities
* Finding or requesting any security documentation or guarantees produced by the creators, as well as any security reports produced for the product
* Searching for user reported vulnerabilities or problems on Google or sites like Stack Overflow
* Reviewing the Git repo, if available, as well as the project's issues, releases, and documentation

All dependencies must be kept up to date to ensure that security and programming fixes are implemented in a timely manner.

### Source Control {#source-control}

Xtract Solutions software and tools must be stored in private repositories, with access restricted to Xtract Solutions employees and contractors as necessary. Storing source code in a version controlled repository assures that our hard work is kept secure from espionage from outside the organization, as well as malicious or unintentional misuse from employees.

Source Control accounts, like those in Github, are to be reviewed regularly, and particularly when an employee leaves, a contract with outside developers finishes, or at least yearly. Preference will be given to removing access over granting it.






# Appendix A: Glossary {#appendix-a}

## Glossary

### Confidential Data

Confidential or sensitive data includes client databases, patient records, financial data, PII, employee records, org charts, call lists, customer/lead lists, and all other information that is:

* Crucial to the running of our business, or our clients' business
* Personally Identifying Information (PII)
* Has the potential to be used against us either in ligitation or competition

### CORS

Cross-Origin Resource Sharing is a protocol that allows a networked location to specify where requests are allowed to come from. This creates a white-list of known and acceptable computers/servers that Xtract Solutions can control.

### ORM

Object-Relational Mapping is a process by which data in one format is converted into another format for use by something else. With regards to programming and databases, this is generally actualized as a library or tool that convert data from an application into statements that can be executed by a database. The process for doing this generally includes sanitizing the data and safeguarding against invalid values.

### OAuth2

OAuth is a protocol for requesting, obtaining, and managing authorization for access to software, tools, and servers. OAuth uses a token system to represent temporary authorization. Tokens expire after a configurable amount of time, and are issued to the user or client system by a centralized server, which keeps track of these authorizations and serves as the single authority for who can access the content.

OAuth 2.0 (OAuth2) is the current version of OAuth in use.






# Appendix B: Resources {#appendix-b}

**Department of Homeland Security, National Cyber Awareness System**

* [Social Engineering Examples](https://www.us-cert.gov/ncas/tips/ST04-014)
* [Staying Safe on Social Media](https://www.us-cert.gov/ncas/tips/ST06-003)
* [Using Caution with Email Attachments](https://www.us-cert.gov/ncas/tips/ST04-010)
* [Good Security Habits](https://www.us-cert.gov/ncas/tips/ST04-003)
* [Protecting Your Privacy](https://www.us-cert.gov/ncas/tips/ST04-013)
* [Choosing and Protecting Passwords](https://www.us-cert.gov/ncas/tips/ST04-002)

**HIPAA**

* [What do the HIPAA Privacy and Security Rules require of covered entities when they dspose of protected health information?](https://www.hhs.gov/hipaa/for-professionals/faq/575/what-does-hipaa-require-of-covered-entities-when-they-dispose-information/index.html)

**CORS**

* [Cross-Origin Resource Sharing, Wikipedia](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)
* Cross-Origin Resource Sharing Specification, W3C] (https://www.w3.org/TR/cors/)

**OAUTH**

* [OAuth 2.0](https://oauth.net/2/)