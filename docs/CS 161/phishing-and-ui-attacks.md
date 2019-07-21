# Phishing and UI attacks

[Slides from SP18](http://www-inst.cs.berkeley.edu/~cs161/sp18/slides/4.12.phishingUIattacks.pdf)

## 3 factors of authentication
1. something you have (Yubikey, phone)
2. something you know (password)
3. something you are (fingerprint, iris scan, facial recognition)

### A 2FA caveat

- Password + answer to a security question is not two-factor authentication --
both of the factors are something you know
- The security question adds another layer of defense, however

## Session hijacking

### How sessions work
- You log into a website, the website generates a random string (your cookie) and stores it alongside your user id in its database
- Then, the websites sends you the cookie in its HTTP response
- In every subsequent HTTP request, your browser sends the cookie to the
  website, so the website logs you in without asking for your username/password

### Techniques
- Attacker steals session id somehow
- He writes JavaScript code so that when the victim visits the attacker's website, all the victim's cookies, from all his websites, are sent (via an POST request) to the attacker's server. Mitigated with Same-Origin Policy and `http-only` flag!
- He sniffs the cookie off the network. Mitigated using `secure` flag, which
  says cookies can only be sent over HTTPS.
- Also, giving the cookie a shorter expiration time means the attacker has less
  time to use the victim's session


## Clickjacking
### About `iframes`
- let you embed a website in another website
- for example -- you may use an iframe to embed Stripe's checkout elements
- malicious JS in the outer site cannot modify or read the inner site at all,
  due to the Same Origin Policy

### What is clickjacking?
- Example: you create a video player and add an invisible iframe for the  FB 'like'
  button in front of the play button
- Causes your users to like your site without realizing it

### Cursorjacking
- Idea: draw the user's real mouse cursor as well as a fake mouse cursor which
  is an offset away from the real cursor
- Create a button, so that when the user "clicks it" using the fake cursor, he
  really clicks something else (say a like button) using his real cursor
- Can hide real cursor using `cursor: none` CSS rule
- Demo: https://koto.github.io/blog-kotowicz-net-examples/cursorjacking/

## Clickjacking defenses
### Ineffective defenses
- Good site pops up a modal confirming user's action. Bad UX!
- Pop up a modal once in a while, not always, to confirm the user's action. Bad
  UX and the bad site can still clickjack, just less effectively.

### Framebusting 
- Good site includes JavaScript code that prevents other pages from framing it
