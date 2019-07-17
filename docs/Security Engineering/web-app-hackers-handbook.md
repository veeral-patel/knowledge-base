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

## Attacking Access Controls

### Types of Access Controls

1. Vertical: Between users and admins
2. Horizontal: Between users and other users
3. Context-dependent: Ie, user cannot access stages in a multistate process out of order

### Types of Access Control Attacks:

1. Vertical privilege escalation: Ie, user becomes admin
2. Horizontal privilege escalation: Ie, user accesses another user's accounts
3. Business logic exploitation: User exploits a flaw in the application's logic (ie, bypasses payment step in shopping checkout)

### Completely Unprotected Functionality

- Anyone who knows a URL can access the functionality
- To find - check (Javascript) code for UI elements only visible to admins

## Direct Access to Methods

- URL parameters call API methods that shouldn't be accessible by users
- Often these API methods have no access control

### Identifier based Functions

- Say document hosted at www.hoster.com/q?docid=3424342
- Document only appears in owner's UI
- However, web app doesn't check that person requesting URL owns document, then attacker can access the document if he gets the URL
- How to get IDs?
  - if IDs randomly generated: check access logs, brute force

### Multistage Functions

- Web app validates on every stage, but...
- Web app forgets to re-validate on last step
- Attacker can intercept packet in last step, change something like source account number, and transfer \$\$\$ out of someone else's account

### Static Files

- Static files are usually put directly onto the server, with no application logic checking if the user has access to them

### Insecure ACL Methods

- Parameter based ACL - send whether user is admin in hidden form field, GET parameter, cookie, etc
- Referer based ACL
- Location-based ACL

## Attacking Application Logic

- Often, flaws in logic are due to making a false assumption, and not anticipating something that could happen

### Asking the Oracle

#### The Functionality

- "Remember me" - web app sets permanent cookie in the browser
- Cookie is unique and unpredictable
- Web app also stores user's username within "ScreenName cookie" - also encrypted

#### The Assumption

- Used same encryption algorithm for both ScreenName and RememberMe
- User can specify his own screen name -> he can encrypt anything he wants by checking the cookie

#### First example

- Attacker replaces ScreenName with RememberMe cookie.
- Contents of RememberMe cookie is decrypted and displayed on screen
- Why not a serious attack? Attacker just gains some basic info like username, IP address, etc. And attacker would need to steal RememberMe cookie, and if he could do that, he could just steal the session

#### Second example

- User can specify their screen names
- A user can choose screen name admin|1|192.168.4.243224
- Web app encrypts this screen name and stores it in the ScreenName cookie
- Now, replace RememberMe cookie with ScreenName cookie
- Logs in attacker as admin!

### Password change function

- Assumed that if user didn't enter the old password, he must be a admin
- Users could just not enter a old password and change any arbitrary user's password

### Proceeding to checkout

- Ecommerce website assumed people would shop in a certain order (find -> pay -> deliver)
- However, could skip from find to deliver w/o paying
- "Forced browsing"
- Try skipping stages, accessing a stage more than once, accessing earlier stages after later ones
- Might encounter errors -> useful for learning about the web app

## Attacking authentication

- Bad password policy
- Multiple users with same username
- Transmitting credentials in cleartext
- Insecure distribution of credentials
- Unsafe handling with HTTPS

### Brute forcible login

- Storing failed login count in cookie
- No account lockout

### Verbose failure messages

- Enumerating username using "new account"
- HTML difference in server response
- Time difference in server response

### Unsafe change password functionality

- Modify username field

### "Forgot password" functionality

- Easily guessed answers
- Brute forcible answers

### "Remember me" functionality

- Store username in persistent cookie
- Store session ID in persistent cookie
- Physical access to victim's computer

### User impersonation functionality

- Hidden function
- Trust user input like cookie
- Impersonate administrator
- Backdoor password

### Incomplete validation of credentials

- For example, stripping off unusual characters or removing first n characters before validating

### Predictable usernames

- Web app generates usernames for you, but they are predictable
- Can be used to enumerate possible usernames

### Predictable initial passwords

- Web app assigns you a password, which you change
- Worst case - everyone has same password
- Password can also be derived from username, job function, etc.
- Or contains a sequence that's guessable from a sample of passwords

## Attacking Backend Components

### OS Command Injection

#### How to detect?

- If not given any immediate output, use time delays
- Inject "run ping for 30 seconds" and see if the app takes 30 seconds
- Try sending output to another file or over SMTP

#### Injecting parameters

- server runs: wget <user input>
- set user input = "url -O file.txt"
- allows you to write any arbitrary files on the server

#### Injecting of scripting commands

- eg, server runs: system(<user input>)
- make server run: system('echo 2011') -> if 2011 printed, then you can inject scripting commands

#### Prevention

- Use server APIs; don't call OS commands directly
- Whitelist user input to a set of expcted values
- Limit character set to alphanumerics only

## File Traversal

- I know what this is
- Try changing format or canonicalization of path

#### Prevention:

- Reject any string that contains a path traversal sequence
- Reject any string not on the whitelist of acceptable file extensions
- Check that file being accessed is in the intended directory

## File Inclusion

### Remote File Inclusion

Example:

```
$country = $\_GET['country'];
include(\$country . '.php')
```

If `$country` = "US", then the code of `US.php` is pasted into the file, which is then run.

If you set `$country` to be a URL of a php file, then that arbitrary code will get executed.

### Local File Inclusion

- Problem: Can't read file X on the server.
- Solution: Include file X into another file, which is displayed. Then see X's contents!

## Server-side HTTP Redirection

- Server takes user input and requests something based on that user input
- Backend HTTP request can be to something on the internal network, or on the Internet

### Example

```
www.fetch.com/q?file="reddit.com/main.css"
```

- Here, file is a URL provided by the user. Then, the website, downloads the file at that URL.
- Attacker can put his own IP or something and make the web app connect to it - file="192.168.0.1:22"
- Use the web app as a HTTP proxy to perform more attacks
  - Attack 3rd-party servers without getting caught
  - Connect to hosts on the internal network

## HTTP Parameter Injection

- Tamper with the URL directly to change the web app's behavior

## Email Header Manipulation

> When a form is added to a Web page that submits data to a Web application, a malicious user may exploit the MIME format to append additional information to the message being sent, such as a new list of recipients or a completely different message body.

> Because the MIME format uses a carriage return to delimit the information in a message, and only the raw message determines its eventual destination, adding carriage returns to submitted form data can allow a simple guestbook to be used to send thousands of messages at once

## SMTP Injection

- Website uses POST parameters to fill out an email to send
- Inject extra data to send arbitrary emails
