---
title: HTTP in Detail
source: https://tryhackme.com/room/httpindetail
platform: TryHackMe
module: Networking
difficulty: Easy
duration: 30 min
tags: [cybersecurity, tryhackme, http, https, url, http-methods, status-codes, headers, cookies, beginner]
status: in-progress
---

# 🌐 HTTP in Detail

> [!info] Room Info
> **Difficulty:** Easy · **Time:** ~30 min · **Module:** Networking (follows [[DNS in Detail]])
> Goal: Understand HTTP(S), URL structure, requests/responses, HTTP methods, status codes, headers, and cookies.

---

## 1. What Is HTTP(S)?

### HTTP (HyperText Transfer Protocol)
Used every time you view a website — developed by **Tim Berners-Lee** and team (1989–1991). HTTP is the rule set for communicating with web servers to transmit webpage data (HTML, images, video, etc.).

### HTTPS (HyperText Transfer Protocol Secure)
The **secure** version of HTTP. HTTPS data is **encrypted**, which:
- Stops others from seeing what you send/receive
- Assures you're actually talking to the real server, not an impersonator

> [!tip] Ties Back
> This builds directly on the client-server concepts from [[Client-Server Basics]] and the encryption/Presentation-layer concepts from [[OSI Model]].

> [!question]- 🧪 Quick Quiz: What Is HTTP(S)?
> 1. What does HTTP stand for?
> 2. What does the "S" in HTTPS add, specifically?
> 3. Who developed HTTP, and roughly when?
>
> **Answers**
> 1. HyperText Transfer Protocol.
> 2. Encryption — protecting data from being read in transit, and verifying you're communicating with the legitimate server.
> 3. Tim Berners-Lee and his team, between 1989–1991.

---

## 2. Requests and Responses

### URL Structure (Uniform Resource Locator)

A URL is an instruction on how to access a resource on the Internet.

**Example:** `http://user:password@tryhackme.com:80/view-room?id=1#task3`

| Part | Value in Example | Meaning |
|---|---|---|
| **Scheme** | `http` | Protocol to use — HTTP, HTTPS, FTP, etc. |
| **User** | `user:password` | Optional login credentials embedded in the URL |
| **Host** | `tryhackme.com` | Domain name or IP address of the server |
| **Port** | `80` | Which port to connect to — default 80 (HTTP) / 443 (HTTPS), but can be 1–65535 |
| **Path** | `/view-room` | File name/location of the resource |
| **Query String** | `?id=1` | Extra parameters passed to the path (e.g. "give me blog article with id=1") |
| **Fragment** | `#task3` | A specific location *within* the requested page |

```mermaid
flowchart LR
    A["http://"] --> B["user:password@"]
    B --> C["tryhackme.com"]
    C --> D[":80"]
    D --> E["/view-room"]
    E --> F["?id=1"]
    F --> G["#task3"]
```

### Making a Request

The bare minimum: `GET / HTTP/1.1` — but real browsing sends extra data via **headers**.

**Example Request:**
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/

```

| Line | Meaning |
|---|---|
| `GET / HTTP/1.1` | Method = GET, resource = homepage (`/`), protocol version = HTTP/1.1 |
| `Host: tryhackme.com` | Which website is being requested |
| `User-Agent: ...` | Which browser/version is making the request |
| `Referer: ...` | The page that linked/referred the client here |
| *(blank line)* | Signals the request has finished |

**Example Response:**
```http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head><title>TryHackMe</title></head>
<body>Welcome To TryHackMe.com</body>
</html>
```

| Line | Meaning |
|---|---|
| `HTTP/1.1 200 OK` | Protocol version + status code (200 = success) |
| `Server: nginx/1.15.8` | Web server software + version |
| `Date: ...` | Server's current date/time/timezone |
| `Content-Type: text/html` | Tells the client what kind of data follows (HTML, image, video, PDF, XML, etc.) |
| `Content-Length: 98` | How much data to expect — lets the client confirm nothing's missing |
| *(blank line)* | Marks the end of the response headers |
| *(body)* | The actual requested content |

> [!question]- 🧪 Quick Quiz: Requests and Responses
> 1. Name all 7 possible parts of a URL and give one example value for each.
> 2. What's the difference between a Path and a Query String?
> 3. What does a blank line signify in both an HTTP request and response?
> 4. What does the Content-Length header allow the client to verify?
> 5. What information does the User-Agent header convey, and why might a server care?
>
> **Answers**
> 1. Scheme (`http`), User (`user:password`), Host (`tryhackme.com`), Port (`80`), Path (`/view-room`), Query String (`?id=1`), Fragment (`#task3`).
> 2. Path identifies *which resource* is being requested; Query String passes *extra parameters* to that resource (e.g. which specific record to return).
> 3. The end of the headers section — request/response is complete.
> 4. That the full response was received — no data is missing.
> 5. It identifies the browser/software making the request; servers use it to format content appropriately, since some HTML/JS/CSS features are browser-specific.

