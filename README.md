[![Documentation Status](https://readthedocs.org/projects/remote-syslog/badge/?version=latest)](https://remote-syslog.readthedocs.io/en/latest/?badge=latest)
# Remote Syslog
Remote Syslog Master script

Currently we are migrating from the RSX-RSC repository. Documention could be off. Documention can befound here:
```
https://www.remotesyslog.com/
https://www.github.com/tslenter/RSX-RSC/
```

Updated RSEWEB export, loader, live view controls are added.

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

## 1. Donation and help

### 1.1 Donation

Crypto:

```
XRP/Ripple: rHdkpJr3qYqBYY3y3S9ZMr4cFGpgP1eM6B
BTC/Bitcoin: 1JVmexqGBQyGv9fVkSynHapi2U6ZCyjTUJ
LTC/Litecoin Segwit: MAH8ATCK6X7biiTQrW7jUZ6L9eg1YBo5qS
ETH/Ethereum: 0xd617391076F9bEa628f657606DEAB7a189199AF5
```
PayPal:

[![paypal](https://www.paypalobjects.com/en_US/NL/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=KQKRPDQYHYR7W&currency_code=EUR&source=url)
