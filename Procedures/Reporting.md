### Create a new project with the appropriate structure of directories and sub-directories
```
mkdir -p ACME-IPT/{Admin,Deliverables,Evidence/{Findings,Scans/{Vuln,Service,Web,'AD Enumeration'},Notes,OSINT,Wireless,'Logging output','Misc Files'},Retest}
```

### Triggers
When you hit an event trigger, stop what you are doing and fill in the appropriate fields.

The idea is that by filling out the report as these milestones occur, you’ll have most of the report done by the time the engagement wraps up.

These are the triggers I used, but you can create your own based on what works best for you. Make sure to write them down and refer to them regularly during the exam. If you’d like, use the table of contents of this blog post open for periodic reference.

### When The Exam Starts
- Meta
    - **Candidate name, title and email**
    - **Engagement Information**
- Document Control
    - **Customer Contacts**
- Network Penetration Testing Assessment Summary
    - Network Summary
    - Summary of Findings
- Executive Summary
    - Executive Summary
    - Approach
    - **Scope**

Basically, fill out the **Meta**, **Document Control**, and **Network Penetration Testing Assessment Summary** sections completely and most of the **Executive Summary**, leaving the **Assessment Overview and Recommendations** field for later.

Most these fields are fairly standard and require little to no modifications. Read them carefully and decide for yourself if you need to change something or leave as is.

### When A Host Or Service Is Discovered
Once you discover a live host and enumerate the available services (e.g., via an Nmap scan), you should fill in the appropriate appendix:

Appendix
Host & Service Discovery

### When A Virtual Host Or Subdomain Is Discovered
You should fill in the appropriate appendix with both the domains provided in the scope of the engagement (if any) and those you discover during your penetration test:

Appendix
Subdomain Discovery

### When A Security Finding Is Discovered
This is one of the most important and time-consuming triggers, so it’s crucial to handle it correctly.

For each security finding, you need to add a Finding to the report.

