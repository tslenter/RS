X. FAQ
======

x.x My RSX/RSE installation does not recieve any logging
--------------------------------------------------------

You probably should check the date. If the date is not correct run in the CLI as root:

.. code-block:: console

   dpkg-reconfigure tzdata

This allows you to configure the timezone.

The next thing to check is within the Kibana console: Management => Advanced Settings => Timezone for date formatting => setup the right timezone.