# Get-Started
1. Download and install the Crestron Powershell EDK 
-Non-Crestron Link: https://crestron-edk.software.informer.com/download/
-Direct Crestron Link https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/Installation.htm


# SuperScript
Crestron Powershell script to pull device information and issue commands to many devices on an IP list.  Once script has ran, it will export the data gathered out to a CSV file for consumption.

This powershell script requires fairly little modification and can be used to gather information on hundreds of crestron devices on a network across multiple subnets.
1. Download the above module
2. Set your username and password
-$cUsername = "USERNAME"
-$cPassword = "PASSWORD"

3. Add IP's to your IP.txt list
4. Run Script
5. Script will attempt to connect to each device and grab various device information from it.

This script is very efficient in its performance and can very quickly filter through hundreds of devices in minutes.

# ScreenGrabber
Screengrabber connectes to the devices in IP.txt, issues the screenshot command, names the screenshot taken after the device's hostname, transfers the screenshot to your PC via FTP and then deletes screenshot file from the device memory

This script is really useful for checking the online status of MTR room touchpanels or Room Scheduler panels. 

# CrestFinder
CrestFinder.ps1 is a secondary script that utilizes the Read-Autodiscovery EDK function.  This script reaches out to device IP's from a text file and broadcasts out to other crestron devices on the same subnet.  This script helps to find other devices you may not know about based on a pre-existing IP list.

1.  Paste IP.txt list in root directory of script
2.  Change IP list name in script (to match name of your IP list)
3.  Run script

Script runs much quicker than superscript and returns IP address, Hostname, Device Model Info, Firmware version, compile date, and mac address.

# Firmware Upgrader
FirmwareUpgrader.ps1 is a secondary script that uses much of the same functionality as the superscript to initialize firmware upgrades across many devices on an IP list.

1. Download firmware file to be sent to devices to the same file location as script
2. Rename the variable "$FW" with the file name to be sent [FW = (Join-Path $PSScriptRoot 'tsw-xx60_2.009.0122.001.puf')]
3. Rename firmware file name [$fname = 'tsw-xx60_2.009.0122.00.puf']
4. Run script!

# DHCP Killer
DHCP Killer is a script to automate the process of turning off DHCP and setting the ethernet settings to static.

1.  Paste IP.txt list in root directory of script
2.  Change IP list name in script (to match name of your IP list)
3.  Edit DNS variables to desired IP's (defaults to googles DNS)
4.  Run script

- Script will filter import ip list and filter through device IP's
- script will pull device IP info (IP address, subnet mask, gateway) 
- script then sets device ethernet settings to static matching previously gathered info
- script disables DHCP
- Your device should have the same IP address it started with, but set to static


# UC-ENGINE Superscript 

.SYNOPSIS
  Asyncronously connects to UC-Engine and grabs windows Get-ComputerInfo details as well as connected devices, information about the touchpanel connected, and other various device info.

.INPUTS
  - $username = 'ENTER YOUR USERNAME' 
  - $password = 'ENTER PASSWORD'
  - $cusername = 'ENTER YOUR USERNAME'  #Crestron Device Username (Touchpanel)
  - $cpassword = 'ENTER PASSWORD' #Crestron Device Password (Touchpanel)
  - IP.txt text file containing IP addresses of devices (One per line)

. REQUIREMENTS
  - Run script as admin
  - Each UC-Engine MUST have PSRemoting enabled (To enable: Run Powershell as administrator ON UC ENGINE ==> Issue the command "Enable-PSRemoting -SkipNetworkProfileCheck")
  - PSCrestron module must be installed (Crestron EDK)
  - IP.txt file for IP's

.OUTPUTS
  C:\MTR  Results.csv
  
.EXAMPLE
  Modify BOTH SETS of username/password variables (Line 97) --> enter UC-ENGINE IP addresses into IP.txt file --> Run Script--> script will output device info to C:\MTR  Results.csv


# CrestScanner - Crestron Port Scanner

.SYNOPSIS
  Asyncronously scans devices in IP.txt file across multiple ports. 

.DESCRIPTION
  Script will connect to up to 30 devices simultaneously scan for various open ports


.INPUTS
  - IP.txt text file containing IP addresses of devices (One per line)

. REQUIREMENTS
  - PSCrestron module must be installed (Crestron EDK)
  - IP.txt file for IP's

.OUTPUTS
  C:\PortScan Results.csv
  
.EXAMPLE
  Enter IP's to scan into IP.txt file in root script directory --> Run script --> Script will scan each device for common ports as well as Crestron specific ports


# More information about the crestron powershell module
https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/Modules/CrestronSession-Module.htm
https://sdkcon78221.crestron.com/sdk/Crestron_EDK_SDK/Content/Topics/PSCrestron.htm#Get-VersionInfo
