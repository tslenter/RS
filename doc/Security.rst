10. Security
============

.. _security:

10.1 Certificate location and replacement
-----------------------------------------

All external connections are encrypted with TLS/SSL, this includes the API on port 8080, SSH and HTTP for user login. 

To update the certificates for Apache 2, copy the new certificates to the following directory:

.. code-block:: console

   /etc/cert/

After you copied the new certificates, update the apache2 configuration. File location:

.. code-block:: console

   /etc/apache2/sites-enabled/

Check for the lines:

.. code-block:: console

    SSLCertificateKeyFile /etc/cert/rs.key
    SSLCertificateFile /etc/cert/rs.crt

Replace the path with the uploaded certificate.

Reload configuration to apply:

.. code-block:: console

   service apache2 restart

10.2 RS4LOGJ-CVE-2021-44228
---------------------------

Apache Log4j vulnerability - CVE-2021-44228 instructions for Remote Syslog:

Remote Syslog uses the Elasticsearch module to save logging.

Effected products: RSL, RSE and RSX.

RSC is not effected.

10.2.1 Upgrade to recommended version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Check version:

.. code-block:: console

   curl -XGET 'http://localhost:9200'

Output:

.. code-block:: console

   "number" : "7.16.2"

or 

.. code-block:: console

   "number" : "6.8.22"

Official document Elasticsearch: 

.. code-block:: console

   https://www.elastic.co/blog/new-elasticsearch-and-logstash-releases-upgrade-apache-log4j2

All versions below: 7.16.2 or 6.8.22 are vulnerable. If the version is higher you are good to go and no action is needed.

Upgrade instuction to Elasticsearch 7.16.2 or 6.8.22:

1) In case of a vitual machine create a snapshot

2) Run the upgrade:

.. code-block:: console

   sudo apt update && sudo apt upgrade

!!Please check if the recommended version or higher is going to be installed!!

10.2.2 Mitigation without upgrade
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Edit:

.. code-block:: console

   nano /etc/elasticsearch/jvm.options

Add: 

.. code-block:: console

   -Dlog4j2.formatMsgNoLookups=true

Restart elasticsearch service:

.. code-block:: console

   service elasticsearch restart