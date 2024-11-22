## What is FTP

<li>FTP is an unsecure file transfer protocol</li>
<li>Data is sent in clear text</li>
<li>Uses port 21</li>

## What is FTPS?

<li>Uses FTP over SSL/TLS</li>
<li>Added support of TLS certificate for encruption</li>
<li>Uses port 22</li>
<li>Not firewall friendly</li>
<li>Difficult to configure</li>

## What is SFTP

<li>Uses FTP over SSH</li>
<li>Uses SSH for transferring files</li>
<li>Default encryption by SSH</li>

## Virtual Environments

In the windows search bar, search for Hyper-V Manager and open it.

Create two new virtual environments, one for OpenSSH and one for SFTP.

## OpenSSH

In your virtual environment, open up the Windows PowerShell Administrator and run the following command:
```pwsh
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*' 
```
Copy the name of the OpenSSH.Server into the command below:
```pwsh
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```
Next start the OpenSSH service and set the startup mode to automatic:
```pwsh
 Get-Service -Name "sshd" | Set-Service -Startup "Automatic" -PassThru | Start-Service -PassThru
```
Next right click on the windows icon, select "Run". Type this in the run box:
```run
%programdata%\ssh\sshd_config
```
Next change the port # from 22 to 2223:
```pwsh
(Get-Content "C:\ProgramData\ssh\sshd_config").replace("#Port 22", "Port 2223") | Set-Content "C:\ProgramData\ssh\sshd_config"
```
