# Web Security and You
**by Oscar Meriday @OMerida**

Great resources is the [Open Web Application Security Project](http://owasp.org)

## Stupid Programmer Errors

* Direct URL access to a protected file
* Ability to URL hack to access unauthorized data (sensitive numbers in URL)

### Information Leaks

* Specifically: visible error handling in production
* Low security hashes.  Don't use MD5!  Always salt hashes!  Use password_hash in PHP.

### Password Guessing
* Login forms should not allow unlimited guesses
* Ratelimiting
* Two-factor authentication (something you know, something you have)
* Log and notify

## Various Attack Vectors

### SQL Injection

**Problem**: A user having the ability to send data that is directly interpreted by your SQL engine.

**Solution**: Use prepared statements ($pdo->prepare, $pdo->execute, $pdo->quote)

### Other Injections

* Command Injecction
* Unchecked File Uploads
* Code Injection (eval)

### Session Hijacking

**Problem**: One user 'becoming' another by taking over their session via impersonation.

**Solution**: Avoid 'session fixation'.  Don't use url cookies for your sessions.  Always regenerate session IDs on a change of access level.  Save an anti-hijack token to another cookie and session.  Require it to be present and match.  Salt on unique data (such as user agent).

### Session Fixation

**Problem**: A user being able to provide a known session ID to another user.

**Solution**: Don't use URL cookies for your sessions.  Set  `session.use_cookies`, `session.use_only_cookies`, `session.cookie_httponly

**Take 2**: Protect from more complicated fixation attacks by generating sessions on change of access level.  Also on logout.

### XSS (Cross-Site Scripting)

**Problem**: A user sending data that is executed as script

**Solution**: Treat everything from a user as suspect.  Escape to the situation, e.g., HTML, JS, etc.  FIEO: Filter input, escape output.  Don't forget about rewritten URL strings.

#### Reflected XSS

**Problem**: Directly echoing back content from the user

**Solution**: For HTML: htmlentities().  For JS: string pattern replacement.  XML: iconv() + string pattern replacement.

#### Stored XSS

**Problem**: You store the data, then later display it.

**Solution**: Same solution as reflected XSS.

#### DOM XSS

Someone pasting untrusted content into input.

**Problem**: What happens in JavaScript, stays in JavaScript.

**Solution**: Replace using function to manually replace angle brackets and quotes.  See jQueryEncoder.

#### CSRF (Cross Site Request Forgery)

**Problem**: A user having the ability to forge or force a request of behalf of another user.

**Solution**: Protect via CSRF token.  Make them specific to a form.

Symfony project has pretty good security component and will take care of a lot of this.

#### Clickjacking

One of the newest threats.  Lots of publicity when Twitter was hit.

**Problem**: Tricks the user into physically making a click on the remote website without realizing it

**Solution**: Use specific header to disallow site framing.  But doesn't work in all clients.  Use JS to make sure you're not displayed in an iframe.