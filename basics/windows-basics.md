# Windows Basics

Check user identity: `whoami`

Create folder: `md [folderName]`

Show hidden files: `dir /A`

Print out file content: `type file.txt`

Grep: `findstr file.txt`

## Windows CMD Basic

### \(1\) Displaying and Searching files

* Display

```text
   type [file]
```

* Multiple files

  ```text
   type *. txt 
   type [filel] [file2]
  ```

* Display one page at a time

```text
  more [file]
```

* Searching for a string within a file:

```text
  type [file] | find /i "[string]"
```

* Searching for regular expressions

```text
 type [file] | findstr [regex]
```

### \(2\) Environment Variables

* see all environment variable

```text
  set
```

* see a specific variable

```text
  set [variable_name]
```

* Some important one:

```text
  set username
  set path
```

### \(3\) Searching the File System

* List all directories

```text
  dir /b /s
```

* Search for a file in the file system

```text
  dir /b /s [directory][file]
```

e.g. `dir /b /s %systemroot%\hosts`

### \(4\) Managing Accounts and Groups and Deleting users

* List local users

```text
  net user
```

* List local groups

```text
  net localgroup
```

* List members of local admin group

```text
  net localgroup administrators
```

* Add user

```text
  net user [logon_ name] [password] /add
```

* Put the user in admin group

```text
  net localgroup administrators [logon_name] /add
```

* Remove a user from a group

```text
  net localgroup [group] [logon_name] /del
```

* Delete a account

```text
  net user [logon_name] /del
```

### \(5\) Local firewall administration

* See the configuration of the firewall

```text
  netsh advfirewall show allprofiles
```

* Allow a given port inbound

```text
  netsh advfirewall firewall add rule name="[Comment]" dir=in action=allow remoteip=[yourIPaddress] protocol=TCP localport=[port]
```

* Delete the firewall rule

```text
  netsh advfirewall firewall del rule name="[Comment]"
```

* Disable the firewall

  ```text
  netsh advfirewall set allprofiles state off
  ```

### \(6\) Interacting with Registry

* Read a reg key

  ```text
  reg query [KeyName]
  ```

* Change a reg key

  ```text
  reg add [KeyName] /v [ValueName] /t [type] /d [Data]
  ```

  KeyName: _**HKLM**_, HKCU, HKCR, _**HKU**_, and HKCC e.g. HKLM\Software\MySubkey

ValueName: Specifies the name for the registry key to be added or deleted e.g. AppInfo

List of valid type:

* REG\_SZ
* REG\_MULTI\_SZ
* REG\_DWORD\_BIG\_ENDIAN
* REG\_DWORD
* REG\_BINARY
* REG\_DWORD\_LITTLE\_ENDIAN
* REG\_LINK
* REG\_FULL\_RESOURCE\_DESCRIPTOR
* REG\_EXPAND\_SZ
* Export settings to a reg file

```text
  reg export [KeyName] [filename.reg]
```

* Import settings from a reg file

```text
  reg import [filename.reg]
```

* For remote machine \(Requires admin-level SMB session\)

  > reg add \ \[MachineName\] \[KeyName\] /v \[ValueName\] /t \[type\] /d \[Data\]

### \(7\) SMB Sessions

* Setting up a session with a target

```text
   net use \\[targetIP] [password] /u: [user]
```

* Mount a share on a target

  ```text
   net use * \\[targetIP] [share] [password] /u:[user]
  ```

* Drop a session

```text
   net use \\[targetIP] /del
```

* Drop all session

```text
   net use * /del
```

### \(8\) Controlling Services with sc

* List all running services

  ```text
  sc query
  ```

* List all installed services

  ```text
  sc query state=all
  ```

* Show a particular service's status

  ```text
  sc qc [service_name]
  ```

* List all running services on _**remote system**_

  ```text
  sc \\[targetIP] query
  ```

* Start a service

  ```text
  sc start [service_name]
  ```

* Stop a service

  ```text
  sc stop [service_name]
  ```

* If service start\_type is disabled

  ```text
  sc config [service_name] start=demand
  ```

### \(9\) Loop

* Counter

```text
  for /L %i in ([start],[step],[stop]) do [command]
```

Example Endless loop

```text
for /L %i in (1,0,2) do echo Hello
```

Normal loop

```text
for /L %i in (1,1,255) do echo %i
```

### \(10\) Run Multiple Commands

* Run Multiple Commands

```text
 [command 1] & [command 2]
```

* Run command1, and run command2 only if command1 succeeds without error

```text
 [command 1] && [command 2]
```

Example: Pause for 4 seconds between each iteration

![](https://github.com/wongkenny240/Penetration-Testing-Notes/tree/cfce35a77df70de3797e6921fb0119b361233957/assets/2018-04-23%202016_37_38-Start.png)

Note: Prepend command with@ to turn off echoing of command

## Windows Registry Basics

| Name | Abbr | Content |
| :--- | :--- | :--- |
| HKEY\_CLASSES\_ROOT | HKCR | Information used by programs for file association and for sharing information. |
| HKEY\_CURRENT\_USER | HKCU | Settings and configuration for the current user. |
| HKEY\_LOCAL\_MACHINE | HKLM | Settings and configuration for all users. |
| HKEY\_USERS | HKU | Settings and configuration for all users on the computer; the information in HKCU is copied from this hive when the user logs in. |
| HKEY\_CURRENT\_CONFIG | N/A | Hardware information about the PC’s resources and configuration. |

### Add a new startup application \(e.g. trojan\)

> \[HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run\]

## PowerShell Basics

Cmdlets are little programs that let you get stuff done Get a list of all cmdlets:

```text
  get-command
```

Find a list of cmdlets

```text
 get-command set*
 get-command *process
```

To list all aliases

```text
 alias
```

Expand an alias into a full name

```text
 alias gcm
```

Get aliases for a cmdlet

```text
 get-alias-definition [cmdlet]
```

Help for a cmdlet

```text
 help [alias]
```

More details/option for help:

```text
help [cmdlet or alias]
[cmdlet or alias] -detailed help 
[cmdlet or alias] -examples help 
[cmdlet or alias] -full help 
[cmdlet or alias] -online
```

TAB: for auto-complete

**PowerShell History**: When you go back and execute a previous command, your "command history pointer" moves up to the command you just re-executed

F7 key: shows you shell history ENTER for rerun, left or right to retype, ESC to get out of it, ALT + F7 to clear it

Display history:

```text
 get-history
```

Or

```text
 history
```

`-whatif` option: to see what command will do

Example:

```text
Remove-Item *.txt -whatif
```

Pipeline: pipe **objects** to other command

Example:

```text
ls | gm
```

`gm` shows the methods and properties output from a given cmdlet.

ForEach-Object \(%{$\_}\) The `%` take each object piped to it and then run a command of your choosing against each individual object. The command is inside `{}`. Current object is `$_`

Example:

```text
ps -name nc | % {stop-process $_}` `100, 200, 500 | % {$_ * 50}
```

Where-Object Check the properties of objects, use with -eq \(equal\), -ne \(not equal\), -like \(like with \* wildcard\), -gt, -lt

```text
get-service | ? {$_.status -eq "running"}
```

Select-Object Creates new objects from those passed down the pipeline, with a subset of properties

```text
get-service | select servicename,displayname
```

Searching for Files or Directories

```text
get-childitem -recurse [dir] [string] | %{echo $_.fullname}
```

![](https://github.com/wongkenny240/Penetration-Testing-Notes/tree/cfce35a77df70de3797e6921fb0119b361233957/assets/2018-05-04%202011_42_02-Start.png)

