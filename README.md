# acc
  
This package contains the standalone Airia Cloud Connector executable for connecting to the Airia Cloud Hub.

## 1. Config & Execute
- Update the `appsettings.json` file with your configuration settings.
  
#### Windows
- Run `Airia.CloudConnector.exe`
  
#### Linux/macOS
- Make the file executable: `chmod +x Airia.CloudConnector`
- Run: `./Airia.CloudConnector`
  
## 2. Persistent Process
#### 2.1 Quick and Simple
Good for a quick test — survives SSH disconnection but won't auto-restart on crash or reboot.
```bash
nohup ./Airia.CloudConnector > output.log 2>&1 &
```
To check it's running:
```bash
ps aux | grep Airia.CloudConnector
```
To Stop it:
```bash
kill <PID>   # use the PID from the ps aux output
```
  
#### 2.2 systemd Service (Recommended)
This is the best approach — it runs as a proper service, auto-restarts on crash, and survives reboots.
  
Step 1 — Create the service file:
```bash
sudo nano /etc/systemd/system/airia-cloudconnector.service
```
Step 2 — Paste this config:
```json
[Unit]
Description=Airia Cloud Connector
After=network.target
 
[Service]
WorkingDirectory=/path/to/your/app
ExecStart=/path/to/your/app/Airia.CloudConnector
Restart=always
RestartSec=5
User=your-linux-username
StandardOutput=journal
StandardError=journal
 
[Install]
WantedBy=multi-user.target
```
⚠️ Replace `/path/to/your/app` and `your-linux-username` with the correct values
  
Step 3 — Enable and start it:
```bash
sudo systemctl daemon-reload
sudo systemctl enable airia-cloudconnector   # auto-start on reboot
sudo systemctl start airia-cloudconnector    # start now
```
Step 4 — Check it's running:
```bash  
sudo systemctl status airia-cloudconnector
```
  
Useful commands:
```bash
sudo systemctl stop airia-cloudconnector      # stop
sudo systemctl restart airia-cloudconnector   # restart
journalctl -u airia-cloudconnector -f         # tail the logs live
```
## 3. Get the package Zip File
  
#### Install Git
```bash
## Ubuntu
sudo apt update
sudo apt install git
  
## RHEL
sudo yum install git
```
  
git clone https://github.com/anthonygrees/acc
  
## 4. Zip
```bash
## RHEL
sudo yum install unzip
  
## Ubuntu  
sudo apt install unzip
```
  
`unzip airia-connector-linux-x64.zip`
  
## 5. ICU Package Error
> Couldn't find a valid ICU package installed on the system. Please install libicu (or icu-libs) using your package manager and try again. Alternatively you can set the configuration flag System.Globalization.Invariant to true if you want to run with no globalization support. Please see https://aka.ms/dotnet-missing-libicu for more information.
  
  
```bash
## Ubuntu
sudo apt-get update
sudo apt-get install libicu-dev

## RHEL
sudo yum install libicu
  
## Fedora
sudo dnf install libicu
```