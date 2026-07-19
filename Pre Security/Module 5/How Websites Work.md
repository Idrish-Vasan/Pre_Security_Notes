---
title: How Websites Work
source: TryHackMe (Web Fundamentals module)
platform: TryHackMe
module: Web Fundamentals
tags: [cybersecurity, tryhackme, html, javascript, web-development, html-injection, sensitive-data-exposure, beginner]
status: in-progress
---

# 🕸️ How Websites Work

> [!info] Room Info
> **Module:** Web Fundamentals (new module — builds on [[HTTP in Detail]])
> Goal: Understand the front end/back end split, HTML structure, JavaScript's role, and two beginner-relevant web vulnerabilities — Sensitive Data Exposure and HTML Injection.

---

## 1. How Websites Work

When you visit a website, your browser (Chrome, Safari, etc.) sends a **request** to a **web server** — a dedicated computer elsewhere — asking for the page. The server responds with data your browser uses to render the page.

> [!tip] Ties Back
> This is the exact request/response cycle covered in [[HTTP in Detail]] and [[Client-Server Basics]] — this room builds on that foundation to explain *what's actually in* the response.

### Two Major Components

| Component | Also Called | Role |
|---|---|---|
| **Front End** | Client-Side | How your browser **renders** the website |
| **Back End** | Server-Side | The server that **processes** your request and returns a response |

> [!question]- 🧪 Quick Quiz: How Websites Work
> 1. What does your browser send to a web server, and what does the server send back?
> 2. What's the difference between front end and back end?
>
> **Answers**
> 1. Your browser sends a request; the server sends back a response containing data used to render the page.
> 2. Front end (client-side) = how the browser displays/renders the site; back end (server-side) = the server logic that processes requests and generates responses.

---

## 2. HTML, CSS & JavaScript — The Building Blocks

| Language | Purpose |
|---|---|
| **HTML** | Builds the website and defines its structure |
| **CSS** | Styles the website (colors, layout, fonts) |
| **JavaScript** | Adds interactivity and complex functionality |

### HTML (HyperText Markup Language)

Built from **elements** (aka **tags**) — the building blocks telling the browser how to display content.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h1>A Heading</h1>
    <p>A paragraph.</p>
</body>
</html>
```

| Element | Purpose |
|---|---|
| `<!DOCTYPE html>` | Declares this as an HTML5 document — standardizes interpretation across browsers |
| `<html>` | Root element — every other element nests inside this |
| `<head>` | Page metadata (e.g. page title) |
| `<body>` | The actual visible content shown in the browser |
| `<h1>` | A large heading |
| `<p>` | A paragraph |
| *(many more)* | `<button>`, `<img>`, list tags, and countless others for specific purposes |

### Attributes

Tags can carry **attributes** — extra properties:

| Attribute | Example | Purpose |
|---|---|---|
| `class` | `<p class="bold-text">` | Style hook — **multiple** elements can share the same class |
| `src` | `<img src="img/cat.jpg">` | Specifies a resource location (e.g. an image file) |
| `id` | `<p id="example">` | **Unique** identifier for one specific element — used for styling and JavaScript targeting |

> [!note] class vs. id
> Multiple elements *can* share a `class`. An `id` must be **unique** to a single element on the page — that's the whole point of it.

> [!tip] Viewing Any Website's HTML
> Right-click → **"View Page Source"** (Chrome) or **"Show Page Source"** (Safari) — you can inspect the raw HTML of virtually any site.

### JavaScript (JS)

Controls **functionality** — without it, a page is static (no interactivity, no dynamic updates).

**Adding JavaScript to a page:**
```html
<!-- Inline in the page -->
<script>
  document.getElementById("demo").innerHTML = "Hack the Planet";
</script>

