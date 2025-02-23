# NMAP

| `open`             | This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `closed`           | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not. |
| `filtered`         | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.                  |
| `unfiltered`       | This state of a port only occurs during the **TCP-ACK** scan and means that the port is accessible, but it cannot be determined whether it is open or closed.                                           |
| `open\|filtered`   | If we do not get a response for a specific port, `Nmap` will set it to that state. This indicates that a firewall or packet filter may protect the port.                                                |
| `closed\|filtered` | This state only occurs in the **IP ID idle** scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.                                           |

<figure><img src=".gitbook/assets/Operating-systems-TTL-Values.png" alt="TTL Values"><figcaption><p>TTL VALUES </p></figcaption></figure>

## &#x20;NMAP COMMANDS

```
sudo nmap 10.129.2.18 -sn -oA host -PE --reason
```

```
sudo nmap 10.129.2.18 -sn -oA host 
```

```
sudo nmap 10.129.2.28 -p- -sV -v 
```

<pre><code><strong>nmap 10.129.133.148 -p 445,80,22,110 -A -v
</strong></code></pre>

{% code title="Testing Firewall" %}
```
sudo nmap 10.129.2.28 -n -Pn -p445 -O
sudo nmap -A -Pn host
```
{% endcode %}

{% code title="SYN Scan" %}
```
sudo nmap 10.129.2.28 -p 21,22,25 -sS -Pn -n --disable-arp-ping --packet-trace
```
{% endcode %}

{% code title="ACK Scan" %}
```
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```
{% endcode %}

{% code title="Decoy IP's " %}
```
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```
{% endcode %}

{% code title="Firewall Testing" %}
```
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```
{% endcode %}

{% code title="Different Source IP" %}
```
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```
{% endcode %}

{% code title="SYN-Scan on a filtered port" %}
```
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace
```
{% endcode %}

{% code title="SYN-Scan From DNS Port" %}
```
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```
{% endcode %}

```
sudo nmap 10.129.2.28 -p 80 -A
```

```
sudo nmap 10.129.2.28 -p 80 -sV --script vuln
```

```
sudo nmap 10.129.2.0/24 -F
```

{% code title="Get Stats" %}
```
sudo nmap 10.129.2.28 -p- -sV --stats-every=5s
```
{% endcode %}

```
sudo nmap 10.129.2.28 -p 25 --script banner,smtp-commands
```

```
sudo nmap 10.129.2.28 -p 443 --packet-trace --disable-arp-ping -Pn -n --reason -sT 
```

```shell-session
sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn
```

```
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

```
sudo nmap 10.129.2.28 -p- -oA target (name the target)
```

<pre><code><strong>nmap 10.129.133.148 -p- -sV -Pn -n --disable-arp-ping --packet-trace
</strong></code></pre>

{% code title="HTML convert xml " %}
```
xsltproc target.xml -o target.html
```
{% endcode %}

### Scanning Options

| **Nmap Option**      | **Description**                                                                            |   |
| -------------------- | ------------------------------------------------------------------------------------------ | - |
| `10.10.10.0/24`      | Target network range.                                                                      |   |
| `-sn`                | Disables port scanning.                                                                    |   |
| `-Pn`                | Disables ICMP Echo Requests                                                                |   |
| `-n`                 | Disables DNS Resolution.                                                                   |   |
| `-PE`                | Performs the ping scan by using ICMP Echo Requests against the target.                     |   |
| `--packet-trace`     | Shows all packets sent and received.                                                       |   |
| `--reason`           | Displays the reason for a specific result.                                                 |   |
| `--disable-arp-ping` | Disables ARP Ping Requests.                                                                |   |
| `--top-ports=<num>`  | Scans the specified top ports that have been defined as most frequent.                     |   |
| `-p-`                | Scan all ports.                                                                            |   |
| `-p22-110`           | Scan all ports between 22 and 110.                                                         |   |
| `-p22,25`            | Scans only the specified ports 22 and 25.                                                  |   |
| `-F`                 | Scans top 100 ports.                                                                       |   |
| `-sS`                | Performs an TCP SYN-Scan.                                                                  |   |
| `-sA`                | Performs an TCP ACK-Scan.                                                                  |   |
| `-sU`                | Performs an UDP Scan.                                                                      |   |
| `-sV`                | Scans the discovered services for their versions.                                          |   |
| `-sC`                | Perform a Script Scan with scripts that are categorized as "default".                      |   |
| `--script <script>`  | Performs a Script Scan by using the specified scripts.                                     |   |
| `-O`                 | Performs an OS Detection Scan to determine the OS of the target.                           |   |
| `-A`                 | Performs OS Detection, Service Detection, and traceroute scans.                            |   |
| `-D RND:5`           | Sets the number of random Decoys that will be used to scan the target.                     |   |
| `-e`                 | Specifies the network interface that is used for the scan.                                 |   |
| `-S 10.10.10.200`    | Specifies the source IP address for the scan.                                              |   |
| `-g`                 | Specifies the source port for the scan.                                                    |   |
| `--dns-server <ns>`  | DNS resolution is performed by using a specified name server.                              |   |
| `-D RND:5`           | Generates five random IP addresses that indicates the source IP the connection comes from. |   |

### Output Options

| **Nmap Option** | **Description**                                                                   |
| --------------- | --------------------------------------------------------------------------------- |
| `-oA filename`  | Stores the results in all available formats starting with the name of "filename". |
| `-oN filename`  | Stores the results in normal format with the name "filename".                     |
| `-oG filename`  | Stores the results in "grepable" format with the name of "filename".              |
| `-oX filename`  | Stores the results in XML format with the name of "filename".                     |

### Performance Options

| **Nmap Option**              | **Description**                                              |
| ---------------------------- | ------------------------------------------------------------ |
| `--max-retries <num>`        | Sets the number of retries for scans of specific ports.      |
| `--stats-every=5s`           | Displays scan's status every 5 seconds.                      |
| `-v/-vv`                     | Displays verbose output during the scan.                     |
| `--initial-rtt-timeout 50ms` | Sets the specified time value as initial RTT timeout.        |
| `--max-rtt-timeout 100ms`    | Sets the specified time value as maximum RTT timeout.        |
| `--min-rate 300`             | Sets the number of packets that will be sent simultaneously. |
| `-T <0-5>`                   | Specifies the specific timing template.                      |
