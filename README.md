# nmap-cheatsheet

# Most Used Commands

`nmap -n -v -sT -A`
 
`nmap -sV -sC`

`nmap -p- --min-rate 1000 -sV`

`nmap -sV  -script vuln`

`nmap -Pn -p- -A -T4 1`

`nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn ping` 

`nmap -p22,50051 -sSC -Pn`

`nmap -p- -sC -sV --min-rate 5000 10.10.X.X -oN nmappc -Pn`

# Ports Environment Variable 
`ports=$(cat ports | awk -F " " '{print $4}' | awk -F "/" '{print $1}' | sort -n | tr '\n' ',' | sed 's/,$//')`

`nmap -Pn -A -p$ports 10.10.X.X`

# Packet Trace 

`nmap -vv -n -sn -PE -T4 --packet-trace 10.10.X.X`

# DoS

`nmap --script http-slowloris --max-parallelism 400 10.10.X.X`

`nmap --script http-slowloris-check 10.10.X.X`

# Brute Forcing 

`nmap --script http-brute -p 10.10.X.X`

`nmap --script http-form-brute -p 10.10.X.X`

`nmap -p 5432 --script pgsql-brute 10.10.X.X`

`nmap --script rtsp-url-brute -p 554`

`nmap -p 23 --script telnet-brute --script-args userdb=myusers.lst,passdb=mypwds.lst,telnet-brute.timeout=8s 10.10.X.X`

# Masscan 

`masscan -p1-65535 10.10.X.X --rate=1000 -e tun0 > ports`

# Identifying Open Ports with Nmap
<img src="https://github.com/T-Crypt/nmap-cheatsheet/blob/main/src/Scanning%20Tips.png" width="650"/>

# IdleScan / FTP Bounce Attack
<img src="https://github.com/T-Crypt/nmap-cheatsheet/blob/main/src/idlescan.png" width="650"/>
