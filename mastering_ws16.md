# Mastering WS 2016



## Chapter 2 - PowerShell

### Setting up profiles 
- `$Profile |Get-Member –Type Noteproperty`
- `Notepad $profile`
- `Test-Path $profile.AllUsersAllHosts`
- `if (!(test-path $profile)) {new-item -type file -path $profile -force}`

### Editing profiles

- `Notepad $Profile`
- `Notepad $profile.AllUsersAllHosts`
- `function awesome-prompt { $env:computername + "\" + (get-location) + "> " }`
- `Function Open-AsAdmin {Start-Process PowerShell -Verb RunAs}`

### Setting up execution policies

- `Set-ExecutionPolicy Restricted`
- `Set-ExecutionPolicy AllSigned`
- `Set-ExecutionPolicy RemoteSigned`
    - `Unblock-File`
- `Set-ExecutionPolicy Unestricted`
- `Set-ExecutionPolicy Bypass`
- `Set-ExecutionPolicy Undefined`

### Recording Powershell sessions

- `Start-Transcript c:\mystranscript.txt`
    - `Help Start-Transcript`
    - `-NoClobber`
    - `-OutputDirectory`
    - `-Append`
    - `Stop-Transcript`
    - `Help About_Start_Transcript`

### Using Aliases and Get-Help

- `Help DIR`
- `Get-Alias`
- `Get-help`
    - `-ShowWindow`
    - `Get-Help Get-Childitem -ShowWindow`
    - `Get-Help DIR -Example`
    - `Get-ChildItem -Recurse`
    - `DIR -Recurse`
- core commands are stored in `%systemdir%`
- `Get-Module -ListAvailable | Where HelpInfoURI`
- `Update-Help`
- `$env:PSModulePath`
- `$env:PSModulePath = $env:PSModulePath + ";f:\OurAddedPath"`

- `Import-Module "D:\LOBModulesWeBought\LOBModule"`
- `Update-Help -Force`

### Updating help without internet access

- `Save-Help -DestinationPath \\SMBFileServer01\ShareName\PSHelpFolder -Credential DomainName\UserName`

### Accessing online help files

- `Get-Help Get-Childitem -Online`

### Understanding the CMDLet Syntax

- `Get-Vm` == `get-vm` == `GeT-vM`
- `$computerList`

### Interpreting the Syntax

- `Help Get-Eventlog`
- `Get-Eventlog  -LogName Security`
- `Get-Eventlog -Security`

### Passing Multiple Values as Parameter

- `Get-EventLog Security –ComputerName Server01, Server02, Server03`

- `Get-EventLog Security –ComputerName (Get-Content c:\computerlist.txt)`

- ```
    $computers = Get-Content c:\Computerlist.txt
    Get-EventLog –LogName Security –ComputerName $computers
    ```

### Show-Command

- `Show-Command Get-Eventlog`
- `Get-EventLog -LogName security -ComputerName Server01, Server02, Server04^M`

### -WhatIf

- ```
    Remove-Item C:\nano\nano-srv02.vhd -WhatIf
    What if: Performing the operation "Remove File" on target "C:\nano\nano-srv02.vhd".
    ```

### -Confirm

- `-Confirm[:{$true | $false}]`

- ```
    Remove-Item C:\nano\nano-srv05.vhd -Confirm
    Are you sure you want to perform this action?
    Performing the operation "Remove File" on target "C:\nano\nano-srv05.vhd".
    [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is
    "Y"):
    ```

### Shortened syntax

- `Get-Service MpsSVC -ComputerName Boston-Srv01`

### Exploring PowerShell Command Concepts

- `Get-Command *adapter`

### Implementing Pipelines

- `Get-EventLog Security | Out-File c:\SecurityEvents.txt`

### Objects and Members

- `Get-Service | Get-Member`

### Object Sorting

- `Get-Service | Sort-Object -Property Name -Descending`
- `Get-Service | Sort-Object Name -Descending`
- `Get-Service | Sort-Object -Descending`
- `Get-Services | Sort-object -Property Status, Name`
    - `get-help sort-object -examples` 

