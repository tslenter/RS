11. FAQ
=======

11.1 My RSX/RSE installation does not recieve any logging
---------------------------------------------------------

You probably should check the date. If the date is not correct run in the CLI as root:

.. code-block:: console

   dpkg-reconfigure tzdata

This allows you to configure the timezone.

The next thing to check is within the Kibana console: Management => Advanced Settings => Timezone for date formatting => setup the right timezone.

11.2 Disk full by Geo2
----------------------

Message in logging:

.. code-block:: console

   Jan 27 10:24:50 plisk002.prd.corp syslog-ng[1793]: geoip2(): getaddrinfo failed; gai_error='Name or service not known', ip='', location='/etc/syslog-ng/conf.d/99X-Checkpoint.conf:32:25'
   Jan 27 10:24:50 plisk002.prd.corp syslog-ng[1793]: geoip2(): maxminddb error; error='Unknown error code', ip='', location='/etc/syslog-ng/conf.d/99X-Checkpoint.conf:32:25'

Components needed for fix:

.. code-block:: console

   File: /etc/syslog-ng/syslog-ng.conf

File destinations: 

.. code-block:: console

   - d_syslog
   - d_error

Log rules:

.. code-block:: console

   - log { source(s_src); filter(f_syslog3); destination(d_syslog); };
   - log { source(s_src); filter(f_error); destination(d_error); };

Fix:

.. code-block:: console

   vi /etc/syslog-ng/syslog-ng.conf

Add rules:

.. code-block:: console

   filter geoip_messages_1 { not match("Name or service not known"); };
   filter geoip_messages_2 { not match("Unknown error code"); };

Change rules:

.. code-block:: console

   -log { source(s_src); filter(f_syslog3); destination(d_syslog); };
   -log { source(s_src); filter(f_error); destination(d_error); };
   +log { source(s_src); filter(f_syslog3); filter(geoip_messages_1); filter(geoip_messages_2); destination(d_syslog); };
   +log { source(s_src); filter(f_error); filter(geoip_messages_1); filter(geoip_messages_2); destination(d_error); };

11.3 Kibana not loaded after upgrade
------------------------------------

Restarting the server will solve this problem. Some report that a restart of the Kibana or Elasticsearch will fix the issue.

.. code-block:: console

   service elasticsearch restart
   service kibana restart

11.4 Data too large, data for [<http_request>] (JVM heap size)
--------------------------------------------------------------

Error message:

.. code-block:: console

   tom@plisx002:~$ curl -X GET 'http://localhost:9200/_cat/health?v'
   {"error":{"root_cause":[{"type":"circuit_breaking_exception","reason":"[parent] Data too large, data for [<http_request>] would be [1014538592/967.5mb], which is larger than the limit of [986061209/940.3mb], real usage: [1014538592/967.5mb], new bytes reserved: [0/0b], usages [request=0/0b, fielddata=3057213/2.9mb, in_flight_requests=0/0b, accounting=261018719/248.9mb]","bytes_wanted":1014538592,"bytes_limit":986061209,"durability":"PERMANENT"}],"type":"circuit_breaking_exception","reason":"[parent] Data too large, data for [<http_request>] would be [1014538592/967.5mb], which is larger than the limit of [986061209/940.3mb], real usage: [1014538592/967.5mb], new bytes reserved: [0/0b], usages [request=0/0b, fielddata=3057213/2.9mb, in_flight_requests=0/0b, accounting=261018719/248.9mb]","bytes_wanted":1014538592,"bytes_limit":986061209,"durability":"PERMANENT"},"status":429}

Increase memory fix:

.. code-block:: console

   nano /etc/elasticsearch/jvm.options

Edit:
.. code-block:: console

   --Xms1g
   --Xmx1g
   +-Xms6g
   +-Xmx6g

11.5 Syslog-NG 3.27.1 breaks with new upgrade on Ubuntu 18.04 and 20.04
-----------------------------------------------------------------------

Error message:

.. code-block:: console

   dpkg: error processing package syslog-ng-mod-sql (--configure):
    dependency problems - leaving unconfigured
   dpkg: dependency problems prevent configuration of syslog-ng-mod-redis:
    syslog-ng-mod-redis depends on syslog-ng-core (>= 3.27.1-2); however:
     Package syslog-ng-core is not configured yet.
    syslog-ng-mod-redis depends on syslog-ng-core (<< 3.27.1-2.1~); however:
     Package syslog-ng-core is not configured yet.

Fix:

Backup configuration:

.. code-block:: console

   mkdir ~/syslog-ng_backup/
   cp -rf /etc/syslog-ng/* ~/syslog-ng_backup/

Verify configuration:

.. code-block:: console

   ls ~/syslog-ng_backup/

Purge syslog-ng and remove everything:

.. code-block:: console

   sudo apt purge syslog-ng-core

If some files remain, delete them all:

.. code-block:: console

   rm -rf /etc/syslog-ng

Reinstall syslog-ng-core:

.. code-block:: console

   sudo apt install syslog-ng-core

Reinstall syslog-ng:

.. code-block:: console

   sudo apt install syslog-ng

Cleanup some packages:

.. code-block:: console

sudo apt auto-remove

Restore RS configuration files:

.. code-block:: console

   cp ~/syslog-ng_backup/conf.d/99* /etc/syslog-ng/conf.d/

If you edited the /etc/syslog-ng/syslog-ng.conf file, check the difference and restore your custom configuration.

This issue should be fixed in version 3.27.1-2.1 and higher.