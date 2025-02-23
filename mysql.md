# MySQL

{% code title="Windows" %}
```cmd-session
mysql.exe -u username -pPassword123 -h 10.129.20.13
```
{% endcode %}

```shell-session
mysql -u username -pPassword123 -h 10.129.20.13
```

```shell-session
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```

```shell-session
mysql -u root -h 10.129.14.132
```

```shell-session
mysql -u root -pP4SSw0rd -h 10.129.14.128
```

<pre class="language-shell-session"><code class="lang-shell-session">mysql> use sys;
mysql> show tables;
<strong>
</strong><strong>-----------------------------------------------+
</strong>| Tables_in_sys                                 |
+-----------------------------------------------+
| host_summary                                  |
| host_summary_by_file_io                       |
| host_summary_by_file_io_type                  |
| host_summary_by_stages                        |
| host_summary_by_statement_latency             |
| host_summary_by_statement_type                |
| innodb_buffer_stats_by_schema                 |
| innodb_buffer_stats_by_table                  |
| innodb_lock_waits                             |
| io_by_thread_by_latency                       |
...SNIP...
| x$waits_global_by_latency                     |
+-----------------------------------------------+


mysql> select host, unique_users from host_summary;

+-------------+--------------+                   
| host        | unique_users |                   
+-------------+--------------+                   
| 10.129.14.1 |            1 |                   
| localhost   |            2 |                   
+-------------+--------------+  
</code></pre>

| **Command**                                          | **Description**                                                                                       |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `mysql -u <user> -p<password> -h <IP address>`       | Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password. |
| `show databases;`                                    | Show all databases.                                                                                   |
| `use <database>;`                                    | Select one of the existing databases.                                                                 |
| `show tables;`                                       | Show all available tables in the selected database.                                                   |
| `show columns from <table>;`                         | Show all columns in the selected database.                                                            |
| `select * from <table>;`                             | Show everything in the desired table.                                                                 |
| `select * from <table> where <column> = "<string>";` |                                                                                                       |
