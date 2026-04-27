# acc

## Config & Execute
- Update the `appsettings.json` file with your configuration settings.
  
### Windows
- Run `Airia.CloudConnector.exe`
  
### Linux/macOS
- Make the file executable: `chmod +x Airia.CloudConnector`
- Run: `./Airia.CloudConnector`
  
## Get the package Zip File
  
### Install Git
Ubuntu
```sudo apt update
sudo apt install git```
  
RHEL
```sudo yum install git```
  
git clone https://github.com/anthonygrees/acc
  
## Zip
```
## RHEL
sudo yum install unzip
  
## Ubuntu  
sudo apt install unzip```
  
```unzip airia-connector-linux-x64.zip```
  
## ICU Package Error
```Couldn't find a valid ICU package installed on the system. Please install libicu (or icu-libs) using your package manager and try again. Alternatively you can set the configuration flag System.Globalization.Invariant to true if you want to run with no globalization support. Please see https://aka.ms/dotnet-missing-libicu for more information.```
  
```
## Ubuntu
sudo apt-get update
sudo apt-get install libicu-dev[9:37 AM]RHEL
sudo yum install libicu
  
## RHEL
sudo dnf install libicu
```