OPTIONAL:Implement User Coaching with JA4 Persistence Method
==============================================================================

You will now enable and test the **user coaching** functionality. This will produce a prompt in the web browser when a user attempts to connect to a *risky AI* web site.



Modify Interception Rule
--------------------------------------------------------------------------------

#. In the **SSL Orchestrator UI**, click on the **Interception Rules** tab.

   .. image:: ./images/user-coaching-1.png
      :align: left


#. Click on the **sslo_l3_outbound-in-t-4** Interception Rule to view the **Summary** page.

   .. image:: ./images/user-coaching-2.png
      :align: left


#. Click on the **Edit** (pencil) icon to view the settings.

#. Scroll down to the **Resources > iRules** section and double-click on the **/Common/user-coaching-ja4t-rule** iRule to add it to the **Selected** panel. ``**Do not move the user-coaching-rule. This rule is already applied to the internal virtual server**``


   .. image:: ./images/user-coaching-3.png
      :align: left


#. Click on the **Save & Next** button to return to the **Summary** page.

   .. image:: ./images/user-coaching-4.png
      :align: left


#. Click on the **Deploy** button.

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.


|


Trigger Conditions for User Coaching
--------------------------------------------------------------------------------

The presentation of the user coaching prompt is determined by a URL category match. The category list is defined in the **user-coaching-rule** iRule.

#. Navigate to **Local Traffic > iRules** and verify that the following iRules are present.

#. Click on the **user-coaching-rule** iRule to view it.

#. Notice that the **COACHING_CATEGORIES** variable defines an array of URL categories.

   .. image:: images/user-coaching-trigger.png
      :align: left

   |

   .. note::

      Per the iRule comments, you can query the URL Category Database to determine the category names to use here. Do not change anything at this time.

|

Test User Coaching with JA4 Persistence Method
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to https://chatgpt.com/. You should receive the SSL Orchestrator user coaching prompt as follows:

   .. image:: ./images/user-coaching-13.png
      :align: left


#. Click on the **Agree** button to acknowledge the warning and terms of use policy. You will then be presented with the OpenAI ChatGPT site.

   .. image:: ./images/user-coaching-14.png
      :align: left

#. Restart **Firefox** and browse to ChatGPT again. You should not see the prompt reappear because the original user coaching acknowledgement has not expired yet.

   .. note::

      The default user coaching session timeout setting is 3600 seconds. This value is configurable in the **user-coaching-rule** iRule.
      **NEED TO ADDRESS THIS WITH KEVIN. Current behavior is that the prompt appears every time they access ChatGPT.**

