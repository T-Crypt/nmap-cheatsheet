# SMTP

```
sudo nmap 10.129.134.115 -p25 --script  smtp-enum-users
```

```shell-session
sudo nmap 10.129.14.128 -p25 --script smtp-open-relay -v
```

```shell-session
sudo nmap 10.129.14.128 -sC -sV -p25
```

```
smtp-user-enum -M VRFY -U users.txt -t 10.129.134.115
```

