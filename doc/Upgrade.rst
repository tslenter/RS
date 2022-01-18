6. Upgrade
==========

.. _upgrade:

6.1 Upgrade RSE core
---------------------

1) To upgrade the RSE core, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct core:

.. code-block:: console

   Option 1 => RSE Core installation
   Option 3 => Core upgrade

The upgrade for RSE core is now completed.

6.2 Upgrade RSC core
--------------------

1) To upgrade the RSC core, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct core:

.. code-block:: console

   Option 2 => RSC Core installation
   Option 3 => Core upgrade

The upgrade for RSC core is now completed.

6.3 Upgrade RSE webinterface
----------------------------

1) To upgrade the RSE webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct webinterface:

.. code-block:: console

   Option 4 => RSE webinterface installation
   Option 1 => Upgrade RSE WEB

The upgrade for RSE webinterface is now completed.

6.4 Upgrade RSC webinterface
----------------------------

Required core = RSE core

1) To upgrade the RSC webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct webinterface:

.. code-block:: console

   Option 3 => RSC webinterface installation
   Option 1 => Upgrade RSC WEB

The upgrade for RSC webinterface is now completed.

6.5 Upgrade RSX webinterface
----------------------------

Required core = RSE core

1) To upgrade the RSX webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct webinterface:

.. code-block:: console

   Option 5 => RSX webinterface installation
   Option 1 => Upgrade RSX WEB

The upgrade for RSX webinterface is now completed.

6.6 Upgrade RSL webinterface (Any project)
------------------------------------------

Required core = RSE core

Remote Syslog RSL clean allows you to upgrade a clean Laravel project for Remote Syslog.

1) To upgrade the RSL webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to remove the correct webinterface:

.. code-block:: console

   Option 6 => RSL devkit
   Option 3 => RSL Removal

3) Reinstall a project from backup, run:

.. code-block:: console

   rseinstaller

4) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 6 => RSL devkit
   Option 1 => RSL Backup

The upgrade for RSL webinterface is now completed.

6.7 Upgrade from legacy Remote Syslog
-------------------------------------

Manual remove Remote Syslog 1.x with the following bash script:

.. code-block:: console

   echo "File is only present if local syslog is activated"
   rm -rf /etc/syslog-ng/conf.d/99-remote-local.conf
   echo "Remove configuration files"
   rm -rf /etc/syslog-ng/conf.d/99-remote.conf
   rm -rf /etc/logrotate.d/remotelog
   rm -rf /etc/colortail/conf.colortail
   rm -rf /opt/remotesyslog
   echo "Remove binary files"
   rm -rf /usr/bin/rsview
   rm -rf /usr/bin/rsinstaller
   echo "Removing legacy GUI website …"
   rm -rf /var/www/html/favicon.ico
   rm -rf /var/www/html/index.php
   rm -rf /var/www/html/indexs.php
   rm -rf /var/www/html/jquery-latest.js
   rm -rf /var/www/html/loaddata.php
   echo "Remove packages …"
   apt -y purge apache2 apache2-utils php libapache2-mod-php syslog-ng colortail
   apt -y autoremove
   echo "Reinstall rsyslog"
   apt -y install rsyslog

After the removal of Remote Syslog 1.x, install the new RSX or RSC. The old syslog data is still available within the log folder /var/log/remote_syslog/.

More information over Remote Syslog 1.x: https://github.com/tslenter/Remote_Syslog

6.8 Upgrade to new distrobution
-------------------------------

Example: Upgrade from Ubuntu 18.04 to 20.04

This holds a upgrade to a new Ubuntu version and some known issues from that time. Those are fixed now.

Upgrade commands:

.. code-block:: console

   apt update && sudo apt upgrade

You probably run in a syslog-ng rdkafka error. This will stop the installation. Therefore we added "apt install -f".
This only effects version 3.27.1 and was fixed in 3.27.1-2.

.. code-block:: console

   apt install -f
   reboot
   apt install update-manager-core
   do-release-upgrade -d

It appears that the package "syslog-ng-mod-rdkafka" has some conflics with the core configuration, If you run in this error, try to uninstall this package:

.. code-block:: console
   
   #This only effects version 3.27.1 and was fixed in 3.27.1-2.
   apt remove syslog-ng-mod-rdkafka

After the upgrade there is a issue with the Apache2 configuration:
Edit the following file: /etc/apache2/mods-enabled/php7.2.load and change:

.. code-block:: console

   -LoadModule php7_module /usr/lib/apache2/modules/libphp7.2.so
   +LoadModule php7_module /usr/lib/apache2/modules/libphp7.4.so

Check to /var/log/syslog for errors. We found 2 errors and this depends on which platform you run the server.
Error 1 || DNS message:

.. code-block:: console

   Apr 30 20:56:22 lusysl003 systemd-resolved[923]: Server returned error NXDOMAIN, mitigating potential DNS violation DVE-2018-0001, retrying transaction with reduced feature level UDP

Recreate symlink will fix this issue:

.. code-block:: console

   ln -sfn /run/systemd/resolve/resolv.conf /etc/resolv.conf

or

.. code-block:: console
   
   rm /etc/resolv.conf
   ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

Error 2 || If you run the server on ESXi you get the following error:

.. code-block:: console

   Apr 30 12:47:53 plisk001.prd.corp multipathd[856]: sdb: add missing path
   Apr 30 12:47:53 plisk001.prd.corp multipathd[856]: sdb: failed to get udev uid: Invalid argument
   Apr 30 12:47:53 plisk001.prd.corp multipathd[856]: sdb: failed to get sysfs uid: Invalid argument
   Apr 30 12:47:53 plisk001.prd.corp multipathd[856]: sdb: failed to get sgio uid: No such file or directory

Edit the following file /etc/multipath.conf to fix this issue:

.. code-block:: console

   +blacklist {
   +    device {
   +        vendor "VMware"
   +        product "Virtual disk"
   +    }
   +}

After that restart the deamon:

.. code-block:: console

   systemctl restart multipath-tools

Reactivate repo:

.. code-block:: console

   wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -
   apt-get install apt-transport-https -y
   echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list
   echo "deb https://artifacts.elastic.co/packages/oss-7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list

   wget -qO - https://cloud.remotesyslog.com/xUbuntu_18.04/Release.key | /usr/bin/apt-key add -
   echo deb https://cloud.remotesyslog.com/xUbuntu_18.04 ./ > /etc/apt/sources.list.d/syslog-ng.list
   apt update
   apt install syslog-ng-mod-snmp syslog-ng-mod-freetds syslog-ng-mod-json syslog-ng-mod-mysql syslog-ng-mod-pacctformat syslog-ng-mod-pgsql syslog-ng-mod-snmptrapd-parser syslog-ng-mod-sqlite3
   sudo apt autoremove

6.9 Ubuntu upgrade policy
-------------------------

For Ubuntu we only test the latest LTS version. At the time of writing this is 20.04 LTS. The next release will be 22.04 LTS.