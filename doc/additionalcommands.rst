8. Additional commands
======================

.. _additionalcommands:

8.1 RSE Elasticsearch commands
------------------------------

8.1.1 Check the cluster health
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Comamnd:

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