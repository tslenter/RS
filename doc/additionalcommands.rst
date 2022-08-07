8. Additional commands
======================

.. _additionalcommands:

8.1 RSE Core commands
---------------------

8.1.1 Check the cluster health
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command:

.. code-block:: console

   curl -XGET -H "Content-Type: application/json" http://localhost:9200/_cluster/health?pretty=true
   
Expected output:

.. code-block:: console

   {
      "cluster_name" : "rsecore",
      "status" : "green",
      "timed_out" : false,
      "number_of_nodes" : 3,
      "number_of_data_nodes" : 3,
      "active_primary_shards" : 10,
      "active_shards" : 20,
      "relocating_shards" : 0,
      "initializing_shards" : 0,
      "unassigned_shards" : 0,
      "delayed_unassigned_shards" : 0,
      "number_of_pending_tasks" : 0,
      "number_of_in_flight_fetch" : 0,
      "task_max_waiting_in_queue_millis" : 0,
      "active_shards_percent_as_number" : 100.0
   }
   
8.1.2 Speed up lifecycly policy check
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to set it to 1 minute:

.. code-block:: console

   curl -XPUT --header 'Content-Type: application/json' http://localhost:9200/_cluster/settings --data '
   {
      "transient": {
        "indices.lifecycle.poll_interval": "1m"
      }
   }'

8.1.3 Set lifecycly policy to default 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to reset the policy:

.. code-block:: console

   curl -XPUT --header 'Content-Type: application/json' http://localhost:9200/_cluster/settings --data '
   {
      "transient": {
        "indices.lifecycle.poll_interval": null
      }
   }'

8.1.4 List indexes 
^^^^^^^^^^^^^^^^^^

Command to list the indexes:

.. code-block:: console

   curl -XGET 'localhost:9200/_cat/indices'

8.1.5 Check cluster diskspace 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to list the cluster diskspace:

.. code-block:: console

   curl -XGET 'localhost:9200/_cat/allocation?v&pretty'
   
8.1.6 Filter on host and time 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Adjust size for more results.

Command to filter on host and time:

.. code-block:: console

   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/rse*/_search -d '{ "query" : { "bool" : { "must": [ { "match": { "HOST_FROM": "172.16.30.1" } }, { "range": { "R_ISODATE": { "gte": "2022-01-13T22:45:39.493+00:00" } } } ] } } , "size": 3 }' | jq

8.1.7 View top 10 results 
^^^^^^^^^^^^^^^^^^^^^^^^^

Command to view top 10 messages:

.. code-block:: console

   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/rse*/_search?pretty
   
8.1.8 View the mapping of the fields 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to view mapping of the fields:

.. code-block:: console

   curl -X GET http://127.0.0.1:9200/rse*/_mapping?pretty
   
8.1.9 Search between times
^^^^^^^^^^^^^^^^^^^^^^^^^^

Adjust size for more results.

Command to view output between a start and top time:

.. code-block:: console
   
   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/rse*/_search -d '{ "query" : { "bool" : { "must": [ { "match": { "HOST_FROM": "172.16.30.1" } }, { "range": { "R_ISODATE": { "gte": "2022-01-13T22:45:39.493+00:00", "lte": "2022-01-17T22:45:39.493+00:00" } } } ] } } , "size": 3 }' | jq

8.1.10 Search uniq MAC adresses from DHCP index
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to view output of uniq MAC adresses from a DHCP index:

Requires logstash to index

.. code-block:: console

   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/logstash-rsx-dhcp*/_search?size=10000 -d '{ "query" : { "bool" : { "should": [ { "match": { "Host_Name": "*NUC00*" } }, { "range": { "@timestamp": { "gte": "now-1d/d" } } } ] } } }' | jq | grep MAC_Address | sort | uniq -d

8.1.11 View 2 exact terms 
^^^^^^^^^^^^^^^^^^^^^^^^^

Command to view multiple exact terms:

.. code-block:: console

   curl -X POST http://127.0.0.1:9200/rse*/_search -H 'Content-Type:application/json' -d '{
   "query": {
     "terms" : {
       "HOST_FROM" : [ "172.16.30.1", "172.16.30.24" ]
       }
     }
   }' | jq
   
8.1.12 View 1 exact term
^^^^^^^^^^^^^^^^^^^^^^^^

Command to view 1 exact term:

.. code-block:: console

   curl -X POST http://127.0.0.1:9200/rse*/_search -H 'Content-Type:application/json' -d  '{
   "query": {
     "term" : {
      "HOST_FROM" : "172.16.30.1"
      }
     }
   }' | jq

8.1.13 Flush indexes
^^^^^^^^^^^^^^^^^^^^

Command to start the flush process of an index makes sure that any data that is currently only persisted in the transaction log is also permanently persisted in Lucene.

.. code-block:: console

   curl -XPOST --header 'Content-Type: application/json' http://localhost:9200/_flush?wait_if_ongoing   

8.1.14 Delete index
^^^^^^^^^^^^^^^^^^^

Command to delete a single index:

Index = logstash-rsx-2020.03.28

.. code-block:: console   

   curl -XDELETE http://localhost:9200/logstash-rsx-2020.03.28 | jq

8.1.15 View license
^^^^^^^^^^^^^^^^^^^

Command to view the license:

.. code-block:: console
   
   curl -XGET 'http://localhost:9200/_license?pretty'
   
8.1.16 Lite search a value on multiple fields
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to filter a single value on all fields:

.. code-block:: console
   
   curl -XGET 'localhost:9200/_all/_search?q=172.16.30.1&pretty'

8.1.17 Lite search a single value for 1 field
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Command to filter a single value within 1 field:

.. code-block:: console
   
   curl -XGET 'localhost:9200/_all/_search?q=HOST_FROM:172.16.30.1&pretty'

8.1.18 Combined searches
^^^^^^^^^^^^^^^^^^^^^^^^

Command to exclude a value and filter down a host within a specific time range:

.. code-block:: console
   
   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/rse*/_search -d '{ "query" : { "bool" : { "must_not" : [ { "match" : { "PROGRAM" : "dhcpd" } } ], "filter" : [ { "term": { "HOST_FROM" : "172.16.30.1" } }, { "range": { "R_ISODATE": { "gte": "2022-08-06T10:13:00.000+00:00", "lte": "2022-08-06T10:20:00.000+00:00" } } } ] } } , "size": 300 }' | jq
   
Command to exclude a value and filter down multiple hosts within a specific time range:

.. code-block:: console

   curl -XGET --header 'Content-Type: application/json' http://localhost:9200/rse*/_search -d '{ "query" : { "bool" : { "must_not" : [ { "match" : { "PROGRAM" : "dhcpd" } } ], "filter" : [ { "terms": { "HOST_FROM" : [ "172.16.30.1", "172.16.30.24" ] } }, { "range": { "R_ISODATE": { "gte": "2022-08-06T10:13:00.000+00:00", "lte": "2022-08-06T10:20:00.000+00:00" } } } ] } } , "size": 300 }' | jq
  
8.2 RSC Core commands
---------------------

8.2.1 Search multiple strings of text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   grep -h "switch1\|switch2\|switch3" /var/log/remote_syslog/* | more
   
8.2.2 Search for the top 15 messages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   egrep -o "%.+?: "/var/log/remote_syslog/remote_syslog.log | sort | uniq -c | sort -nr | head -n 15

8.3 Unsupported commands
---------------------

8.3.1 Disable NTP and change date
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   timedatectl set-time '2022-01-20'
   timedatectl set-ntp 0
