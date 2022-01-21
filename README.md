[![Documentation Status](https://readthedocs.org/projects/remote-syslog/badge/?version=latest)](https://remote-syslog.readthedocs.io/en/latest/?badge=latest)
[![Website remotesyslog.com](https://img.shields.io/website-up-down-green-red/http/shields.io.svg)](https://www.remotesyslog.com/)
[![GitHub issues](https://img.shields.io/github/issues/Naereen/StrapDown.js.svg)](https://github.com/tslenter/RS/issues)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

# Remote Syslog
Remote Syslog Master script

Documention can be found here:

https://remote-syslog.readthedocs.io/

https://www.remotesyslog.com/

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

### 1.2 Funds
All donations and other funds will be used to cover cost of this project and to improve tests/plugins/core scripts. The roadmap will display new functions or products. Check https://www.remotesyslog.com for more information.

## 2. Tips for RSX/RSE
- Make a good lifecycle policy to prevent a full disk (Just monitor it for some time).
- Everything is built in a block structure so you can disable default services and add your own. This block structure allows you to disable the RSX/RSE concept and go an elastic stack setup, or something else.
- By default everything Syslog can be received at port 514 UDP/TCP, we do recommend 514/UDP and no 514/TCP (UDP is faster and we recommend that for all services).
- RSX/RSE is capable of running a cluster setup, we recommend a cluster of 3 for full redundancy. When running a cluster make sure you create a good update plan.
- By default we use Syslog-ng as core, this parses all syslog data. If you like to create fields for smart searches within the Kibana interface this is required.
- Check out the active directory (AD) setup. The RSX/RSE authentication page works with Linux PAM. PAM can beconfigured to use a AD.
- The default login name for RSX/RSE is the created with the Debian/Ubuntu installation. Do NOT use a root user! If you only created a root user, create a noraml user account for the login.
- We do have some patterns preconfigured. (CheckPoint, Cisco, Microsoft, F5, and more) You probably need to edit them to match the infrastructure.
- Because we use open source software everything is free and patterns can be found with a good google search as well.

Find more plugins: https://github.com/syslog-ng/syslog-ng/tree/master/scl

## 3. Help

To improve the code and functions we like to have you help. Send your idea or code to: info@remotesyslog.com or create a pull request. We will review it and add it to this project.
