# SNMP

```shell-session
snmpwalk -v2c -c public 10.129.14.128
```

{% code title="brute the community string then walk" %}
```shell-session
sudo apt install onesixtyone
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 10.129.14.128
```
{% endcode %}

```shell-session
sudo apt install braa
braa <community string>@<IP>:.1.3.6.*   # Syntax
braa public@10.129.14.128:.1.3.6.*
```
