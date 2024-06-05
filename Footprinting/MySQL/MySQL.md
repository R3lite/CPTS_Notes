It's an open-source SQL relational database management system developed and supported by Oracle.
Works according to client-server principle
The databases are often stored in a single file with extension `.sql`.
Ideally suited for apps such as dynamic websites, where efficient syntax and high response speed are essential. Often used in LAMP (Linux, Apache, MySQL, PHP) combination.

The web application informs the user if an error occurs during processing, which various SQL injections can provoke.o
MariaDB is a fork of the original MySQL.

### Default configuration
```shell
 cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'
```

### Dangerous settings
|**Settings**|**Description**|
|---|---|
|`user`|Sets which user the MySQL service will run as.|
|`password`|Sets the password for the MySQL user.|
|`admin_address`|The IP address on which to listen for TCP/IP connections on the administrative network interface.|
|`debug`|This variable indicates the current debugging settings|
|`sql_warnings`|This variable controls whether single-row INSERT statements produce an information string if warnings occur.|
|`secure_file_priv`|This variable is used to limit the effect of data import and export operations.|
## Footprinting the Service

Usually MySQL server runs on TCP port 3306.
```shell
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```
Connecting to MySQL
```shell
 mysql -u root -pP4SSw0rd -h 10.129.14.128
```
More about this database can be found in the [reference manual](https://dev.mysql.com/doc/refman/8.0/en/system-schema.html#:~:text=The%20mysql%20schema%20is%20the,used%20for%20other%20operational%20purposes) of MySQL.

|**Command**|**Description**|
|---|---|
|`mysql -u <user> -p<password> -h <IP address>`|Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password.|
|`show databases;`|Show all databases.|
|`use <database>;`|Select one of the existing databases.|
|`show tables;`|Show all available tables in the selected database.|
|`show columns from <table>;`|Show all columns in the selected database.|
|`select * from <table>;`|Show everything in the desired table.|
|`select * from <table> where <column> = "<string>";`|Search for needed `string` in the desired table.|
There is also a widely covered [security issues](https://dev.mysql.com/doc/refman/8.0/en/general-security-issues.html) section in the reference manual that covers best practices for securing MySQL servers. We should use this when setting up our MySQL server to understand better why something might not work.