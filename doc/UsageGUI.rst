4. Usage GUI
============

.. _UsageGUI:

4.1 GUI Requirements
--------------------

.. code-block:: console

   RSE Core is required for RSX and RSE.
   RSC Core is required for for RSC.

4.2 RSE GUI usage
-----------------

Documentation is build for RSE version 0.1.

4.2.1 RSE Login
^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_login.jpg?raw=true
   :width: 300
   :align: center
   :alt: image 1

Above image shows the default login. which can be found with the following url: https://<ip-of-server>/. To login use the account what was used during the installation.
The password requires the following:

.. code-block:: console

   - Minimum of 4 characters
   - Minimum of 1 capital letter
   - Minimum of 1 special characters (!, @, #, $, %, ^, &, *, _, =, +, -)

4.2.2 RSE dashboard
^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_dashboard.jpg?raw=true
   :width: 400
   :align: center

Above image shows the dashboard and it contains the top 10 stats with a heath indicator of the elasticsearch engine.
   
4.2.3 RSE text viewer
^^^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_text_screen.jpg?raw=true
   :width: 400
   :align: center
   
The image above gives the default view after the login. Here you can search end view live logging.

4.2.3 RSE menu
^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_menu.jpg?raw=true
   :width: 800
   :align: center
   
The image above displays the menu. Select "Dashboard" to view the dashboard page. "Options" holds some more additions configurations. "Logout" logs the connected user out. 
   
4.2.4 RSE options
^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_menu_dropdown.jpg?raw=true
   :width: 400
   :align: center
   
Within the option menu there are 3 option. "Test message" sends a UPD and TCP test message to the system. "Clear live log archive" clears all logging from the server.
"License" redirects you to the license page of Remote Syslog.

4.2.5 RSE searchbar
^^^^^^^^^^^^^^^^^^^

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/rse_searchbar.jpg?raw=true
   :width: 800
   :align: center
   
The searchbar allows to search live logging on fields, regex and on text strings. It buffer field allows to give any number between 0 and 3000 to limit or extend search results.

The buttons:

1) The "search" button allows you to view the live logging with ot without a searchstring or buffer value.
2) The "stop" button stop the live logging with or without a searchsting or buffer value.
3) The "redo" button loads the default settings and the live logging strats scolling without buffer and searchsting.
4) The "download" button exports the text to a HTML file.

4.2.6 RSE searchbar example searchstrings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default 3 fields are used by RSE. These are:

1) MESSAGE
2) DATE
3) HOST_FROM

.. list-table:: Search options
   :widths: 40 40 20 
   :header-rows: 1

   * - What:
     - Command:
     - Tested:
   * - MAC address:
     - \\\'24\\\\:5a\\\\:4c\\\\:1e\\\\:a3\\\\:dc\\\
     - V
   * - Search on a field:
     - MESSAGE: com*
     - V
   * - Use wildcard:
     - com*
     - V