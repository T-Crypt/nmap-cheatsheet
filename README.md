# Gobuster

```shell-session
cat ./vhosts | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://192.168.10.10 -H "HOST: ${vhost}.randomtarget.com" | grep "Content-Length: ";done
```

\


```
ffuf -w /usr/share/seclists/Discovery/DNS/namelist.txt -u http://10.129.202.236 -H "HOST: FUZZ.inlanefreight.htb" -fs 10918 -mc 200
```

```shell-session
export TARGET="facebook.com"
export NS="d.ns.facebook.com"
export WORDLIST="numbers.txt"
gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"

```

{% code title="Patterns" %}
```bash
lert-api-shv-{GOBUSTER}-sin6
atlas-pp-shv-{GOBUSTER}-sin6
```
{% endcode %}

```bash
gobuster dir -u http://94.237.59.185:46471/ -w /usr/share/dirb/wordlists/common.txt

```

