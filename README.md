# Remote Syslog
Remote Syslog Master script

Updated RSEWEB response. Buffer is max: 3500 and refresh is max 3 seconds.

Updated RSECORE Service start time for Elasticsearch to 360 Seconds. Some slow systems need more time to start this service.

Added RSv2 installation option for RSECORE. (Web source is locked, scripts available)

Confirmed setups:
```
Tested for Ubuntu 20.04 LTS virtual machine.
Tested for Ubuntu 21.04 Raspberry Pi 4 (4GB RAM)
```

Quick installation:
```
git clone https://www.github.com/tslenter/RS
cd RS
chmod +x rseinstaller
sudo ./rseinstaller
Option 1 => RSE Core installation
Option 1 => Core installation

sudo ./rseinstaller
Optional webinsterface:
Option 2 => RSE webinterface installation
Option 2 => Install RSE WEB
```

Use SSH to run the CLI commands. Updated commands:
```
rseview
rseinstaller
rseuser
```

Webinterface is running @ port 443 (SSL)

Default login is using the PAM modules (default installation credentials). 

Usefull commands:

```
curl -XPUT --header 'Content-Type: application/json' http://localhost:9200/_cluster/settings --data '
{
  "transient": {
    "indices.lifecycle.poll_interval": "1m"
  }
}'
```
