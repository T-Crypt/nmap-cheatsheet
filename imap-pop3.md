# IMAP \ POP3

```shell-session
sudo nmap 10.129.14.128 -sV -p110,143,993,995 -sC
```

```shell-session
curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd
```

```shell-session
curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v
```

```shell-session
openssl s_client -connect 10.129.14.128:pop3s
```

```shell-session
openssl s_client -connect 10.129.14.128:imaps
```

```
tag SELECT INBOX

tag FETCH 1:1 (BODY[HEADER])

tag FETCH 1 BODY[]


```
