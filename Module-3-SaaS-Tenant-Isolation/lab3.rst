Implement SaaS Tenant Isolation
==============================================================================

You will now enable and test the **tenant isolation** functionality. This will insert headers into the HTTP request to identify the tenants which would be allowed for the SaaS application. This can be setup for users to only use a specific tenant(s) to prevent users from copying data between tenants.

Let's take a look at the iRule to get an idea of the various services you can configure, and what we will use for testing the functionality in this lab. 



Inspect iRule ``saas-tenant-rule``
--------------------------------------------------------------------------------