---

## 3. HTTP Methods

Methods communicate the client's **intended action**.

| Method | Purpose |
|---|---|
| **GET** | Retrieve information from the server |
| **POST** | Submit data to the server — often creates a new record |
| **PUT** | Submit data to **update** existing information |
| **DELETE** | Remove information/records from the server |

> [!example] Matching Actions to Methods
> - Create a new user account → **POST**
> - Update your email address → **PUT**
> - Remove a picture you uploaded → **DELETE**
> - View a news article → **GET**

> [!question]- 🧪 Quick Quiz: HTTP Methods
> 1. Which method would you use to submit a new blog post?
> 2. Which method retrieves data without modifying anything?
> 3. What's the functional difference between POST and PUT?
> 4. Which method would remove an item from your shopping cart?
>
> **Answers**
> 1. POST.
> 2. GET.
> 3. POST typically creates a new record; PUT updates an existing one.
> 4. DELETE.

---

## 4. HTTP Status Codes

Every response's first line includes a **status code** — the outcome of the request.

### The 5 Ranges

| Range | Category | Meaning |
|---|---|---|
| **100–199** | Informational | First part of request accepted, continue sending — rare in practice |
| **200–299** | Success | Request completed successfully |
| **300–399** | Redirection | Client is redirected to a different resource |
| **400–499** | Client Errors | Something wrong with the *client's* request |
| **500–599** | Server Errors | Something wrong on the *server's* side — usually serious |

### Common Status Codes

| Code | Name | Meaning |
|---|---|---|
| **200** | OK | Request completed successfully |
| **201** | Created | A new resource was created (e.g. new user, new post) |
| **301** | Moved Permanently | Resource has permanently relocated |
| **302** | Found | *Temporary* redirect — may change again |
| **400** | Bad Request | Something wrong/missing in the request (e.g. missing expected parameter) |
| **401** | Not Authorised | Must log in to view this resource |
| **403** | Forbidden | No permission to view this resource, regardless of login state |
| **404** | Page Not Found | Requested resource doesn't exist |
| **405** | Method Not Allowed | Wrong method used (e.g. GET sent where POST was expected) |
| **500** | Internal Server Error | Server hit an unhandled error |
| **503** | Service Unavailable | Server overloaded or down for maintenance |

