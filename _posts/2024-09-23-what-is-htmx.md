---
layout: post
title:  "What is HTMX?"
date:   2024-09-23 11:00:00
categories: [learning,htmx]
---

HTMX is a great tool for enhancing your HTML skills, allowing you to handle modern interactions in web apps without heavy reliance on JavaScript frameworks like React, Angular, or Vue. Unlike those full-fledged frameworks, **HTMX** lets you work primarily with **HTML** while still having access to dynamic web functionality like server-side rendered UIs, partial updates, and more.

Let’s dive into HTMX step by step:

---

### 1. **What is HTMX?**
[**HTMX**](https://htmx.org/) is a lightweight JavaScript library that allows you to directly write declarative AJAX in HTML. It enables your webpage to work like a modern web application by making **HTTP requests** (GET, POST, PUT, DELETE, etc.) directly from HTML elements (e.g., buttons, forms, divs) without writing custom JavaScript.

- **Main goals**:
  - Simplify complex client-server interactions.
  - Let HTML take back the responsibility of handling interactions and data fetching.
  - Avoid reliance on large JavaScript frameworks.

---

### 2. **Getting Started with HTMX**
HTMX is very simple to add to your project. You include the library in your HTML, and you're good to go!

#### a. **Install HTMX**
You can load HTMX in your project directly from a CDN.

```html
<script src="https://unpkg.com/htmx.org"></script>
```

#### b. **Basic Example**
To get started, all you need to do is add a few attributes to your HTML. This attribute-driven approach is what makes HTMX so powerful, as you don’t have to write any custom JavaScript for interactions.

Let’s take a simple example where clicking a button fetches some content from the server and injects it into a `div`.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/htmx.org"></script>
    <title>HTMX Example</title>
</head>

<body>

    <!-- The button triggers a GET request to /hello when clicked -->
    <button hx-get="/hello" hx-target="#output">Click me for greeting</button>

    <!-- The server response will be injected here -->
    <div id="output"></div>

</body>

</html>
```

Here’s what each of the **HTMX** attributes does:
- **`hx-get="/hello"`**: Defines the HTTP method (`GET` in this case) and URL (`/hello`).
- **`hx-target="#output"`**: Specifies the target element where the server response should be injected (the `div` with id `output`).

When the button is clicked, it makes an **HTTP GET** request to the `/hello` endpoint, and the server's response will be injected into the `#output` div.

---

### 3. **HTMX Attributes**
HTMX is built around the concept of augmenting HTML elements with additional attributes, enabling you to work declaratively. Here’s a list of some key HTMX attributes you'll work with:

- **`hx-get` / `POST` / `PUT` / `DELETE`:** Triggers a specified HTTP request on interaction (click, submit, etc.).
  
  ```html
  <button hx-post="/submit" hx-target="#result">Submit Data</button>
  ```

- **`hx-trigger`:** Defines the event that will trigger the request (by default, it’s `click` for buttons and links).

  ```html
  <input hx-get="/autocomplete" hx-trigger="keyup changed" hx-target="#suggestions">
  ```

- **`hx-target`:** Specifies where to inject the server response (by default, HTMX assumes it's the triggering element).

- **`hx-swap`:** Determines how the returned content should be swapped into the target element (by default, it's `innerHTML` but there are other options such as "beforebegin," "afterbegin", etc.).

- **`hx-vals`:** Passes custom values along with the request in JSON format.

---

### 4. **Practical Examples**
Now, let’s apply HTMX to some common web application use cases:

#### a. **Handling a Simple Form**
We’ll enhance a form submission with no JavaScript by using HTMX to make an AJAX POST request.

```html
<form hx-post="/submit-form" hx-target="#form-result">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name">
    <button type="submit">Submit</button> 
</form>

<div id="form-result"></div>
```
In this case:
- The form will be submitted to `/submit-form` using the **POST** method.
- The response will be injected into the `#form-result` div (it can be a success message, validation error, or new content).

#### b. **Polling / Live Updates**
HTMX can handle polling, which is useful if you need to show live data like stock prices or notifications.

```html
<!-- Poll server for updates every 10 seconds -->
<div hx-get="/live-updates" hx-trigger="every 10s" hx-swap="outerHTML">
    <p>Waiting for updates...</p>
</div>
```

This will trigger an HTTP GET request to `/live-updates` every `10` seconds and replace the `<div>` content.

#### c. **Loading Partial Content**
Sometimes, you only want to load part of a page. Instead of reloading the whole page, HTMX can request just a piece of HTML and inject it where needed, keeping the user interaction smooth.

For example, imagine a table where you want to load more rows when a user clicks "Load more":

```html
<table>
    <tbody id="table-rows">
        <tr><td>Row 1</td></tr>
        <tr><td>Row 2</td></tr>
    </tbody>
</table>
<button hx-get="/load-more" hx-target="#table-rows" hx-swap="afterend">Load more</button>
```

This will append new rows to the `<tbody>` without reloading the entire table.

---

### 5. **Swap Types**
HTMX supports several ways to modify how the server’s response is injected into the DOM. By default, it replaces the **`innerHTML`** of the target element, but you can change this behavior using the **`hx-swap`** attribute.

- **`innerHTML`** (default): Replaces the target element’s content with returned content.
- **`outerHTML`**: Replaces the target element itself.
- **`beforebegin`**: Inserts the content before the target element (outside the target).
- **`afterbegin`**: Inserts the content at the beginning inside the target element.
- **`beforeend`**: Inserts content at the end of the target element.
- **`afterend`**: Inserts the content after the target element.

Example:
```html
<div hx-get="/new-content" hx-target="this" hx-swap="beforeend">
    Existing content
</div>
```
In this case, newly fetched content will be appended inside the `div`.

---

### 6. **Working with JSON**
While HTMX primarily deals with HTML, you can also handle JSON data. Usually, just point the request to an endpoint that returns JSON and use a callback. You can use **`hx-ext="json-encapsulation"`**, or extract JSON from the response and allow it to update specific DOM elements.

```html
<!-- Expecting JSON data from the server -->
<button hx-get="/info.json" hx-target="#output" hx-ext="json-encapsulation">
    Get JSON Info
</button>

<div id="output" hx-swap-oob="true"></div>
```
HTMX also has its own built-in support for processing JSON with its `hx-vals`.

---

### 7. **Progressive Enhancement**
HTMX excels at **progressive enhancement**. You can start with a fully static website and incrementally enhance certain areas with interactive behavior. If JavaScript is disabled on the client side, your project will still work perfectly, gracefully degrading back to a normal HTML form-driven web page.

### 8. **Integrating HTMX in a Backend Stack**
HTMX is backend-agnostic, meaning it works seamlessly with almost all popular server-side frameworks (e.g., Django, Flask, Rails, Laravel, Express.js). Here is an overall flow:
1. The frontend sends requests via HTMX.
2. The backend processes the request and responds with appropriate HTML which HTMX injects into the page.

For example, in Express.js, you could send small HTML fragments from the server:
```javascript
app.get('/hello', (req, res) => {
    res.send('<p>Hello HTMX!</p>');
});
```

In Django, it could look like:
```python
def hello(request):
    return HttpResponse('<p>Hello HTMX!</p>')
```

---

### 9. **Useful Resources for HTMX**
- **Official Documentation**: [htmx.org](https://htmx.org) - Comprehensive and full of examples.
- **HTMX Explained**: [Intro to HTMX](https://htmx.org/docs/#introduction) - Read a basic intro to get started with more examples and use cases.
- **Watch Videos**: Check YouTube for various **HTMX** tutorials for real-time follow-ups.

---

### 10. **Next Steps**
- **Build a CRUD application**: Now that you’ve got the basics, try building a full CRUD app (Create, Read, Update, Delete) where interaction happens without page reloads. HTMX shines in these scenarios.
- **Explore Advanced Features**: Features such as WebSockets and Server-Sent Events (SSE) allow you to build real-time applications with minimal JavaScript.