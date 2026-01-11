Implement Sinkhole mode for DoH Guardian
========================================

We have confirmed **BIG-IP SSLO** can successfully *blackhole* DoH requests we deem necessary, we will now build upon the existing DoH Guardian Service Extension by adding the capability to sinkhole DoH requests. This will allow you to display a custom blocking page to the user when a DoH request matches a specified URL Category.

During this portion, we will perform the following tasks:
   - Understand how *sinkhole* differs from *blackhole*.
   - Download and run the Sinkhole installation script. 
   - Configure the **Sinkhole** mode on the DoH Guardian iRule to block any DoH requests that are categorized as *Sports* or *Information Technology*.
   - Test the new *sinkhole* finctionality by going to any site that is categorized as *Sports* or *Information Technology* by **BIG-IP SSLO**.


|

How does *sinkhole* mode work?
------------------------------

In a sinkhole response, the resolver sends back an IP address that points to a local blocking server. In contrast to a blackhole, a DNS sinkhole is diverting to something. The sinkhole destination is then able to respond to the client's request, so instead of just dying, the user might get a blocking page instead. In a DoH/DNS sinkhole without SSL Orchestrator, a client would initiate a TLS handshake to this server (believing it's the real site) and would get a certificate error because the server certificate on that blocking server doesn't match the Internet hostname requested by the client. 

The SSL Orchestrator solution requires two configurations:
   - A sinkhole internal virtual server that simply hosts the "blank" certificate that SSL Orchestrator will use to mint a trusted server certificate to the client.
   - An SSL Orchestrator outbound L3 topology modified to listen on the sinkhole destination IP and to inject the blocking response content.

Testing
-------
