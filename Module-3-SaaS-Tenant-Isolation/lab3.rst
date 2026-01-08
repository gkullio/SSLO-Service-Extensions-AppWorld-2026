Implement SaaS Tenant Isolation
==============================================================================

You will now enable and test the **tenant isolation** functionality. This will insert headers into the HTTP request to identify the tenants which would be allowed for the SaaS application. This can be setup for users to only use a specific tenant(s) to prevent users from copying data between tenants.

Let's take a look at the iRule to get an idea of the various services you can configure, and what we will use for testing the functionality in this lab. 

You will then test by going to https://httpbin.org/headers in your **Ubuntu-Client** WEBRDP session to show the missing tenant control headers. Then again after modifying the configuration, test to show how the headers are properly inserted.

Inspect iRule *saas-tenant-rule*
--------------------------------------------------------------------------------

#. Go to your **BIG-IP SSLO** GUI tab and navigate to **Local Traffic > iRules** and click on the **saas-tenant-irule** iRule to view the contents. There are 250 lines to the rule, and most of that is comments to help the user understand the functionality of the iRule.  

   .. note::

      **Do not change anything at this time. This is only to show the extent of the iRule**

#. Please focus on lines 125-135 of the iRule. This is where we will test the proper insertion of headers for this lab. This section sets the static variable and array to define what headers and values are to be inserted.

   .. image:: images/saas-irule-lab-test.png
      :align: left

#. Now go to lines 241-248. This section executes the action based on the match of the URL. In this case, we are matching against httpbin.org. This is so we can actually see the headers being inserted.

   .. image:: images/saas-irule-action.png
      :align: left


#. Now hit the back button on the browser to get out of the iRule view, and lets test the functionality before adding new Service Extension.




View the reported headers before adding the SaaS Tenant Isolation Service
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to the following URL: 

   .. code-block:: text

      https://httpbin.org/headers


#. You should **not** see the X-Test-Header-1 or X-Test-Header-2 headers in the response. You will see something similar the following:

   .. image:: images/saas-headers-missing.png
      :align: left



#. Lets get back to the SSL Orchestrator UI and update the Interception Rule and Service Chain to use this Service Extension. 

Click on the **SSL Orchestrator** tab on the left side of the GUI, and then click **Configuration**.


Modify Interception Rule
--------------------------------------------------------------------------------

#. In the **SSL Orchestrator UI**, click on the **Interception Rules** tab.

   .. image:: ./images/saas-interception-rule.png
      :align: left


#. Click on the **sslo_l3_outbound-in-t-4** Interception Rule to view the **Summary** page.

   .. note::

      We are going to use the same interception rule for SaaS Tenant Isolation. All of the Service Extensions we are using in this lab can be stacked on top of a single Interception Rule and L3 Outbound topology.

   .. image:: ./images/user-coaching-2.png
      :align: left


#. Click on the **Edit** (pencil) icon to view the settings.

#. Scroll down to the **Resources > iRules** section and double-click on the **/Common/saas-tenant-irule** iRule to add it to the **Selected** panel.

   .. image:: ./images/saas-interception-rule-assign.png
      :align: left


#. Click on the **Save & Next** button to return to the **Summary** page.

   .. image:: ./images/user-coaching-4.png
      :align: left


#. Click on the **Deploy** button.

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.



Add SaaS Tenant Isolation to the existing *User Coaching* Service Chain
--------------------------------------------------------------------------------

It's time to add the SaaS Isolation Service to the existing Service Chain that was created in the previous lab.

#. Click on the **Service Chains** tab and click the existing Service Chain **ssloSC_user_coaching**.

   .. image:: ./images/saas-service-chain.png
      :align: left

#. The name field is already filled out as we are amending the existing Service Chain.

#. Double-click on the **ssloS_F5_SaaS-Tenant-Isolation** Service to add to the Selected Service Chain Order.

   .. image:: ./images/saas-service-chain-add.png
      :align: left

#. Click **Deploy** and then **OK** to acknowledge the warning.  Click **OK** again after the deployment has completed.








