# Web Application Hacker's Handbook

## Mapping an application

- Automatic spidering
- Choosing a page vs choosing a function
- Discovering hidden parameters
- Check `robots.txt`

### Analysing the application

- User input
- URL file paths & request parameters
- HTTP headers (Burp Intruder)
- Out of band channels
- Identifying server side technologies
- Banner grabbing
- HTTP fingerprinting (HTTPRecon)
- Directory names
- Session tokens
- Third party code components
- Extrapolating application behavior
- Isolating unique application behavior

### User directed spidering

- Proxy/spider tools
- Browser extensions

### Discovering hidden content

- Brute force: Burp Intruder
- Search for temporary/hidden files
- Infer files from naming scheme
- Google hacking, Wayback machine
- Web server bug enumerates directory (N/Wikto)

## Attacking Users: XSS

There are three kinds of XSS:

1. Reflected XSS
2. Stored XSS
3. DOM-Based XSS

### Reflected XSS

- Aka first order XSS
- A website is vulnerable to reflected XSS if it immediately returns user input back to the browser, without properly validating it.

#### Example

Say

```
www.example.com/q?message="This is an error"
```

returns the HTML page:

```
<p>This is an error</p>
```

Then, the url `www.example.com/q?message="<script> alert(1) </script>"`.

returns the HTML page:

```
<p> <script> alert(1) </script> </p>
```

and opens a alert on the page.

### Stored XSS

- Aka second order XSS
- User submitted by a user is stored in the web app (not displayed immediately) then showed to other users.
- For example, an attacker can write a post containing embedded Javascript. anyone who visits the post runs his arbitrary Javascript
- Stored XSS is more serious than Reflected XSS
- Reflected XSS - need to get victim to visit URL, while in stored XSS you just need to wait for them to
- Stored XSS victims are already on the web app, and often
  authenticated, so cookie stealing is more likely to succeed

### DOM-Based XSS

- Instead of some dynamic program displaying the parameter in HTML, Javascript writes the parameter from the DOM after the page loads

### XSS Payloads

- Virtual defacement
- Injecting trojan functionality
- Inducing user actions
- Exploiting trust relationships
- Escalating the client-side attack
