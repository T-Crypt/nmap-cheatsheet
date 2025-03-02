# Windows Commands

{% code title="File Count in C:\" %}
```cmd-session
dir n: /a-d /s /b | find /c ":\"
```
{% endcode %}

{% code title="Search for file with a  word" %}
```cmd-session
dir n:\*cred* /s /b

dir n:\*secret* /s /b

```
{% endcode %}

{% code title=" specific word within a text file" %}
```cmd-session
findstr /s /i cred n:\*.*
```
{% endcode %}

### Powershell

{% code title="Powershell Credential Function" %}
```powershell-session
PS C:\htb> $username = 'plaintext'
PS C:\htb> $password = 'Password123'
PS C:\htb> $secpassword = ConvertTo-SecureString $password -AsPlainText -Force
PS C:\htb> $cred = New-Object System.Management.Automation.PSCredential $username, $secpassword
PS C:\htb> New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred
```
{% endcode %}

```powershell-session
Get-ChildItem \\192.168.220.129\Finance\
```

{% code title="File Count" %}
```powershell-session
PS C:\htb> N:
PS N:\> (Get-ChildItem -File -Recurse | Measure-Object).Count
```
{% endcode %}

{% code title="File with string find " %}
```powershell-session
Get-ChildItem -Recurse -Path N:\ | Select-String "cred" -List
```
{% endcode %}
