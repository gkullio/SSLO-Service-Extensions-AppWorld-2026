Deploy SaaS Tenant Isolation Objects
================================================================================

SaaS Tenant Isolation Script
--------------------------------------------------------------------------------

**SaaS Tenant Isolation** functionality is a Service Extension for SSL Orchestrator. An installation script automates the creation of the configuration objects needed to implement this functionality.

The script creates the following objects:

   - F5_SaaS-Tenant-Isolation Inspection Service - the SaaS Tenant Isolation Service Extension to interact with decrypted traffic flows.
   - SaaS Tenant Isolation iRule - injects the SaaS Tenant Isolation prompts, as well as optional logging.

Download the Installation Script
--------------------------------------------------------------------------------

#. From the UDF **Deployment** tab, access the Web Shell of the **BIG-IP SSL Orchestrator** resource. This will open a new browser tab with an SSH session (logged in as the **root** user).

   .. image:: images/udf-sslo-webshell-1.png
      :align: left


#. Download the installation script:

   .. code-block:: text

      cd /tmp

      curl -sk https://raw.githubusercontent.com/f5devcentral/sslo-service-extensions/refs/heads/main/saas-tenant-isolation/saas-tenant-isolation-installer.sh -o saas-tenant-isolation-installer.sh


   .. tip::

      Click the **copy** icon in the URL text box above and paste it into the **BIG-IP SSLO - Web Shell** session. If your local machine is Windows, press the <CTRL>-<SHIFT>-V combination to paste.


Run the Installation Script
--------------------------------------------------------------------------------

#. Make the installation script executable:

   .. code-block:: text

      chmod +x saas-tenant-isolation-installer.sh


#. Create a BASH environment variable containing the BIG-IP username and password:

   .. code-block:: text

      export BIGUSER='admin:admin'


#. Run the installation script to create all of the SaaS Tenant Isolation objects:

   .. code-block:: text

      ./saas-tenant-isolation-installer.sh


   .. image:: images/udf-sslo-webshell-2.png
      :align: left
