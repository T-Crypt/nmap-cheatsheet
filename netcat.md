# NetCat

{% code title="Connect with Source Port 53 -- Firewall Rule" %}
```shell-session
ncat -nv --source-port 53 10.129.2.28 50000
```
{% endcode %}
