# DNS

```shell-session
 nslookup -type=NS zonetransfer.me
```

```shell-session
nslookup -type=any -query=AXFR zonetransfer.me nsztm1.digi.ninja
```

{% code title="DIG - AXFR Zone Transfer - Internal" %}
```shell-session
dig axfr internal.inlanefreight.htb @10.129.14.128
```
{% endcode %}

{% code title="DIG - AXFR Zone Transfer" %}
```shell-session
dig axfr inlanefreight.htb @10.129.14.128
```
{% endcode %}

```shell-session
dig any inlanefreight.htb @10.129.14.128
```

```shell-session
dig CH TXT version.bind 10.129.120.85
```

```shell-session
dig ns inlanefreight.htb @10.129.14.128
```

```shell-session
dig soa www.inlanefreight.com
```

SubDomain BruteForcing&#x20;

```shell-session
for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.inlanefreight.htb @10.129.14.128 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done
```

```shell-session
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```

```
dnsenum --dnsserver 10.129.134.115 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/fierce-hostlist.txt --threads 90 dev.inlanefreight.htb
```
