11. WAF Web Application Firewall
================================

.. _WAF:

11.1 WAF Requirements
---------------------

.. code-block:: console

   Logstash installed
   RSE Core
   RSX Interface

11.2 File download locations
----------------------------

   Download vcredist_x64.exe: https://www.microsoft.com/en-us/download/details.aspx?id=40784
   Download ModSecurityIIS_2.9.3-64b.msi: https://github.com/SpiderLabs/ModSecurity/releases
   Download filebeat: https://www.elastic.co/downloads/beats/filebeat
   Download winlogbeat: https://www.elastic.co/downloads/beats/winlogbeat
   
11.3 IIS Module installation
----------------------------

Step 1

11.3.1 Visual C++ Redistributable Packages installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Start he installation of the Visual C++ Redistributable packages.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MVB/1.png?raw=true
   :width: 300
   :align: center
   :alt: image 1

Click next.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MVB/2.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Wait for the installation to finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MVB/3.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click close. The installation is done.

11.3.2 ModSecurity installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 2

Start he installation of the ModSecurity package.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/1.png?raw=true
   :width: 300
   :align: center
   :alt: image 1

Click next.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/2.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Accept and click next.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/3.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click next.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/4.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click next.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/5.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click Install.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/6.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Wait for the installation to finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/7.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click Finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/MODSEC/8.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Check within the IIS console if the modules are loaded.

Depending of the installation go to section 11.3.3 (WinLogBeat) or 11.3.4 (Filebeat).

11.3.3 Filebeat installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3

Start he installation of the ModSecurity package.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/1.png?raw=true
   :width: 300
   :align: center
   :alt: image 1

Accept and click Install.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/2.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Wait for the installation to finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/3.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click Finish.

11.3.3 WinLogBeat installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3

Start he installation of the ModSecurity package.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/WinLogBeat/1.png?raw=true
   :width: 300
   :align: center
   :alt: image 1

Accept and click Install.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/WinLogBeat/2.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Wait for the installation to finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/WinLogBeat/3.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click Finish.

11.3.4 Filebeat installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3

Start he installation of the ModSecurity package.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/1.png?raw=true
   :width: 300
   :align: center
   :alt: image 1

Accept and click Install.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/2.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Wait for the installation to finish.

.. image:: https://github.com/tslenter/RS/blob/main/doc/images/WAF/FileBeat/3.png?raw=true
   :width: 300
   :align: center
   :alt: image 1
   
Click Finish.