<!-- Or loaded from an external file -->
<script src="/location/of/javascript_file.js"></script>
```

**Example:** the code above finds the element with `id="demo"` and changes its content to `"Hack the Planet"`.

**Events** let HTML elements trigger JavaScript:
```html
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
```

> [!note] Events Can Live Elsewhere Too
> `onclick`/`onhover` handlers can be defined directly on an element (as above) **or** inside a `<script>` block — same effect, different organization.

> [!question]- 🧪 Quick Quiz: HTML, CSS & JavaScript
> 1. What role does each of HTML, CSS, and JavaScript play?
> 2. What's the root element of any HTML page?
> 3. What's the functional difference between the `class` and `id` attributes?
> 4. How can you view the raw HTML of any website you visit?
> 5. What happens to a webpage's interactivity if JavaScript is removed entirely?
> 6. Name two ways JavaScript can be added to an HTML page.
>
> **Answers**
> 1. HTML = structure/content; CSS = styling/appearance; JavaScript = interactivity/functionality.
> 2. `<html>`.
> 3. `class` can be shared across multiple elements (used for shared styling); `id` must be unique to one specific element (used for precise targeting/styling/JS).
> 4. Right-click → "View Page Source" (Chrome) or "Show Page Source" (Safari).
> 5. The page becomes static — no dynamic updates, no interactive elements respond to user actions.
> 6. Inline within `<script>` tags directly in the page, or loaded remotely via `<script src="...">`.

---

## 3. Security Issue: Sensitive Data Exposure

**Sensitive Data Exposure** occurs when a website fails to properly protect or remove sensitive clear-text information visible to the end user — typically found in the **frontend source code**.

> [!warning] Why This Matters
> Since anyone can "View Page Source" on any website, a developer who forgets to remove things like temporary login credentials, hidden links to private pages, or other sensitive data in HTML/JavaScript comments has effectively **published that data publicly**.

> [!example] Real Attack Scenario
> An attacker finds an HTML comment containing temporary login credentials while reviewing page source → uses those credentials to log in elsewhere on the application, or worse, to access backend components.

> [!success] Security Practice
> When assessing a web application, **reviewing page source code** for exposed credentials or hidden links should be one of the **first steps**.

> [!question]- 🧪 Quick Quiz: Sensitive Data Exposure
> 1. What is Sensitive Data Exposure, in one sentence?
> 2. Where is this type of vulnerability typically found?
> 3. Give a real example of what an attacker might find and exploit.
> 4. Why should reviewing page source be an early step in a security assessment?
>
> **Answers**
> 1. A website failing to properly protect/remove sensitive clear-text data visible to end users.
> 2. In the frontend source code (HTML, JavaScript, comments).
> 3. Login credentials left in an HTML comment, which an attacker could use to log in elsewhere on the app or access backend systems.
> 4. Because it's a quick, easy check that can reveal accidentally exposed secrets — a common and often overlooked developer mistake.

---

## 4. Security Issue: HTML Injection

**HTML Injection** occurs when **unfiltered user input is displayed on the page**. If a site fails to **sanitize** user input, an attacker can inject their own HTML (or JavaScript) into a vulnerable page.

> [!tip] What Is Sanitization?
> Filtering out "malicious" text a user submits, so it can't be interpreted as executable code/markup by the browser.

> [!example] How It Happens
> A form takes user input (e.g. "What's your name?") and passes it directly into a JavaScript function that writes it to the page. If the developer doesn't sanitize this input, a user can type `<h1>Hacked</h1>` instead of their name — and the browser will render it as an actual HTML heading, not plain text.

> [!warning] Related but Different: Database Injection
> This room briefly distinguishes HTML Injection (client-side — affects what's *displayed*) from **database injection** (manipulating a backend database query, e.g. to log in as another user) — a separate vulnerability class covered elsewhere.

> [!success] Core Security Principle
> **Never trust user input.** Developers must sanitize everything a user submits before using it anywhere in the page — e.g. stripping out HTML tags before displaying user-supplied text.

> [!question]- 🧪 Quick Quiz: HTML Injection
> 1. What causes HTML Injection to be possible on a website?
> 2. What does "sanitizing" user input mean?
> 3. Walk through a concrete example of how an attacker could exploit unsanitized input in a "What's your name?" field.
> 4. How does HTML Injection differ from database injection?
> 5. What's the core defensive principle developers should follow regarding user input?
>
> **Answers**
> 1. A website displaying unfiltered/unsanitized user input directly on the page.
> 2. Filtering out potentially malicious content (like HTML tags) from user-submitted text before it's used anywhere.
> 3. Instead of typing a name, the attacker types HTML (e.g. `<h1>Hacked</h1>`); if unsanitized, the browser renders it as an actual heading rather than literal text.
> 4. HTML Injection affects what's displayed on the client side; database injection manipulates backend database queries — different layers, different consequences.
> 5. Never trust user input — always sanitize it before using it anywhere in frontend or backend functionality.

---

## 🧠 Key Takeaways
- Website = **front end** (client-side rendering) + **back end** (server-side processing), connected via HTTP request/response (see [[HTTP in Detail]]).
- **HTML** structures content via elements/tags; **CSS** styles it; **JavaScript** makes it interactive.
- `class` = reusable style hook (many elements); `id` = unique per-element identifier.
- **Sensitive Data Exposure**: secrets accidentally left visible in frontend source — always check "View Page Source" during a security review.
- **HTML Injection**: unsanitized user input rendered as live HTML/JS — the fix is always **sanitize input**, never trust what a user submits.
- Both vulnerabilities in this note are frontend/client-side issues — a preview of the broader web security topics likely coming later in this module.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Trace the full flow of visiting a website, from browser request to rendered page.
> 2. Explain the roles of HTML, CSS, and JavaScript using an analogy of your choice.
> 3. What's the difference between `class` and `id`, and when would you use each?
> 4. Define Sensitive Data Exposure and explain how to check for it.
> 5. Define HTML Injection and explain the one core fix that prevents it.
> 6. Why is "never trust user input" considered a foundational security principle?

## 🔗 Related Notes
- [[HTTP in Detail]]
- [[Client-Server Basics]]
- [[DNS in Detail]]
- [[OSI Model]]
- [[Web Fundamentals MOC]]

## 📌 Next Steps
- [ ] Right-click → View Page Source on a few real websites you use and look for anything unusual in comments
- [ ] Try building a tiny HTML page with a form and an `id`-targeted JavaScript function to see injection risk firsthand (in a safe, local sandbox only)
- [ ] Revisit quiz sections for spaced repetition
