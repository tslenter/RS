2. Installation instuctions
============================

.. _installation:

2.1 Installation RSE core
-------------------------

1) To use RSE core, download the masterscript:

.. code-block:: console

   git clone https://www.github.com/tslenter/RS

2) Run the RSE installation

Run the script masterscript as follows:

.. code-block:: console

   cd RS
   sudo ./rseinstaller

3) Select the following options to install the correct core:

.. code-block:: console

   Option 1 => RSE Core installation
   Option 1 => Core installation

The installation for RSE core is now completed.

2.2 Installation RSC core
-------------------------

Required core = RSC core

1) To use RSC core, download the masterscript:

.. code-block:: console

   git clone https://www.github.com/tslenter/RS

2) Run the RSC installation

Run the script masterscript as follows:

.. code-block:: console

   cd RS
   sudo ./rseinstaller

3) Select the following options to install the correct core:

.. code-block:: console

   Option 2 => RSC Core installation
   Option 1 => Core installation

The installation for RSE core is now completed.

2.3 Installation RSE webinterface
---------------------------------

1) To install the RSE webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 4 => RSE webinterface installation
   Option 2 => Install RSE WEB

The installation for RSE webinterface is now completed.

2.4 Installation RSC webinterface
---------------------------------

Required core = RSE core

1) To install the RSC webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 3 => RSC webinterface installation
   Option 2 => Install RSC WEB

The installation for RSC webinterface is now completed.

2.5 Installation RSX webinterface
---------------------------------

Required core = RSE core

1) To install the RSX webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 5 => RSX webinterface installation
   Option 2 => Install RSX WEB

The installation for RSX webinterface is now completed.

2.6 Installation RSL webinterface (Clean project)
-------------------------------------------------

Required core = RSE core

Remote Syslog RSL clean allows you to install a clean Laravel project for Remote Syslog.

1) To install the RSL webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 6 => RSL devkit
   Option 2 => RSL Clean

The installation for RSL webinterface is now completed.

2.7 Installation RSL webinterface (Backup project)
--------------------------------------------------

Required core = RSE core

Remote Syslog RSL backup allows you to restore a Laravel project for Remote Syslog.

1) To install the RSL webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to install the correct webinterface:

.. code-block:: console

   Option 6 => RSL devkit
   Option 1 => RSL Backup

The installation for RSL webinterface is now completed.

2.8 Installation RSE Docker for Synology
----------------------------------------

Login to the Synlogy console. Usually found: https://<nas_ip>:5000

2.8.1 Download image
^^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_download_image.png?raw=true
   :width: 400
   :align: center

Search and download as show in the image above.

2.8.2 Install image
^^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_install_image.png?raw=true
   :width: 400
   :align: center

Press launch(start) as show in the image above to install the RSE image.

2.8.3 Configure network
^^^^^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_create_network_settings.png?raw=true
   :width: 400
   :align: center

Add the network ports as in the image above to configure the right forwarding.

2.8.4 Check summary
^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_overview.png?raw=true
   :width: 400
   :align: center

Check the setting. The image above has the correct values. The container auto-starts.

2.8.5 Known error afer apply
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If this error is not shown to you, please skip this section.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_port_use_error.png?raw=true
   :width: 400
   :align: center

Edit the port settings as following:

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_change_setting_error.png?raw=true
   :width: 400
   :align: center
   
Stop the container within the Synology GUI.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_start_stop_container.jpg?raw=true
   :width: 400
   :align: center
   
After this login to the CLI of the Synology NAS and search for the following file:

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_find_configuration_file.png?raw=true
   :width: 400
   :align: center
   
Edit the file as following and change the port 513 to 514:

.. code-block:: console

   vi /volume4/@docker/containers/73a981a58c43e92b8bd26226094d830d746244fa211f68e31748f2c446a963fa/hostconfig.json

   {
     "Binds": [],
     "ContainerIDFile": "",
     "LogConfig": {
       "Type": "db",
       "Config": {}
     },
     "NetworkMode": "bridge",
     "PortBindings": {
       "443/tcp": [
         {
           "HostIp": "",
           "HostPort": "8000"
         }
       ],
       "514/tcp": [
         {
           "HostIp": "",
           "HostPort": "514" <<<==
         }
       ],
       "514/udp": [
         {
           "HostIp": "",
           "HostPort": "514" <<<<==
         }
       ]
     },

Restart the Synology services:

Synology version 6.x:

.. code-block:: console

   synoservice --restart pkgctl-Docker
   
Synology version 7.x:

.. code-block:: console

   sudo synopkgctl stop Docker
   sudo synopkgctl start Docker 

After this configuration start the container within the webinterface of the Synology NAS.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/docker_start_stop_container.jpg?raw=true
   :width: 400
   :align: center

2.8.6 Known limitation
^^^^^^^^^^^^^^^^^^^^^^

Due the bridge interface the source is displayed as the bridge interface.

2.8.7 Default login
^^^^^^^^^^^^^^^^^^^

The web interface is available @ https://<nas_ip>:8000. The default login is: Username "test" and the password is "Test123!"

To change the user use the reseview tool within the docker container. (CLI)

2.9 Docker image creation from scratch
--------------------------------------

Example is given for Remote Syslog RSE.

2.9.1 Create docker image
^^^^^^^^^^^^^^^^^^^^^^^^^

Download the ubuntu image from the registered images.

And run the following commands:

.. code-block:: console

   apt update && apt upgrade -y
   apt install lsb-release wget dialog wget git apt-utils gnupg2 -y
   git clone https://www.github.com/tslenter/RS
   cd RS
   ./rseinstaller
   
Change the following file:

.. code-block:: console

   vi /etc/elasticsearch/elasticsearch.yml
   
   add: 
   
   xpack.ml.enabled: false
   
2.9.1 Create docker image
^^^^^^^^^^^^^^^^^^^^^^^^^

Example code to create a docker image:

.. code-block:: console

   docker commit --message "Remote Syslog RSE for Synology ..." --author tom.slenter@remotesyslog.com RSDOCK001
   docker images
   docker tag 86bc8a78b689 tslenter/remote_syslog_rse_web
   docker login --username=<username>
   docker push <username>/remote_syslog_rse_web:latest
