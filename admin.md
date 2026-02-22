# Cookie Check and Key Remover Code Snippets

## 1. Cookie Check Snippet
Add this snippet to any HTML page to check for the `access` cookie. If the cookie is missing or invalid, it redirects the user to the main page (`index.html`).

```html
<script>
    function checkCookie() {
        const cookies = document.cookie.split("; ");
        const cookie = cookies.find(row => row.startsWith("access="));
        if (!cookie || cookie.split("=")[1] !== "1") {
            window.location.href = "/index.html"; // Redirect to main page
        }
    }

    window.onload = checkCookie; // Run the check when the page loads
</script>
```

---

## 2. Key Remover Snippet
Add this snippet to any HTML page to allow users to delete the `access` cookie using a button or the "Escape" key (panic key).

```html
<script>
    function deleteCookie() {
        document.cookie = "access=; path=/; expires=Thu, 01 Jan 1970 00:00:00 UTC;";
        document.getElementById("message").textContent = "The access cookie has been deleted. Redirecting to the main page...";
        setTimeout(() => {
            window.location.href = "/index.html"; // Redirect to main page after deletion
        }, 2000); // Delay before redirect
    }

    function panicKeyHandler(event) {
        if (event.key === "Escape") { // Triggered when the "Escape" key is pressed
            deleteCookie(); // Delete the cookie and redirect
            document.getElementById("message").textContent = "Panic key triggered! The access cookie has been deleted. Redirecting to the main page...";
        }
    }

    window.onload = function() {
        document.addEventListener("keydown", panicKeyHandler); // Attach panic key listener
    };
</script>
```

### Example Usage
To use the key remover snippet, add this button and message placeholder to your HTML page:

```html
<button onclick="deleteCookie()">Delete Access Cookie</button>
<p id="message"></p>
```

---
