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

3.4.1 Add user
^^^^^^^^^^^^^^

.. code-block:: console

   rsuser tom add web-only
  
Creates a user tom for the webinterface only. Drop the web-only option to setup a user for CLI.


3.4.2 Remove user
^^^^^^^^^^^^^^^^^

.. code-block:: console

   rsuser tom rm

Removes the user tom. 

3.5 Python module
-----------------

Remote Syslog rslogger can be used to write important lines of informational logging from a python script to a remote syslog server. We found it usefull as we run multiple scripts on different hosts. With this we track the given info on a central / remote server. Example use case: automation scripts for device configuration.

3.5.1 Requirements
^^^^^^^^^^^^^^^^^^

- Remote Syslog core or other syslog listener must be running as minimum
- Python script below has the same path as the running python script

3.5.2 Installation
^^^^^^^^^^^^^^^^^^

Install the python socket module using the following command:

.. code-block:: console
   
   pip install socket
   
Get a local copy of this repo:

.. code-block:: console

   git clone https://github.com/tslenter/rslogger
   cd rslogger
   #On Windows:
   copy rslogger <Directory of the project>
   #On Linux
   cp rslogger <Directory of the project>
   

3.5.3 Example with Cisco DNA Controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following is a demo example that extracts data from a Cisco DNA controller and sends the data string to a syslog socket: 

.. code-block:: console

   import requests
   import os
   from requests.auth import HTTPBasicAuth
   import urllib3
   import argparse
   from rslogger import syslog
   from rslogger import fcl
   from rslogger import lvl

   #Disable HTTPS validation
   urllib3.disable_warnings()

   #Set variables to None
   hostname = None
   username = None
   password = None

   #Create HTTP header
   headers = {
                 'content-type': "application/json",
                 'x-auth-token': ""
             }

   #Global information
   print('Running from directory: ', os.getcwd())

   #Add arguments
   parser = argparse.ArgumentParser()
   parser.add_argument('-n', '--hostname',  help='Enter a hostname or ip of the Cisco DNA Controller', required=True)
   parser.add_argument('-u','--username', help='Add a username', required=True)
   parser.add_argument('-p', '--password', help='Add a password', required=True)
   args = parser.parse_args()

   #Extract variables from namespace to global
   globals().update(vars(args))

   #Generate token for DNA Controller
   def dnac_login(host, passwrd, user):
       # Generate token
       BASE_URL = 'https://' + host
       AUTH_URL = '/dna/system/api/v1/auth/token'
       USERNAME = user
       PASSWORD = passwrd

       response = requests.post(BASE_URL + AUTH_URL, auth=HTTPBasicAuth(USERNAME, PASSWORD), verify=False)
       token = response.json()['Token']
       return token

   #Extract data from DNA controller
   def network_device_list(token, host):
       url = "https://" + host + "/api/v1/network-device"
       headers["x-auth-token"] = token
       response = requests.get(url, headers=headers, verify=False)
       data = response.json()
       for item in data['response']:
           #Feel free to list more information: item["hostname"],item["platformId"],item["softwareType"],item["softwareVersion"],item["upTime"], item["serialNumber"], item["managementIpAddress"]
           message = str("hostname: ")+item["hostname"]
           syslog(message, level=lvl['notice'], facility=fcl['log_audit'], host='172.16.201.2', port=514)

   #Login to DNA Controller
   if hostname or username or password != None:
       print("Started session on: " + hostname)
       print("Started session with user: " + username)
       login = dnac_login(hostname, password, username)
       network_device_list(login, hostname)
   else:
       print("Did you use the parameters to run this command?")

3.5.4 Available facility
^^^^^^^^^^^^^^^^^^^^^^^^

kern, user, mail, daemon, auth, syslog, lpr, news, uucp, cron, authpriv, ftp, ntp, log_audit, log_alert, clock_daemon, local0, local1, local2, local3, local4, local5, local6, local7


3.5.5 Available levels
^^^^^^^^^^^^^^^^^^^^^^

emerg, alert, crit, err, warning, notice, info, debug

3.5.6 Most basic code (Example)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console
   
   from rslogger import syslog
   from rslogger import fcl
   from rslogger import lvl
   
Run test message to localhost (a syslog server is needed)

.. code-block:: console

   syslog()
   
Expected output:

.. code-block:: console

   Jul  5 17:02:21 localhost daemon: notice: Test is RS test message to localhost

Run with variables:

.. code-block:: console

   message=str('Hello world')
   syslog(message, level=lvl['alert'], facility=fcl['daemon'], host='172.16.201.2', port=514)

Expected output (syslog server):

.. code-block:: console

   Jul  5 17:02:21 comp0001.remotesyslog.com rslogger: daemon: alert: rslogger_output: Hello world
