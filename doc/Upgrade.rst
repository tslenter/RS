5. Upgrade
==========

.. _upgrade:

5.1 Upgrade RSE core
---------------------

1) To upgrade the RSE core, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct core:

.. code-block:: console

   Option 1 => RSE Core installation
   Option 3 => Core upgrade

The upgrade for RSE core is now completed.

5.2 Upgrade RSC core
--------------------

1) To upgrade the RSC core, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct core:

.. code-block:: console

   Option 2 => RSC Core installation
   Option 3 => Core upgrade

The upgrade for RSC core is now completed.

5.3 Upgrade RSE webinterface
----------------------------

1) To upgrade the RSE webinterface, run:

.. code-block:: console

   rseinstaller

2) Select the following options to upgrade the correct webinterface:

.. code-block:: console

   Option 4 => RSE webinterface installation
   Option 1 => Upgrade RSE WEB

The upgrade for RSE webinterface is now completed.

5.4 Upgrade RSC webinterface
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

5.5 Upgrade RSX webinterface
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

5.5 Upgrade RSL webinterface (Any project)
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