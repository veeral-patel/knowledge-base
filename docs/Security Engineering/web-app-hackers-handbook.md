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

## Automating Web Attacks

### Uses for automation

- Enumerate identifiers
- Harvesting data
- Web app fuzzing

### Enumerating valid identifiers

- Ex. pages can be identified by page IDs, but not all page IDs correspond to
  valid pages.
- Detecting hits
  - HTTP status code
  - Response length
  - String in response body
  - Location header (for redirects)
  - Set Cookie header
  - Time delays

### Harvesting data

- Ex. Each page has sensitive information. You write a script to scrape each
  page for the data.

### Web app fuzzing

- Sending lots of attack strings to a website and seeing the results is
  tedious done manually

## Bypassing client-side controls

- Hidden form fields
- HTTP cookies
- URL parameters
- Referer header

### Obfuscated data

- Ex: ASP.NET View State
- Try to decipher algorithm
- Find a way to convert a string you choose into opaque string
- Replay opaque string in other requests
- Attack server side logic that deobfuscates the opaque string

### Bypassing client side validation in HTML forms

- Intercept and modify data after submitting
- Disable Javascript in browswer
- Intercept the server response and modify validation JS
  script to eliminate its effect
- Look for disabled elements
- Client side validation only problematic if no server side validation is done

### Capturing data with browser extensions

- Intercept and modify requests to/from browser extension
  - Serialized data: Deserialize, modify, re-serialize (Burp plugins)
  - May need to install SSL certificate in proxy
  - Non-HTTP protocol: Echo Mirage tool
- Reverse engineer the browser extension, learn what it's doing
  - Then modify code, recompile, and uploadto browser
- Modify the Javascript that interacts with extension (eg, show a hidden view)
- Attaching a debugger (JavaSnoop, Jswap)