> [!tip] Visual Reference
> The room recommends [http.cat](https://http.cat/) for a visual/memorable way to learn status codes.

> [!question]- 🧪 Quick Quiz: HTTP Status Codes
> 1. What code range indicates a client-side error? A server-side error?
> 2. What status code would you get after successfully creating a new blog post?
> 3. What's the difference between 401 and 403?
> 4. What code indicates a resource simply doesn't exist?
> 5. If a server can't reach its database and crashes mid-request, what status code range would that likely fall in?
> 6. What code would you get sending a GET request to an endpoint that only accepts POST?
>
> **Answers**
> 1. Client errors = 400–499; server errors = 500–599.
> 2. 201 Created.
> 3. 401 means you need to authenticate (log in) to access the resource; 403 means you're forbidden regardless of login status.
> 4. 404 Page Not Found.
> 5. 500 Internal Server Error (500–599 range).
> 6. 405 Method Not Allowed.

---

## 5. Headers

Headers are extra data sent alongside a request or response. Not strictly required, but essential for a functional web experience.

### Common Request Headers (Client → Server)

| Header | Purpose |
|---|---|
| **Host** | Specifies which site to serve, if the server hosts multiple sites |
| **User-Agent** | Identifies the browser/software making the request |
| **Content-Length** | Tells the server how much data to expect (e.g. form submissions) |
| **Accept-Encoding** | Which compression methods the client supports |
| **Cookie** | Data sent back to help the server "remember" the client |

### Common Response Headers (Server → Client)

| Header | Purpose |
|---|---|
| **Set-Cookie** | Instructs the client to store data, sent back on future requests |
| **Cache-Control** | How long to cache this response before re-requesting |
| **Content-Type** | What type of data is being returned (HTML, CSS, JS, image, PDF, video, etc.) |
| **Content-Encoding** | What compression method was used on the returned data |

> [!question]- 🧪 Quick Quiz: Headers
> 1. Which header tells a server which specific website (among several hosted) you want?
> 2. Which header tells the browser what kind of data it just received?
> 3. Which request header identifies your browser?
> 4. Which response header instructs the browser to store data for future requests?
> 5. Why might Content-Length matter when submitting a form?
>
> **Answers**
> 1. Host.
> 2. Content-Type.
> 3. User-Agent.
> 4. Set-Cookie.
> 5. It tells the server exactly how much data to expect, letting it confirm nothing was cut off or lost during submission.

---

## 6. Cookies

**Cookies** = small pieces of data stored on your computer, saved when a server sends a **`Set-Cookie`** header. On every subsequent request, your browser sends that cookie data back.

> [!tip] Why Cookies Exist
> HTTP is **stateless** — it doesn't remember previous requests on its own (recap from [[Client-Server Basics]]). Cookies solve this by letting the server "remember" who you are, your preferences, or whether you've visited before.

> [!warning] Most Common Use: Authentication
> Cookies are commonly used for login sessions. The cookie value is typically not a readable password — it's a **token**: a unique, hard-to-guess secret code.

### Viewing Your Own Cookies
Open browser DevTools → **Network** tab → click a request → check the **Cookies** tab for what was sent/received.

> [!question]- 🧪 Quick Quiz: Cookies
> 1. Which header creates/sets a cookie on the client?
> 2. Why does HTTP need cookies at all?
> 3. What does a cookie typically contain for authentication purposes — a plaintext password or something else?
> 4. Where in browser DevTools would you check what cookies are being sent?
>
> **Answers**
> 1. Set-Cookie.
> 2. Because HTTP itself is stateless — cookies let the server persist identity/preferences across otherwise independent requests.
> 3. A token — a unique, hard-to-guess secret code, not a plaintext password.
> 4. Network tab → click a specific request → Cookies tab.

---

## 🧠 Key Takeaways
- **HTTP** = the protocol for transmitting webpage data; **HTTPS** = encrypted HTTP, adding privacy + server authenticity.
- A **URL** breaks down into: Scheme, User, Host, Port, Path, Query String, Fragment.
- Every HTTP exchange = a **request** (method + headers) and a **response** (status code + headers + body).
- **Methods**: GET (read), POST (create), PUT (update), DELETE (remove).
- **Status codes**: 1xx info, 2xx success, 3xx redirect, 4xx client error, 5xx server error.
- **Headers** carry metadata both directions — Host/User-Agent/Cookie (request) and Set-Cookie/Content-Type/Cache-Control (response).
- **Cookies** solve HTTP's statelessness — small stored data (often auth tokens) sent back on every request via the Cookie header.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Break down every part of this URL: `https://admin:pass123@shop.example.com:8443/products?id=42#reviews`
> 2. Write a minimal example HTTP GET request with Host and User-Agent headers.
> 3. Match each HTTP method (GET/POST/PUT/DELETE) to a real action you'd take on a social media profile.
> 4. List all 5 status code ranges and one example code from each.
> 5. Explain why cookies are necessary given that HTTP is stateless.
> 6. What's the difference between a 401 and a 403 status code, and give a real scenario for each.

## 🔗 Related Notes
- [[Client-Server Basics]]
- [[DNS in Detail]]
- [[OSI Model]]
- [[Networking Protocols - TCP UDP Packets Frames Ports]]
- [[What is Networking]]
- [[Networking MOC]]

## 📌 Next Steps
- [ ] Use browser DevTools → Network tab to inspect a real request/response on a site you use daily — identify the method, status code, and at least 3 headers
- [ ] Check your own browser's cookies for a logged-in site and see if you can identify the session token
- [ ] Revisit quiz sections for spaced repetition
