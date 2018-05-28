# Post Exploitation - Windows

Two types of privilege escalation:

* Vertical
* Horizontal

### Information Gathering

Find out OS Name and Version:

> `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`
>
> `ver`

Hostname:

> `hostname`

Username:

> `whoami`
>
> `echo %username`

Check user privilege \(check if belong to admin group\):

> `net user [user]`

Network:

> `ipconfig /all`

### Searching for Password in Configuration files

Clear-text passwords

> _c:\unattend.txt_
>
> _c:\sysprep.ini - \[Clear Text\]_
>
> _c:\sysprep\sysprep.xml - \[Base64\]_

The command below will search the file system for file names containing certain keywords

> `dir /s *pass* == *cred* == *vnc* == *.config*`

Search certain file types for a keyword, this can generate a lot of output.

> `findstr /si password *.xml *.ini *.txt`

Similarly the two commands below can be used to grep the registry for keywords, in this case "password".

> `reg query HKLM /f password /t REG_SZ /s`
>
> `reg query HKCU /f password /t REG_SZ /s`

### Discovery of Missing Patches

##### By CMD

> `wmic qfe get Caption,Description,HotFixID,InstalledOn`
>
> `wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr /C:"KB3136041" /C:"KB4018483"`

##### By Metasploit

> `use post/windows/gather/enum_patches`

##### By PowerShell \(Sherlock\)

> `PS C:\Users\User > Find-AllVulns`

##Tools

####PowerUp


##### Privilege Escalation Table \(Due to lack of sufficient patching\)

