---
layout: post
title: Authentication Meetup Notes
excerpt: "This is a brief overview of some the types of authentication and authorization when creating web and mobile apps."
tags: [authentication, authorization, web applications, mobile, oauth, openid]
modified: 2015-02-19
comments: true
---
#What is Authentication?
Authentication is the ability to confirm the identity of someone or something. Usually this is accomplished by the client supplying a unique password, token or some other unique identifier that only the client would know.
#What is difference between Authentication and Authorization?
Is confirming that the authenticated client has adequate credentials to access something specific such as an administration page.

#Authentication Types
* Basic Authentication
* Digest Authentication
* Forms
    * Username/password
    * Token
* OpenID - Authentication, Stackoverflow
* OAuth - Permission / Authorization
    * OAuth 2.0 - Facebook, Google, Microsoft
    * OAuth 1.x - Twitter
    * Implicit vs Explicit
* MFA / 2FA - Something you own - phone, keychain random number generator
* SAML - Enterprise
* FIDO - Enterprise?
* [Passwordless](https://hacks.mozilla.org/2014/10/passwordless-authentication-secure-simple-and-fast-to-deploy/)
    1. The site/app asks the users for for their email or phone number.
    1. The user receives a one time password/token via email or text to login.
    1. The user uses the link with that token to login to the site
    1. The server logs the user in and uses a session to keep the user logged in while on the site
    * Pros
        * Very simple to setup
        * No email verification steps
        * No passwords to remember
    * Cons
        * Tokens in plain text to email
        * Users aren't used to this flow and may think it's not as easy
        * Potential for emails or texts to not arrive or go to junk mail

#User IDs: Email or username?

* Email Address
    * Unique
    * Verifiable
* Username
    * Good option if publicly visible
    * What else?

#Email Considerations - [cheat sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
* Many sites screw up validating that the user entered a valid email
* How to fix the problem of losing the email address?
* Local part is case sensitive. The domain part is not. Weird.
* Validation Recommendations
* Check for presence of at least one @ symbol in the address
* Ensure the local-part is no longer than 64 octets
* Ensure the domain is no longer than 255 octets
* Ensure the address is deliverable

#Passwords - [cheat sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
* Complexity Recommendations
    * Password must meet at least 3 out of the following 4 complexity rules
    * at least 1 uppercase character (A-Z)
    * at least 1 lowercase character (a-z)
    * at least 1 digit (0-9)
    * at least 1 special character (punctuation) — do not forget to treat space as special characters too
    * at least 10 characters at most 128 characters
    * not more than 2 identical characters in a row (e.g., 111 not allowed)

    Clearly state your password rules when creating an account and changing your password.
    Require uses to enter their password twice to avoid password resets from typos.
    Allow users to retrieve forgotten passwords.
    Don't store passwords and don't implement hash storage unless a vetted library is not available and if it isn't read
    Only transmit passwords and secure tokens over TLS/SSL.
    Re-authenticate to update sensitive info like password and email address. This will prevent a compromised session from being used.

    Requiring long complex passwords will make your servers less of a target for hackers. Your site won't be unhackable, but at least they'll target your competitor instead. Prevent brute force by slowing down tries. Exponentially increasing is a good option.

# Example of Username/Password
1.  Click Login w/ username and password filled in
1.  Username and password are sent back to the server
1.  The server looks up the user based on the username, hashes the password and compares the stored hash
1.  The server generates and stores a token string for that user and sends it back
1.  The client stores the token to respond with it on every subsequent secure request

#Example of Facebook
1.  The user clicks the login with Facebook button
1.  The library opens up a popup window and sends a request to Facebook to see if the user is logged in
1.  If the user isn't logged in the popup prompt the user to login to Facebook
1.  The library then checks to see if the logged in user has given proper permissions to the Facebook app
1.  If the user hasn't the popup window ask the user to authorize the app
1.  Then either one of two things happens
1.  Either the library goes through the implicit grant process (full oauth for client side only) and retrieves the authentication token
1.  Or the library starts the explicit grant process and gets the request token from Facebook
1.  The client then sends either token to the server
1.  If the client sent the full authentication token the server will still need to validate the token and user
1.  Otherwise teh server itself will handle the rest of the Oauth process and get the valid authentication token
1.  The server will then generate a Bearer token (not Facebook) and return it to the client

#Example of Secure Requests
1.  The client makes a secure request and includes the Bearer token in the header
1.  The server verifies that the token is valid and not expired and then fufills the request
1.  If the token is invalid or expired return a 401 Unauthorized or 403 Forbidden
1.  If the client gets 403 response then prompt to login again


