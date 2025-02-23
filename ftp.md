# FTP

```shell-session
sudo nmap -sC -sV -p 21 192.168.2.142 
```

```
ftp> get Important\ Notes.txt
```

{% code title="Download All Available Files" %}
```
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136

tree .
```
{% endcode %}

```
put testupload.txt
```

{% code title="Find NMAP FTP Scripts" %}
```
find / -type f -name ftp* 2>/dev/null | grep scripts

nmap -sV -p21 -sC -A 10.129.14.136

sudo nmap -sV -p21 -sC -A 10.129.14.136 --script-trace
```
{% endcode %}

```shell-session
medusa -u fiona -P /usr/share/wordlists/rockyou.txt -h 10.129.203.7 -M ftp 
```

{% code title="Service Interaction" %}
```
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```
{% endcode %}