| OS | Description | Security Bulletin | KB | Exploit |
| :--- | :--- | :--- | :--- | :--- |
| Windows Server 2016 | Windows Kernel Mode Drivers | [MS16-135](https://technet.microsoft.com/en-us/library/security/ms16-135.aspx) | 3199135 | [Exploit](https://github.com/mwrlabs/CVE-2016-7255)[Github](https://github.com/FuzzySecurity/PSKernel-Primitives/blob/master/Sample-Exploits/MS16-135/MS16-135.ps1) |
| Windows Server 2008 ,7,8,10 Windows Server 2012 | Secondary Logon Handle | [MS16-032](https://technet.microsoft.com/en-us/library/security/ms16-032.aspx) | 3143141 | [GitHub](https://github.com/khr0x40sh/ms16-032)[ExploitDB](https://www.exploit-db.com/exploits/39719/)[Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms16_032_secondary_logon_handle_privesc) |
| Windows Server 2008, Vista, 7 | WebDAV | [MS16-016](https://technet.microsoft.com/en-us/library/security/ms16-016.aspx) | 3136041 | [Github](https://github.com/koczkatamas/CVE-2016-0051) |
| Windows Server 2003, Windows Server 2008, Windows 7, Windows 8, Windows 2012 | Windows Kernel Mode Drivers | [MS15-051](https://technet.microsoft.com/en-us/library/security/ms15-051.aspx) | 3057191 | [GitHub](https://github.com/hfiref0x/CVE-2015-1701/raw/master/Compiled/Taihou32.exe)[ExploitDB](https://github.com/offensive-security/exploit-database-bin-sploits/raw/master/sploits/37049-32.exe)[Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms15_051_client_copy_image) |
| Windows Server 2003, Windows Server 2008, Windows Server 2012, 7, 8 | Win32k.sys | [MS14-058](https://technet.microsoft.com/en-us/library/security/ms14-058.aspx) | 3000061 | [GitHub](https://github.com/sam-b/CVE-2014-4113)[ExploitDB](https://github.com/offensive-security/exploit-database-bin-sploits/raw/master/sploits/39666.zip)[Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms14_058_track_popup_menu) |
| Windows Server 2003, Windows Server 2008, 7, 8, Windows Server 2012 | AFD Driver | [MS14-040](https://technet.microsoft.com/en-us/library/security/ms14-040.aspx) | 2975684 | [Python](http://bhafsec.com/files/windows/MS14-40-x32.py)[EXE](http://bhafsec.com/files/windows/MS14-40-x32.exe)[ExploitDB](https://www.exploit-db.com/exploits/39446/)[Github](https://github.com/JeremyFetiveau/Exploits/blob/master/MS14-040.cpp) |
| Windows XP, Windows Server 2003 | Windows Kernel | [MS14-002](https://technet.microsoft.com/en-us/library/security/ms14-002.aspx) | 2914368 | [Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms_ndproxy) |
| Windows Server 2003, Windows Server 2008, 7, 8, Windows Server 2012 | Kernel Mode Driver | [MS13-005](https://technet.microsoft.com/en-us/library/security/ms13-005.aspx) | 2778930 | [Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms13_005_hwnd_broadcast)[ExploitDB](https://www.exploit-db.com/exploits/24485/)[GitHub](https://github.com/0vercl0k/stuffz/blob/master/ms13-005-funz-poc.cpp) |
| Windows Server 2008, 7 | Task Scheduler | [MS10-092](https://technet.microsoft.com/en-us/library/security/ms10-092.aspx) | 2305420 | [Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms10_092_schelevator)[ExploitDB](https://www.exploit-db.com/exploits/15589/) |
| Windows Server 2003, Windows Server 2008, 7, XP | KiTrap0D | [MS10-015](https://technet.microsoft.com/en-us/library/security/ms10-015.aspx) | 977165 | [Exploit](http://bhafsec.com/files/windows/KiTrap0d.zip)[ExploitDB](https://www.exploit-db.com/exploits/11199/)[GitHub](https://github.com/offensive-security/exploit-database-bin-sploits/raw/master/sploits/11199.zip)[Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms10_015_kitrap0d) |
| Windows Server 2003, XP | NDProxy | [MS14-002](https://technet.microsoft.com/en-us/library/security/ms14-002.aspx) | 2914368 | [Exploit](http://bhafsec.com/files/windows/MS14-002.exe)[ExploitDB](https://www.exploit-db.com/exploits/30014/)[ExploitDB](https://www.exploit-db.com/exploits/37732/)[Github](https://github.com/dev-zzo/exploits-nt-privesc/blob/master/MS14-002/MS14-002.c) |
| Windows Server 2003, Windows Server 2008, 7, 8, Windows Server 2012 | Kernel Driver | [MS15-061](https://technet.microsoft.com/en-us/library/security/ms15-061.aspx) | 3057839 | [Github](https://github.com/Rootkitsmm/MS15-061) |
| Windows Server 2003, XP | AFD.sys | [MS11-080](https://technet.microsoft.com/en-us/library/security/ms11-080.aspx) | 2592799 | [EXE](http://bhafsec.com/files/windows/ms110-080.exe)[Metasploit](https://www.rapid7.com/db/modules/exploit/windows/local/ms11_080_afdjoinleaf)[ExploitDB](https://www.exploit-db.com/exploits/18176/) |
| Windows Server 2003, XP | NDISTAPI | [MS11-062](https://technet.microsoft.com/en-us/library/security/ms11-062.aspx) | 2566454 | [ExploitDB](https://www.exploit-db.com/exploits/40627/) |
| Windows Server 2003, Windows Server 2008, 7, 8, Windows Server 2012 | RPC | [MS15-076](https://technet.microsoft.com/en-us/library/security/ms15-076.aspx) | 3067505 | [Github](https://github.com/monoxgas/Trebuchet) |
| Windows Server 2003, Windows Server 2008, 7, 8, Windows Server 2012 | Hot Potato | [MS16-075](https://technet.microsoft.com/en-us/library/security/ms16-075.aspx) | 3164038 | [GitHub](https://github.com/foxglovesec/RottenPotato)[PowerShell](https://github.com/Kevin-Robertson/Tater)[HotPotato](https://github.com/foxglovesec/Potato) |
| Windows Server 2003, Windows Server 2008, 7, XP | Kernel Driver | [MS15-010](https://technet.microsoft.com/en-us/library/security/ms15-010.aspx) | 3036220 | [GitHub](https://github.com/offensive-security/exploit-database-bin-sploits/raw/master/sploits/39035.zip)[ExploitDB](https://www.exploit-db.com/exploits/37098/) |
| Windows Server 2003, Windows Server 2008, 7, XP | AFD.sys | [MS11-046](https://technet.microsoft.com/en-us/library/security/ms11-046.aspx) | 2503665 | [EXE](http://bhafsec.com/files/windows/ms11-046.exe)[ExploitDB](https://www.exploit-db.com/exploits/40564/) |

### Privilege Escalation Exploit

| Exploit-DB | Vul Name | MS\# | 2000 | XP | 2003 | 2008 | Vista | 7 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 271 | Lsasrv.dll | MS04-011 | SP2/3/4 | SP0/1 | - | - | - | - |
| 350 | Util Manager | MS04-019 | SP2/3/4 | - | - | - | - | - |
| 351 | POSIX | MS04-020 | SP4 | - | - | - | - | - |
| 352 | Univ lang. Util Mgr | MS04-019 | SP2/3/4 | - | - | - | - | - |
| 355 | Univ lang. Util Mgr | MS04-019 | SP2/3/4 | - | - | - | - | - |
| 1149 | PnP Service | MS05-039 | SP4 | SP2 | SP1 | - | - | - |
| 1197 | keybd\_event | - | all | all | all | - | - | - |
| 1198 | CSRSS | MS05-018 | SP3/4 | SP1/2 | - | - | - | - |
| 1407 | Kernel APC | MS05-055 | SP4 | - | - | - | - | - |
| 1911 | Mrxsmb.sys | MS06-030 | all | SP2 | - | - | - | - |
| 2412 | Windows Kernel | MS06-049 | SP4 | - | - | - | - | - |
| 3220 | Print spool service | - | - | All | - | - | - | - |
| 5518 | win32k.sys | MS08-025 | SP4 | SP2 | SP1/SP2 | SP0 | SP0/SP1 | - |
| 6705 | Churrasco | MS09-012 | - | - | All | - | - | - |
| 6705 | Churraskito | - | - | All | All | - | - | - |
| 21923 | Winlogon NetDDE | - | All | All | - | - | - | - |
| 11199 | KiTrap0D/vdmallowed | MS10-015 | All | All | All | All | All | All |
| 14610 | Chimichurri | MS10-059 | - | - | - | All | All | SP0 |
| 15589 | Task Scheduler | MS10-092 | - | - | - | SP0/SP1/SP2 | SP1/SP2 | SP0 |
| 18176 | AFD.Sys | MS11-080 | - | SP3 | SP3 | - | - | - |
|  |  | MS13-005 |  |  |  |  |  |  |
|  |  | MS13-081 |  |  |  |  |  |  |
|  |  | MS14-058 |  |  |  |  |  |  |
|  |  | MS14-068 |  |  |  |  |  |  |
|  |  | MS14-070 |  |  |  |  |  |  |
|  |  | MS15-051 |  |  |  |  |  |  |
|  |  | MS15-052 |  |  |  |  |  |  |

### Useful Link
https://github.com/Hack-with-Github/Windows

http://www.exumbraops.com/penetration-testing-102-windows-privilege-escalation-cheatsheet/

