Deploy DoH Guardian Configuration Objects
=========================================

|

The **Serivce Extension** DNS-over-HTTPS (**DoH**) Guardian provides the functionality to detect DoH requests and apply policies for logging, management, and anomaly detection. There is a one-line script that we will use to deploy the necessary objects.

- The script creates the following objects:

asdfasdfa

|

Download the installation script
--------------------------------

#. From the UDF **Deployment** tab, access the web shell of the **BIG-IP SSLO** resource. This will open a new browser tab with an SSH session (logged in as the **root** user).

   .. image:: images/udf-sslo-webshell-1.png
      :align: left


#. Change Directory to the /tmp directory:

   .. code-block:: text

      cd /tmp


#. Download the installation script:

   .. code-block:: text
 
      curl -sk https://raw.githubusercontent.com/f5devcentral/sslo-service-extensions/refs/heads/main/doh-guardian/doh-guardian-installer.sh -o doh-guardian-installer.sh


   .. tip::

      Click the **copy** icon in the URL text box above and paste it into the **BIG-IP SSLO - Web Shell** session. If your local machine is Windows, press the <CTRL>-<SHIFT>-V combination to paste.

|

Run the Installation Script
----------------------------

#. Make the installation script executable:

   .. code-block:: text

      chmod +x doh-guardian-installer.sh


#. Create a BASH environment variable containing the BIG-IP username and password:

   .. code-block:: text

      export BIGUSER='admin:admin'


#. Run the installation script to create all of the DoH Guardian objects:

   .. code-block:: text

      ./doh-guardian-installer.sh


   .. image:: images/udf-doh-guardian-install.png
      :align: left


Verify Object Creation
----------------------