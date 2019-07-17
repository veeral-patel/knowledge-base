# The Tangled Web

[Book link](https://www.amazon.com/Tangled-Web-Securing-Modern-Applications/dp/1593273886)

## HTTP

### 3 versions of HTTP

- HTTP 0.9
- HTTP 1.0
- HTTP 1.1

### HTTP 0.9

- client could only do: `GET /page.html`
- server has to return the page
- no way for client to submit any options
- or for the server to provide more detailed error messages (page not available, page moved, etc)

### HTTP 1.1

#### What changes for the client?

- client can use different methods besides GET
- client can now send headers

#### Common headers

`User-Agent` - browser version information
`Host` - hostname of server
`Accept` - which content types (HTML, image, etc) client can accept
`Accept-Language` - which language client can accept
`Referer` - site user visited before this one - can leak info about browsing habits - usually sent, but with a few exceptions

- client can send a payload after headers
- but he must provide the length of the payload (Content-Length)

```
GET /page.html
Host: www.google.com
User-Agent: "Google Chrome 3.5"
Content-Type: text/html
Content-Length: 5

Hello
```

#### What changes for the server?

```
HTTP/1.1 200 OK
Server: Bunny-Server/0.9.2
Content-Type: text/plain
Connection: close

BUNNY WISH HAS BEEN GRANTED
```

- server can actually send back data!
- which protocol, status code, status explanation
- other headers

## HTTP request methods

- GET - information retrieval
- POST - submit information to server
  - payload
  - length of payload - content-length

## Keepalive sessions

- original idea was that client requests data, server sends data, and connection is closed
- but setting up a TCP connection every request made requests slow
- to keep a session alive, the server must also state the content length of its payload. that way, the client knows when it has received all the data and can request more.
- keepalive sessions default in HTTP 1.1 (disable with connection: close) and can be enabled in 1.0

## Chunked data transfers

- for the server to state the content length of the payload, it needs to
  know the length of the payload. however, in video streaming for example,
  it won't work to store the data, split it up, and then send portions with the
  content length
- instead, as we get portions of the data, we send it in chunks along with its content length
- use Transfer-Encoding: chunked

## Cache options

- server might want to cache responses it sends out

```
Expires: [when to evict response from cache]
Date: [when message was sent]
Pragma: cache option for proxies
Cache-Control: [who can cache it and how?]
```

## HTTP cookies

### Purpose

- Session management
- Personalization
- User tracking

- once used for local storage - now, use local storage APIs

### HTTP Cookie Semantics

- HTTP Cookies are sent by the server to the browser using the Set-Cookie
  header

```
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: hello=world
Set-Cookie: apple=banana
```

Then, on every new request to the server, the browser will send the cookies with every request

```
GET /page.html HTTP/1.1
Host: www.google.com
Cookie: hello=world; apple=banana;
```

#### Cookie options

- `Expires` -- when browser should evict cookie. if not set, then after browser closes.
- `Domain` -- browser should send cookies to a broader domain than sent the original cookie. however, can't send to another domain altogether
- `Path` -- browser sends cookies to a more specific path in the original domain
- `Secure` -- browser won't send cookie over non-HTTPS connections - migitates MITM
- `HttpOnly` -- client can't access cookie using javascript - migitates XSS

### `Expires`

- if server doesn't specify the cookie's expiration date (with `Expire`), then cookie lasts for as long as the browser is open--creating a **session cookie**
- if server specifies Expire, then cookie lasts until expiration--creating a **persistent cookie**
- web servers have no explicit way of asking web browser to delete a cookie
- every cookie is uniquely identified by the tuple (cookie name, domain, path), so a new cookie can overwrite an old cookie
- you could also set a short expire date
