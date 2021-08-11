# Remote Syslog
Remote Syslog Master script

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
