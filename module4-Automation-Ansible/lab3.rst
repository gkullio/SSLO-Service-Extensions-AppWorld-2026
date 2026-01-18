Example Ansible Playbooks
================================================================================

The |GitHub| SSLO API Reference repository contains sets of example playbooks to configure SSL Orchestrator:

- **Outbound Layer 3 Topology**

  - *sslo-config-ssl-outbound.yaml*: Deploys an Outbound Layer 3 Transparent Proxy Topology 
  - |outbound-l3-topology-link|: Outbound Layer 3 Transparent Proxy Topology Playbook

- **Outbound existing application Topology**

  - *config-sslo-existing-app-1sslo.yaml*: Deploy an SSL Orchestrator **existing application** configuration with Services, Service Chains, and Security Policy.
  - *config-sslo-existing-app-2ltm.yaml*: Deploy a simple LTM application (VIP, SSL Profiles, Pool) and attach the SSL Orchestrator **existing application** Security Policy.

- **Delete** Utility

  - *utility-sslo-delete-all.yaml*: Delete all SSL Orchestrator configuration objects.

- **Revoke license** Utility

  - *utility-revoke-license.yaml*: Revoke BIG-IP license so that it can be re-used.


.. |GitHub| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/tree/main" target="_blank"> GitHub </a>

.. |outbound-l3-topology-link| raw:: html

      <a href="https://github.com/f5devcentral/sslo-api-reference/blob/main/applications/sslo-config-ssl-outbound.yaml" target="_blank"> Outbound Layer 3 Transparent Proxy Topology Playbook </a>

