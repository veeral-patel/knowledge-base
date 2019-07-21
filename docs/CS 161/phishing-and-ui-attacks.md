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

## Attacks on session management

### How sessions work
- You log into a website, the website generates a random string (your cookie) and stores it alongside your user id in its database
- Then, the websites sends you the cookie in its HTTP response
- In every subsequent HTTP request, your browser sends the cookie to the
  website, so the website logs you in without asking for your username/password

### Session hijacking attack
- Attacker steals session id somehow
- He writes JavaScript code so that when the victim visits the attacker's website, all the victim's cookies, from all his websites, are sent (via an POST request) to the attacker's server. Mitigated with Same-Origin Policy and `http-only` flag!
- He sniffs the cookie off the network. Mitigated using `secure` flag, which
  says cookies can only be sent over HTTPS.
- Also, giving the cookie a shorter expiration time means the attacker has less
  time to use the victim's session
