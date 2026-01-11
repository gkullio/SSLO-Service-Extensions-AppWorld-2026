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

      **Please do not change anything at this time.** Take this time to review the notes and comments in each section to understand the functionality of the iRule.

#. Look at lines 40 - 44, and 54 - 58. These are the sections that control *blackhole* and *sinkhole* mode.



Add the DoH Guardian Service to the existing Service Chain
----------------------------------------------------------

|

Configure the Firefox browser in the Ubuntu-Client to use Google's DoH server
-------------------------------------------------------------------------------

|

#. Entry 1

Test the DoH Guardian Service Extension *blackhole* functionality
-------------------------------------------------------------------------

|

#. Entry 1

Enable the *blackhole* mode on the DoH Guardian iRule to block any DoH requests that are categorized as *Sports*
---------------------------------------------------------------------------------------------------------------- 

By definition, a DNS blackhole essentially diverts a DNS client to nothing. A DNS blackhole will either drop the request entirely or respond with an NXDOMAIN. However, a browser that fails in getting a DoH response will almost always retry with regular DNS, making this a less effective option for blocking DoH queries. To properly blackhole a DoH request, the client must receive an actual response, but to something that does not exist. 

In this implementation, a DoH blackhole responds to the client with either a 199.199.199.199 IPv4 address for an A request, or 0:0:0:0:0:ffff:c7c7:c7c7 IPv6 address for a AAAA request.

|

#. Entry 1

Conclusion
----------

With the completion of this portion, please continue to the next lab to implement the *sinkhole* mode on the DoH Guardian Service.