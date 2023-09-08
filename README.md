# nmap-cheatsheet

# ADding my most used nmap commands 

nmap -n -v -sT -A
 
nmap -sV -sC 

nmap -p- --min-rate 1000 -sV

nmap -sV  -script vuln

nmap -Pn -p- -A -T4 1

nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn ping 

nmap -p22,50051 -sSC -Pn 



nmap -p- -sC -sV --min-rate 5000 10.10.11.214 -oN nmappc -Pn


masscan -p1-65535 10.10.X.X --rate=1000 -e tun0 > ports

# Ports Environment Variable 
"ports=$(cat ports | awk -F " " '{print $4}' | awk -F "/" '{print $1}' | sort -n | tr '\n' ',' | sed 's/,$//')" 
nmap -Pn -A -p$ports 10.10.X.X

