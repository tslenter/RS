3. Usage CLI
============

RSE CLI is usable for RSX and RSE.
RSC CLI is only usable for RSC.

.. _usage:

3.1 RSE viewer (rseview)
------------------------

.. code-block:: console
   
   Usage rseview:

   -h,--help                                       Display help
   -s,--search <search string> <buffer>            Search through logging
   -v,--view <buffer>                              View logging
   -l,--live <buffer>                              View live logging
   -ls,--livesearch <search string> <buffer>       Search through live logging
   -t,--testmessage                                Send a test message
   -c,--clearlog                                   Clear log index
   -p,--lifecyclepolicy                            Change lifecycle policy
   -ps,--pslifecyclepolicy                         View lifecycle policy
   -xi,--indexinfo                                 View indexes
   -xh,--healthinfo                                View elasticsearch health
   -u,--usage                                      View disk / ram usage

   
3.1.1 Display help
^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -h
  
Displays help menu with all available options.


3.1.2 Display logging with search string
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -s mysearch 90

Displays logging with the given search string. Output will be given in the console. Buffer of 90 gives the latest 90 results.


3.1.3 Display logging
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -v 90

Displays the latest logging. Output will be given in the console. Buffer of 90 gives the latest 90 results. Buffer is default 50.


3.1.4 Display live logging
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -l 90

Displays live logging. Output will be given in the console. Buffer of 90 gives the latest 90 results. Buffer is default 50.


3.1.5 Display live logging with search string
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -ls mysearch 90

Displays live logging with the given search string. Output will be given in the console. Buffer of 90 gives the latest 90 results. Buffer is default 50.


3.1.6 Generate test message
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -t

Generates a test message. Run "rseview -s test" to check if it was successfull.


3.1.7 Clear all logging
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -c

Clears all logging. Output will be given in the console.


3.1.8 Change policy
^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -p
   
Sets a new lifecycly plocicy for the elasticsearch remote syslog index. Data is given in day and gigabyte. Output will be given in the console.


3.1.9 Display policy
^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -ps
   
Displays the lifecycle policy. Output will be given in the console.


3.1.10 Display index / shard info
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -xi
   
Displays index / shard info. Output will be given in the console.


3.1.11 Display cluster / server info
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -xh
   
Displays cluster / server info. Output will be given in the console.


3.1.12 Display usage
^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseview -u
   
Displays disk and RAM info. Output will be given in the console.

3.2 RSC viewer (rsview)
-----------------------

.. code-block:: console
   
   Usage rsview:

   -h,--help                          Display help
   -s,--search <search string>        Search through logging
   -v,--view                          View logging
   -l,--live                          View live logging
   -ls,--livesearch <search string>   Search through live logging
   -t,--testmessage                   Send a test message
   -c,--clearlog                      Clear total log archive

3.2.1 Display help
^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -h
  
Displays help menu with all available options.


3.2.2 Display logging with search string
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -s mysearch

Displays logging with the given search string. Output will be given in the console. 


3.2.3 Display logging
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -v

Displays the latest logging. Output will be given in the console. 


3.2.4 Display live logging
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -l

Displays live logging. Output will be given in the console. 


3.2.5 Display live logging with search string
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -ls

Displays live logging with the given search string. Output will be given in the console. 


3.2.6 Generate test message
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -t

Generates a test message. Run "rsview -s test" to check if it was successfull.


3.2.7 Clear all logging
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsview -c

Clears all logging. Output will be given in the console.

3.3 RSE user management (rseuser)
---------------------------------

.. code-block:: console
   
   Usage rseuser:

   Please use the command as: rseuser <username> <rm or add> <web-only>

3.3.1 Add user
^^^^^^^^^^^^^^

.. code-block:: console

   rseuser tom add web-only
  
Creates a user tom for the webinterface only. Drop the web-only option to setup a user for CLI.


3.3.2 Remove user
^^^^^^^^^^^^^^^^^

.. code-block:: console

   rseuser tom rm

Removes the user tom. 

3.4 RSC user management (rsuser)
--------------------------------

.. code-block:: console
   
   Usage rsuser:

   Please use the command as: rsuser <username> <rm or add> <web-only>

3.3.1 Add user
^^^^^^^^^^^^^^

.. code-block:: console

   rsuser tom add web-only
  
Creates a user tom for the webinterface only. Drop the web-only option to setup a user for CLI.


3.3.2 Remove user
^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsuser tom rm

Removes the user tom. 