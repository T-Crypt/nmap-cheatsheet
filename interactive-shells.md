# Interactive Shells

{% code title="Interactive" %}
```shell-session
/bin/sh -i
```
{% endcode %}

{% code title="Perl" %}
```shell-session
perl —e 'exec "/bin/sh";'

perl: exec "/bin/sh";
```
{% endcode %}

{% code title="Ruby" %}
```shell-session
ruby: exec "/bin/sh"
```
{% endcode %}

{% code title="Lua" %}
```shell-session
lua: os.execute('/bin/sh')
```
{% endcode %}

{% code title="AWK" %}
```shell-session
awk 'BEGIN {system("/bin/sh")}'
```
{% endcode %}

{% code title="Using Find / Exec" %}
```shell-session
find / -name nameoffile -exec /bin/awk 'BEGIN {system("/bin/sh")}' \;

find . -exec /bin/sh \; -quit
```
{% endcode %}

{% code title="Vim" %}
```shell-session
vim -c ':!/bin/sh'

vim
:set shell=/bin/sh
:shell
```
{% endcode %}

