# FootPrinting

{% embed url="https://crt.sh/" %}

<pre class="language-bash"><code class="lang-bash">export TARGET="facebook.com"
<strong>curl -s "https://crt.sh/?q=${TARGET}&#x26;output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"
</strong></code></pre>

<pre class="language-bash" data-title="SOURCE multi recon "><code class="lang-bash"><strong>nano sources.txt
</strong><strong>
</strong><strong>baidu
</strong>bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye

export TARGET="facebook.com"
cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done

cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"

cat facebook.com_*.txt | sort -u > facebook.com_subdomains_passive.txt

cat facebook.com_subdomains_passive.txt | wc -l
</code></pre>

```bash
export TARGET="facebook.com"
export PORT="443"
openssl s_client -ign_eof 2>/dev/null <<<$'HEAD / HTTP/1.0\r\n\r' -connect "${TARGET}:${PORT}" | openssl x509 -noout -text -in - | grep 'DNS' | sed -e 's|DNS:|\n|g' -e 's|^\*.*||g' | tr -d ',' | sort -u

```

{% code title="Certificate output in Json" %}
```
curl -s https://crt.sh/?q=xceptional.com\&output\=json | jq .
```
{% endcode %}

{% code title="SubDomains" %}
```
curl -s https://crt.sh/\?q\=xceptional.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u > subdomainlist
```
{% endcode %}

{% code title="Company Hosted Servers" %}
```
for i in $(cat subdomainlist);do host $i | grep "has address" | grep xceptional.com | cut -d" " -f1,4;done
```
{% endcode %}

{% code title="Shodan - IP List" %}
```bash
for i in $(cat subdomainlist);do host $i | grep "has address" | grep xceptional | cut -d" " -f4 >> ip-addresses.txt;done

for i in $(cat ip-addresses.txt);do shodan host $i;done
```
{% endcode %}

{% code title="DNS Records" %}
```
dig any xceptional.com
```
{% endcode %}

TOOLS&#x20;

| [Baidu](http://www.baidu.com/)                           | Baidu search engine.                                                                                                            |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `Bufferoverun`                                           | Uses data from Rapid7's Project Sonar - [www.rapid7.com/research/project-sonar/](http://www.rapid7.com/research/project-sonar/) |
| [Crtsh](https://crt.sh/)                                 | Comodo Certificate search.                                                                                                      |
| [Hackertarget](https://hackertarget.com/)                | Online vulnerability scanners and network intelligence to help organizations.                                                   |
| `Otx`                                                    | AlienVault Open Threat Exchange - [https://otx.alienvault.com](https://otx.alienvault.com/)                                     |
| [Rapiddns](https://rapiddns.io/)                         | DNS query tool, which makes querying subdomains or sites using the same IP easy.                                                |
| [Sublist3r](https://github.com/aboul3la/Sublist3r)       | Fast subdomains enumeration tool for penetration testers                                                                        |
| [Threatcrowd](http://www.threatcrowd.org/)               | Open source threat intelligence.                                                                                                |
| [Threatminer](https://www.threatminer.org/)              | Data mining for threat intelligence.                                                                                            |
| `Trello`                                                 | Search Trello boards (Uses Google search)                                                                                       |
| [Urlscan](https://urlscan.io/)                           | A sandbox for the web that is a URL and website scanner.                                                                        |
| `Vhost`                                                  | Bing virtual hosts search.                                                                                                      |
| [Virustotal](https://www.virustotal.com/gui/home/search) | Domain search.                                                                                                                  |
| [Zoomeye](https://www.zoomeye.org/)                      | A Chinese version of Shodan.                                                                                                    |

### Layer No.1: Internet Presence

The first layer we have to pass is the "Internet Presence" layer, where we focus on finding the targets we can investigate. If the scope in the contract allows us to look for additional hosts, this layer is even more critical than for fixed targets only. In this layer, we use different techniques to find domains, subdomains, netblocks, and many other components and information that present the presence of the company and its infrastructure on the Internet.

`The goal of this layer is to identify all possible target systems and interfaces that can be tested.`

***

### Layer No.2: Gateway

Here we try to understand the interface of the reachable target, how it is protected, and where it is located in the network. Due to the diversity, different functionalities, and some particular procedures, we will go into more detail about this layer in other modules.

`The goal is to understand what we are dealing with and what we have to watch out for.`

***

### Layer No.3: Accessible Services

In the case of accessible services, we examine each destination for all the services it offers. Each of these services has a specific purpose that has been installed for a particular reason by the administrator. Each service has certain functions, which therefore also lead to specific results. To work effectively with them, we need to know how they work. Otherwise, we need to learn to understand them.

`This layer aims to understand the reason and functionality of the target system and gain the necessary knowledge to communicate with it and exploit it for our purposes effectively.`

This is the part of enumeration we will mainly deal with in this module.

***

### Layer No.4: Processes

Every time a command or function is executed, data is processed, whether entered by the user or generated by the system. This starts a process that has to perform specific tasks, and such tasks have at least one source and one target.

`The goal here is to understand these factors and identify the dependencies between them.`

***

### Layer No.5: Privileges

Each service runs through a specific user in a particular group with permissions and privileges defined by the administrator or the system. These privileges often provide us with functions that administrators overlook. This often happens in Active Directory infrastructures and many other case-specific administration environments and servers where users are responsible for multiple administration areas.

`It is crucial to identify these and understand what is and is not possible with these privileges.`

***

### Layer No.6: OS Setup

Here we collect information about the actual operating system and its setup using internal access. This gives us a good overview of the internal security of the systems and reflects the skills and capabilities of the company's administrative teams.

`The goal here is to see how the administrators manage the systems and what sensitive internal information we can glean from them.`

<figure><img src=".gitbook/assets/enum-method3.png" alt=""><figcaption></figcaption></figure>
