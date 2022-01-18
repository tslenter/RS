7. Additional configuration
===========================

.. _additionconfiguration:

7.1 Active Directory integration via PAM
----------------------------------------

Run commands as root:

.. code-block:: console

   su -

Upgrade distro:

.. code-block:: console

   apt-get update && apt upgrade -y

Install packages:

.. code-block:: console

   apt-get install realmd packagekit sssd-tools sssd libnss-sss libpam-sss adcli oddjob oddjob-mkhomedir adcli samba-common ntpdate ntp unzip resolvconf git -y

Enable DNS service:

.. code-block:: console

   systemctl start resolvconf.service
   systemctl enable resolvconf.service
   systemctl status resolvconf.service

Configure DNS service:

.. code-block:: console
   
   nano /etc/resolvconf/resolv.conf.d/head

Add:

.. code-block:: console
   
   nameserver <ip dnsserver domeincontroller>

Reload DNS service:

.. code-block:: console
   
   systemctl restart resolvconf.service

Check if domain controller connection:

.. code-block:: console
   
   ping dom001.lan.local

Join controller:

.. code-block:: console
   
   realm join --user=administrator lan.local --verbose

Expected output:

.. code-block:: console
   
   * Successfully enrolled machine in realm

Edit sssd deamon:

.. code-block:: console
   
   nano /etc/sssd/sssd.conf

Edit configuration:

.. code-block:: console

   [sssd]
   domains = LAN.LOCAL
   config_file_version = 2
   services = nss, pam, sudo
   default_domain_suffix = lan.local
   full_name_format = %1$s

   [domain/lan.local]
   ad_domain = lan.local
   krb5_realm = LAN.LOCAL
   realmd_tags = manages-system joined-with-adcli
   cache_credentials = True
   id_provider = ad
   krb5_store_password_if_offline = True
   default_shell = /bin/bash
   ldap_id_mapping = True
   use_fully_qualified_names = True
   fallback_homedir = /home/%u@%d
   #Restict AD search:
   #ldap_search_base = DC=lan,DC=local
   #ldap_user_search_base OU=Power Users,OU=Accounts,DC=lan,DC=local
   #ldap_group_search_base OU=Groups,DC=lan,DC=local
   access_provider = simple
   simple_allow_groups = <ad group 1>, <ad group 2>
   manage-system = yes
   automatic-id-mapping = yes

Reload sssd deamon:

.. code-block:: console

   service sssd restart

Configure PAM to auto create home folder:

.. code-block:: console

   nano /etc/pam.d/common-session

Add:

.. code-block:: console

   session    required    pam_mkhomedir.so skel=/etc/skel/ umask=0022

Grant root rights (only ubuntu):

.. code-block:: console

   nano /etc/sudoers

Add:

.. code-block:: console

   %<add ad group here> ALL=(ALL:ALL) ALL


To add a additional group use the following command:

.. code-block:: console

   realm permit -g <groepnaam>@lan.local

Secure apache2 login:

.. code-block:: console

   nano /etc/apache2/sites-enabled/rsx-apache.conf

Change the following configuration:

.. code-block:: console

   #Change in all 3 location blocks:
                   Require valid-user
                   #Require user user1 user2 user3
   #To:
                   #Require valid-user
                   Require user test01 <<-- username

Reload apache2 services:

.. code-block:: console

   service apache2 restart
   
7.2 Integrate Active Directory LDAP authentication for Apache 2
---------------------------------------------------------------

Activate LDAP module apache:

.. code-block:: console

   a2enmod ldap authnz_ldap

Configure /etc/apache2/apache2.conf as following:

.. code-block:: console

   <Directory /var/www/html>
   AuthType Basic
   AuthName "Remote Syslog Login"
   Options Indexes FollowSymLinks
   AllowOverride None
   AuthBasicProvider ldap
   AuthLDAPGroupAttributeIsDN On
   AuthLDAPURL "ldap://<myadhost>:389/dc=DC01,dc=local?sAMAccountName?sub?(objectClass=*)"
   AuthLDAPBindDN "CN=,OU=Accounts,DC=DC01,DC=local"
   AuthLDAPBindPassword
   AuthLDAPGroupAttribute member
   require ldap-group cn=,ou=Groups,dc=DC01,dc=local
   </Directory>

Reload apache2 services:

.. code-block:: console

   service apache2 restart

7.3 Basic authentication for Apache 2
-------------------------------------

Install apache2-utils:

.. code-block:: console

   apt-get install apache2-utils

Create .htpasswd file:

.. code-block:: console

   htpasswd -c /etc/apache2/.htpasswd <myuser>

Configure /etc/apache2/apache2.conf as following:

.. code-block:: console

   <Directory /var/www/html>
   AuthType Basic
   AuthName "Remote Syslog Login"
   AuthBasicProvider file
   AuthUserFile "/etc/apache2/.htpasswd"
   Require user
   Options Indexes FollowSymLinks
   AllowOverride None
   Require valid-user
   Order allow,deny
   Allow from all
   </Directory>

Reload apache2 services:

.. code-block:: console

   service apache2 restart

7.4 Generate an email from an event (Only RSC)
----------------------------------------------

Required core = RSC core

Install netsend:

.. code-block:: console

   sudo apt install sendmail

Edit:

.. code-block:: console

   /etc/mail/sendmail.cf

Search for => #"Smart" relay host (may be null)

Change after DS => DSsmtp.lan.corp

Use the following script and save it to /opt/mailrs:

Create array:

.. code-block:: console

   #!/bin/bash
   #Array of words:
   declare -a data=(Trace module)

Check if error messages exist:

.. code-block:: console

   for word in "${data[@]}"; do
       mesg=$(cat /var/log/remote_syslog/remote_syslog.log | grep "^$(date +'%b %d')" | grep $word)
       if [ -z "$mesg" ]
       then
           echo "No variable!"
       else
           echo "Variable filled, setting variable to continue …"
           mesgall=1
       fi
   done

Generate email:

.. code-block:: console

   if [ -z "$mesgall" ]
   then
       echo "Nothing to do, abort"
       exit
   else
       echo "Subject: Syslog critical errors" > /opt/rs.txt
       echo "" >> /opt/rs.txt
       echo "Hello <user>," >> /opt/rs.txt
       echo "" >> /opt/rs.txt
       echo "The following message is generated by Remote Syslog." >> /opt/rs.txt
       echo "" >> /opt/rs.txt
       for word in "${data[@]}"; do
           cat /var/log/remote_syslog/remote_syslog.log | grep "^$(date +'%b %d')" | grep $word >> /opt/rs.txt
       done
       echo "" >> /opt/rs.txt
       echo "The messages above are generated by the <hostname>!" >> /opt/rs.txt
       echo "" >> /opt/rs.txt
       echo "Thank you for using Remote Syslog … ;-)" >> /opt/rs.txt
       cat /opt/rs.txt
       /usr/sbin/sendmail -v -F "T.Slenter" -f "info@mydomain.com" ticketsystem@domain.com < /opt/rs.txt
   fi


Make file executable:

.. code-block:: console
   
   chmod +x /opt/mailrs


Install with cron:
Command:

.. code-block:: console
   
   crontab -e

Edit:

.. code-block:: console

   0 * * * * /opt/mailrs