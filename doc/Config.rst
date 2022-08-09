9. Configuration Files
=======================

.. _Config:

9.1 Config files locations
--------------------------

9.1.1 Default RSC Core configuration/files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   Syslog-ng global config:       /etc/syslog-ng/syslog-ng.conf
   Syslog-ng additional configs:  /etc/syslog-ng/conf.d/99*
   Logrotate:                     /etc/logrotate.d/remotelog
   Syslog-ng logrotate:           /etc/logrotate.d/syslog-ng
   Colortail global:              /opt/remotesyslog/colortail
 
9.1.2 Default RSE Core configuration/files:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   Syslog-ng global config:       /etc/syslog-ng/syslog-ng.conf
   Syslog-ng additional configs:  /etc/syslog-ng/conf.d/99*   
   Elasticsearch global config:   /etc/elasticsearch/elasticsearch.yml  
   
9.1.3 Default RSX web configuration/files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   Kibana global config:          /etc/kibana/kibana.yml
   
9.1.4 Default Plugin configuration/files:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   Filebeat global:               /etc/filebeat/filebeat.yml
   Filebeat Cisco:                /etc/filebeat/modules.d/cisco.yml
   Filebeat netflow:              /etc/filebeat/modules.d/netflow.yml
   Logstash global config:        /etc/logstash/logstash.yml
   Logstash additional configs:   /etc/logstash/conf.d/99*
   
9.2 Config checks
-----------------

9.2.1 Logstash test new config
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   /usr/share/logstash/bin/logstash --config.test_and_exit -f /etc/logstash/conf.d/97-rsmdefault.conf --path.settings /etc/logstash/
