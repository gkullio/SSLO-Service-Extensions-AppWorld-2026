Implement SaaS Tenant Isolation
==============================================================================

You will now enable and test the **tenant isolation** functionality. This will insert headers into the HTTP request to identify the tenants which would be allowed for the SaaS application. This can be setup for users to only use a specific tenant(s) to prevent users from copying data between tenants.

Let's take a look at the iRule to get an idea of the various services you can configure, and what we will use for testing the functionality in this lab. 



Inspect iRule *saas-tenant-rule*
--------------------------------------------------------------------------------

#. Go to you **BIG-IP SSLO** GUI tab and navigate to **Local Traffic > iRules** and click on the **saas-tenant-irule** iRule to view the contents. There are 250 lines to the rule, and most of that is comments to help the user understand the functionality of the iRule.  

    .. note::

      **Do not change anything at this time. This is only to show the extent of the iRule**

#. Please focus on lines 125-135 of the iRule. This is where we will test the proper insertion of headers for this lab. This section sets the static variable and array to define what headers and values are to be inserted.

   .. image:: images/saas-irule-lab-test.png
      :align: left

#. Now go to lines 241-248. This section executes the action based on the match of the URL. In this case, we are matching against httpbin.org.

   .. image:: images/saas-irule-action.png
      :align: left

#. Now lets get back to the SSL Orchestrator UI and update the Interception Rule to use this Service Extension.



Modify Interception Rule
--------------------------------------------------------------------------------




