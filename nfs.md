# NFS

```shell-session
sudo nmap 10.129.14.128 -p111,2049 -sV -sC
```

```
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

{% code title="Show Available NFS" %}
```
showmount -e 10.129.14.128
```
{% endcode %}

{% code title="Mounting NFS Share" %}
```
mkdir target-NFS
sudo mount -t nfs 10.129.14.128:/ /target-NFS/ -o nolock
cd target-NFS
tree .


sudo mkdir /mnt/Finance
sudo mount -t cifs -o username=plaintext,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance
```
{% endcode %}

```
sudo umount ./target-NFS
```
