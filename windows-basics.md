# Windows Basics

Check user identity: `whoami`

Create folder: `md [folderName]`

Show hidden files: `dir /A`

Print out file content: `type file.txt`

Grep: `findstr file.txt`

#### Windows CMD Basic

##### (1) Displaying and Searching files

* Display
> type [file]

* Multiple files
> type *. txt or type (filel] (file2]

* Display one page at a time
> more [file]


* Searching for a string within a file:
> type [file] | find /i "[string]"

* Searching for regular expressions
> type (file] I findstr [regex]

##### (2) Environment Variables

* see all environment variable
> set

* see a specific variable
> set [variable_name]

* Some important one:
> set username
>
> set path

##### (3) Searching the File System
* List all directories
> dir /b /s

* Search for a file in the file system
> dir /b /s [directory]\[file]

e.g. dir /b /s %systemroot%\hosts

##### (4) Managing Accounts and Groups and Deleting users
* List local users
> net user

* List local groups
> net localgroup

* List members of local admin group
> net localgroup administrators

* Add user
> net user [logon_ name] [password] /add

* Put the user in admin group
> net localgroup administrators [logon_name] /add

* Remove a user from a group
> net localgroup [group] [logon_name] /del

* Delete a account
> net user [logon_name] /del

##### (5) Local firewall administration
* See the configuration of the firewall
> netsh advfirewall show allprofiles

* Allow a given port inbound
> netsh advfirewall firewall add rule name=<span style="color:blue">"[Comment]"</span> dir=<span style="color:blue">in</span> action=<span style="color:blue">allow</span> remoteip=<span style="color:blue">[yourIPaddress]</span> protocol=TCP localport=<span style="color:blue">[port]</span>

* Delete the firewall rule
> netsh advfirewall firewall del rule name=<span style="color:blue">"[Comment]"</span>

* Disable the firewall
> netsh advfirewall set allprofiles state <span style="color:blue">off</span>

##### (6) Interacting with Registry
* Read a reg key
> reg query [KeyName]

* Change a reg key
> reg add <span style="color:blue">[KeyName]</span> /v <span style="color:blue">[ValueName]</span> /t <span style="color:blue">[type]</span> /d
<span style="color:blue">[Data]</span>

KeyName: ***HKLM***, HKCU, HKCR, ***HKU***, and HKCC
e.g. HKLM\Software\MySubkey

ValueName: Specifies the name for the registry key to be added or deleted
e.g. AppInfo

List of valid type:
* REG_SZ
* REG_MULTI_SZ
* REG_DWORD_BIG_ENDIAN
* REG_DWORD
* REG_BINARY
* REG_DWORD_LITTLE_ENDIAN
* REG_LINK
* REG_FULL_RESOURCE_DESCRIPTOR
* REG_EXPAND_SZ



* Export settings to a reg file
> reg export <span style="color:blue">[KeyName]</span> <span style="color:blue">[filename.reg]</span>

* Import settings from a reg file
> reg import [filename.reg]

* For remote machine (Requires admin-level SMB session)
> reg add <span style="color:red">\\\\ [MachineName]</span> <span style="color:blue">[KeyName]</span> /v <span style="color:blue">[ValueName]</span> /t <span style="color:blue">[type]</span> /d
<span style="color:blue">[Data]</span>

##### (7) SMB Sessions
* Setting up a session with a target
> net use \\\<span style="color:blue">[targetIP] [password]</span> /u: <span style="color:blue">[user]</span>

* Mount a share on a target
> net use * \\\<span style="color:blue">[targetIP) \[share][password]</span> /u : <span style="color:blue">[user]</span>

* Drop a session
> net use <span style="color:red">\\\</span><span style="color:blue">[targetIP]</span> /del

* Drop all session
> net use * /del

##### (8) Controlling Services with sc
* List all running services
> sc query

* List all installed services
> sc query state=all

* Show a particular service's status
> sc qc [service_name]

* List all running services on <span style="color:blue">***remote system***</span>
> sc \\\\[targetIP] query

* Start a service
> sc start [service_name]

* Stop a service
> sc stop [service_name]

* If service start_type is disabled
> sc config [service_name] start=demand

##### (9) Loop
* Counter
> for / L %i in ([start],[step] , [stop]) do [command]

Example
Endless loop
> for /L %i in (1 , 0 , 2) do echo Hello

Normal loop
> for /L %i in (1 , 1,255) do echo %i



##### (10) Run Multiple Commands
* Run Multiple Commands
> [command 1] & [command 2]

* Run command1, and run command2 only if command1
succeeds without error
> [command 1] && [command 2]

Example: Pause for 4 seconds between each iteration



![](/assets/2018-04-23 16_37_38-Start.png)

Note: Prepend command with@ to turn off echoing of command

#### Windows Registry Basics

| Name | Abbr |Content |
| :--- | :--- | :--- |
| HKEY\_CLASSES\_ROOT | HKCR | Information used by programs for file association and for sharing information. |
| HKEY\_CURRENT\_USER | HKCU | Settings and configuration for the current user. |
| HKEY\_LOCAL\_MACHINE | HKLM | Settings and configuration for all users. |
| HKEY\_USERS | HKU | Settings and configuration for all users on the computer; the information in HKCU is copied from this hive when the user logs in. |
| HKEY\_CURRENT\_CONFIG | N/A | Hardware information about the PC’s resources and configuration. |

#### Add a new startup application (e.g. trojan)
>[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run]


#### PowerShell Basics

Cmdlets are little programs that let you get stuff done
Get a list of all cmdlets:
> get-command


Find a list of cmdlets
> get-command set*

> get-command *process

To list all aliases
> alias

Expand an alias into a full name
> alias <span style="color:blue">gcm</span>


Get aliases for a cmdlet
> get-alias-definition [cmdlet]

Help for a cmdlet
> help [alias]

More details/option for help:
> help [cmdlet or alias] -detailed
> help [cmdlet or alias] -examples
> help [cmdlet or alias] -full
> help [cmdlet or alias] -online

TAB: for auto-complete

**PowerShell History**: When you go back and execute a
previous command, your "command
history pointer" moves up to the
command you just re-executed

F7 key: shows you shell history
ENTER for rerun, left or right to retype, ESC to get out of it, ALT + F7 to clear it

Display history:
> get-history

Or

> history

`-whatif` option: to see what command will do

Example:
> `Remove-Item *.txt -whatif`

Pipeline: pipe **objects** to other command

Example:
>`ls | gm`

`gm` shows the methods and properties output from a given cmdlet.

ForEach-Object (%{$\_})
The `%` take each object piped to it and then run a command of your choosing against each individual object. The command is inside `{}`. Current object is `$_`

Example:
> `ps -name nc | % {stop-process $_}`
> `100, 200, 500 | % {$_ * 50}`

Where-Object
Check the properties of objects, use with -eq (equal), -ne (not equal), -like (like with * wildcard), -gt, -lt

> `get-service | ? {$_.status -eq "running"}`

Select-Object
Creates new objects from those passed down the pipeline, with a subset of properties

> `get-service | select servicename,displayname`

Searching for Files or Directories

> `get-childitem -recurse [dir] [string] | %{echo $_.fullname}`

![](/assets/2018-05-04 11_42_02-Start.png)
