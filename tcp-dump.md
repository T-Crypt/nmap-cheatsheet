# TCP DUMP

```shell-session
sudo tcpdump -i tun0 host 10.10.14.2 and 10.129.2.28

nc -nv 10.129.2.28 25 (or specify the port)
```
