SaaS Tenant Isolation Scenario
================================================================================

Challenge
--------------------------------------------------------------------------------

Your company has a growing number of SaaS applications that are used for daily productivity, (Office 365, Webex, Zoom, Youtube, Githubm, etc.) and you are concerned about the risk of misuse and data exfiltration. You are challenged with finding a solution to reduce this risk by implementing a strategy to isolate controls to restrict access to unnecessary portions of SaaS applications.

|

Solution
--------------------------------------------------------------------------------


The **service extension** for **tenant isolation** can help meet this challenge. When a user attempts to connect to a SaaS Application, the **tenant isolation** inspection would be applied to the traffic flow. This action would be based on iRule header inspection that can be set for a specific SaaS application and can remove and insert various headers based on the organizational access allowed to the service.  