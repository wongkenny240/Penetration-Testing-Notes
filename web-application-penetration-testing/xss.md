# XSS

## XSS Basic

There are 3 types of XSS:

* Reflected XSS
* Stored XSS
* DOM-based XSS

## Reflected XSS

1. Detect input parameters and determine how they are input \(includes HTTP parameters, POST data, hidden form field values, and predefined radio or selection values\)
2. Use input data with each input parameters to see if any responses are triggered.
3. Examine the resulting web page HTML and searching for the test input.

## Bypass XSS filters

Input such as `<script>` and `<` or `>` may be filtered by the web application or browser.

### Without using a tag

#### Form

```text
<input type="text" name="state" value="INPUT_FROM_USER">
```

#### Form after injecting \(`" onfocus="alert(document.cookie)`\)

```text
<input type="text" name="state" value="" onfocus="alert(document.cookie)">
```

### Different syntax

Different syntax may bypass the filter but treated by the browser as valid syntax.

```text
"><script >alert(document.cookie)</script >
```

### Bypass non-recursive filtering

For some filter, it only perform once on the string and not recursively. It can be bypass with multiple tag

```text
<scr<script>ipt>alert(document.cookie)</script>
```

## Stored XSS

Stored XSS occurs when a web application gathers input from a user which might be malicious, and then stores that input in a data store for later use.

### Typical Flow of Stored XSS Attack

* Attacker stores malicious code into the vulnerable page
* User authenticates in the application
* User visits vulnerable page
* Malicious code is executed by the user's browser

### How to Discover?

## DOM-based XSS

The DOM, or Document Object Model, is the structural format used to represent documents in a browser.

For example, the page contains javascript that takes in user-input and change the content of the page.

It has nothing to deal with the server.

```text
<script>
function displayGreeting(name){
    if (name != ''){
        document.getElementById('greeting').innerHTML = "Hello " + name + "!"
    }
}
</script>
```

## How to exploit an XSS

Source:

[https://www.owasp.org/index.php/Cross-site\_Scripting\_\(XSS](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS)\)

[https://labs.detectify.com/2012/11/07/how-to-exploit-an-xss/](https://labs.detectify.com/2012/11/07/how-to-exploit-an-xss/)

