Implement DoH Guardian
======================

We have confirmed the DoH Guardian configuration objects were successfully added to BIG-IP SSLO.  We now configure the existing **L3 Outbound Proxy** to use the new service.  

During this lab, we will perform the following actions:
   - Review the *DoH Guardian iRule* to see the various controls available.
   - Add the **DoH Guardian Service** to the existing Service Chain
   - Configure Firefox in the Ubuntu-Client to use Google's DoH server.
   - Test the DoH Guardian Service Extension running a tail command on the BIG-IP LTM Logs, then go to any site using the DoH configured Firefox browser in the Ubuntu-Client.
   - Enable the *blackhole* mode on the Doh Guardian iRule to block any DoH requests that are categorized as *Sports*. 

|

Inspect the DoH Guardian iRule *doh-guardian-irule*
---------------------------------------------------

#. Go to the **BIG-IP SSLO** GUI tab and navigate to **Local Traffic > iRules** and click on the **doh-guardian-irule** iRule to view the contents.

   .. note::

      **Please do not modify the iRule at this time.** Review the notes and comments in each section to understand the functionality of the iRule. 

#. Look at lines 40 - 44, and 54 - 58. These are the sections that control *blackhole* and *sinkhole* mode.  For this portion of the lab, we will use the *blackhole* feature.  We will use the other feature in the next lab.

   .. image:: images/doh-blackhole-irule.png
      :align: left

   .. image:: images/doh-sinkhole-irule.png
      :align: left


#. As you can probably notice, this is a quite complex iRule. However, it was designed in a way to be easy to modify and change the behavior.  Each section of the iRule is commented to explain the functionality of the code.

To customize functionality
The doh-guardian-rule iRule has a number of editable settings:

DOH_LOG_LOCAL:
Enables or disables local (/var/log/ltm) logging of DoH requests and events. (1=on, 0=off)
DOH_LOG_HSL:
Defines a high-speed logging pool to send logs to external SIEM. (pool name)
DOH_CATEGORY_TYPE:
Defines the category database to use, subscription, custom, or both. (string selection)
DOH_BLOCKING_BASIC:
Enables or disables basic DoH blocking. This option is mutually exclusive and simply blocks all detected DoH requests. (1=on, 0=off)
DOH_BLACKHOLE_BY_CATEGORY:
Defines the list of categories that will trigger a DoH blackhole action. (category list)
DOH_BLACKHOLE_BY_CATEGORY_ACTION:
Allows for the default blackhole action, or a dryrun (logging) action. (string selection)
DOH_SINKHOLE_BY_CATEGORY:
Defines the list of categories that will trigger a DoH sinkhole action. (category list)
DOH_SINKHOLE_BY_CATEGORY_ACTION:
Allows for the default sinkhole action, or a dryrun (logging) action. (string selection)
DOH_SINKHOLE_IP4:
Defines the IP4v address that will be used for the sinkhole action on A requests. (ipv4 address)
DOH_SINKHOLE_IP6:
Defines the IP4v address that will be used for the sinkhole action on AAAA requests. (ipv6 address)
DOH_ANOMALY_DETECTION:
Enables or disables anomaly detection. (1=on, 0=off)
DOH_ANOMALY_CONDITION_LONG_DOMAIN:
Defines the long subdomain anomaly detection, by virtue of a max character length setting (integer, default=52 characters).
DOH_ANOMALY_CONDITION_LONG_DOMAIN_ACTION:
Defines the action to be taken on the long subdomain anomaly: dryrun, drop, blackhole, or sinkhole. (string selection)
DOH_ANOMALY_CONDITION_UNCOMMON_TYPE:
Defines the uncommon query type anomaly detection, by virtue of a list of uncommon types. (DNS record type list)
DOH_ANOMALY_CONDITION_UNCOMMON_TYPE_ACTION:
Defines the action to be take on the uncommon type anomaly: dryrun, drop, blackhole, or sinkhole. (string selection)

Add the DoH Guardian Service to the existing Service Chain
----------------------------------------------------------

Now that we have confirmed the DoH Guardian configuration objects were successfully added to BIG-IP SSLO, we will add the DoH Guardian Service to the existing Service Chain.  

#. Go to the **BIG-IP SSLO** GUI tab in your web browser and navigate to **SSL Orchestrator > Configuration**. 

#. Click on **Service Chains** and then click on the **ssloSC_user_coaching** Service Chain.  

   .. image:: images/doh-service-chain-add.png
      :align: left

#. Double click the **ssloS_F5_DoH** in the Services Available list to add it to the Selected Service Chain Order.

   .. image:: images/doh-service-chain-add-1.png
      :align: left

#. Click **Deploy** then **OK** (possibly twice) to confirm the changes.  

Configure the Firefox browser in the Ubuntu-Client to use Google's DoH server
-------------------------------------------------------------------------------

#. Go to the **Ubuntu-Client** GUI tab in your web browser and open up the **Firefox Browser**.

#. In the Firefox Browser, click on the **Settings** icon (three horizontal lines) and then click on **Settings**.

#. In the **Find in Settings** search box, type **DoH**, and it will display the following:

   .. image:: images/doh-firefox-configure.png
      :align: left

#. In order to force all browsing to use DNS-over-HTTPS, click the **Increased Protection** radial button. 

#. In the **Choose provider** text box, type the following:

|

   .. code-block:: text

      https://dns.google/dns-query

#. After inputting the Google DNS provider, you should see the Status change to **Active** and the Provider Name change to **dns.google**.

   .. image:: images/doh-firefox-configure-2.png
      :align: left

#. After configuring you can close and reopen **Firefox**.

|

Test the DoH Guardian Service Extension *blackhole* functionality
-------------------------------------------------------------------------

So far, we have inspected the **doh-guardian-irule**,  added the **ssloS_F5_DoH** Service to the existing **Service Chain**, and setup **Firefox** to use Google's DoH server for all DNS queries.

Logging is setup automatically in this lab to log all DNS-over-HTTPS requests to the local log file (/var/log/ltm). 

#. Go back to your **BIG-IP SSLO** in your UDF Environment and open the **Web Shell**.  From there you can view the running logs with the following command:  

   .. code-block:: text

      tail -f /var/log/ltm

   .. note::

      You should see a few entries in the logs since we closed and reopened **Firefox**.

   .. image:: images/doh-logging.png
      :align: left




Enable the *blackhole* mode on the DoH Guardian iRule to block any DoH requests that are categorized as *Sports*
---------------------------------------------------------------------------------------------------------------- 

By definition, a DNS blackhole essentially diverts a DNS client to nothing. A DNS blackhole will either drop the request entirely or respond with an NXDOMAIN. However, a browser that fails in getting a DoH response will almost always retry with regular DNS, making this a less effective option for blocking DoH queries. To properly blackhole a DoH request, the client must receive an actual response, but to something that does not exist. 

In this implementation, a DoH blackhole responds to the client with either a 199.199.199.199 IPv4 address for an A request, or 0:0:0:0:0:ffff:c7c7:c7c7 IPv6 address for a AAAA request.

|

#. Entry 1

Conclusion
----------

With the completion of this portion, please continue to the next lab to implement the *sinkhole* mode on the DoH Guardian Service.