# Window Server 2016 Inside Out



## Chapter 1

### PowerShell

#### Basic Commands
```
update-help

get-command

get-command -module <module name>

get-command -noun <noun name>

help <cmdlet name>

help -detailed <cmdlet name>

help -examples <cmdlet name>
```

#### PowerShell Gallery
```
find-module -repository psgallery | out-host -paging

find-module -repository psgallery -name <module name>

install-module -repository psgallery -name <module name>

update-module

get-installedmodule
```

#### Remoting
```
enable-psremoting

$cred = get-credential
enter-pssession -computername <computer name> -credential $cred
```

##### Remoting to a non-domain joined computer
```
set-item wsman:\localhost\Client\TrustedHosts -Value 192.168.3.200 -concatenate

help about_remote_faq -showwindow
```

##### One to many remoting
```
$computers = get-content c:\computers.txt

invoke-command -scriptblock { get-service wuauserv } -computername $computers

$computers = get-content c:\Computers.txt
invoke-command -filepath c:\FixStuff.ps1
```

##### Remote Tabs
PSh ISE > File > New Remote PSh Tab >
```
Computer: <computer name, ex: DC1>
Username: <user name, ex: domain\admin.account>
```
..> Connect 



#### Snippets

PSh ISE > if-else, do-while 

```
new-snippet
```

#### PowerShell Direct

- works only on WS16 and W10

```
get-vm

enter-pssession -vmname <vm name>
```

#### Remote Desktop

System Properties > Remote tab > enable 

```
set-itemproperty -path "HKLM:\System\CurrentControlSet\Control\Terminal Server" -Name "fDenyTSConnections" -Value 0

Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```
