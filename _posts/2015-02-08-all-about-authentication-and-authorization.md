---
layout: post
title: All About Authentication and Authorization
excerpt: "This is a brief overview of some the types of authentication and authorization when creating web and mobile apps."
tags: [authentication, authorization, web applications, mobile, oauth, openid]
modified: 2015-02-08
comments: true
---
Coming soon.

<!--
What is Authentication?
Authentication is being able to confirm the identity of someone or something. Usually this is accomplished by the client supplying a unique password, token or some other unique identifier that only the client would know.

What is Authorization?
Is confirming that the authenticated client has adequate credentials to access something specific such as an administration page.

Some older types of Authentication considered insecure for modern apps that require secure access:
Basic Authentication
Digest Authentication
#

Current Types
Forms Authentication
OAuth 2.0 - Facebook, Google,
OAuth 1.x - Twitter
MFA
Passwordless [here](https://hacks.mozilla.org/2014/10/passwordless-authentication-secure-simple-and-fast-to-deploy/)
  1. The site/app asks the users for for their email or phone number.
  2. The user receives a one time password/token via email or text to login.
  3. The user uses the link with tht token to login to the site
  4. The server logs the user in and uses a session to keep the user logged in while on the site

  Very simple to setup
  No email verification steps
  No passwords to remember

  Tokens in plain text to email
  Users aren't used to this flow and may think it's not as easy
  Potential for emails or texts to not arrive or go to junk mail

User IDs: Email or username?
    Should be case insensitive.

    Email
    Unique
    Verifiable
    How to fix the problem of losing the email address?
    Problems verifying that it is valid. Local part is unfortunately case sensitive. The domain part is not. Weird.

    Check for presence of at least one @ symbol in the address
    Ensure the local-part is no longer than 64 octets
    Ensure the domain is no longer than 255 octets
    Ensure the address is deliverable
    [link](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)

    Username
    Good if publicly visible
    What else?

Passwords

Complexity Recommendations [link](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
    Password must meet at least 3 out of the following 4 complexity rules
    at least 1 uppercase character (A-Z)
    at least 1 lowercase character (a-z)
    at least 1 digit (0-9)
    at least 1 special character (punctuation) — do not forget to treat space as special characters too
    at least 10 characters
    at most 128 characters
    not more than 2 identical characters in a row (e.g., 111 not allowed)

    Clearly state your password rules when creating an account and changing your password.
    Require uses to enter their password twice to avoid password resets from typos.
    Allow users to retrieve forgotten passwords.
    Don't store passwords and don't implement hash storage unless a vetted library is not available and if it isn't read [this](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet)
    Only transmit passwords and secure tokens over TLS/SSL.
    Re-authenticate to update sensitive info like password and email address. This will prevent a compromised session from being used.


    Requiring long complex passwords will make your servers less of a target for hackers. Your site won't be unhackable, but at least they'll target your competitor instead.

    Prevent brute force by slowing down tries. Exponentially increasing is a good option.

Forms Based
OAuth - Permission / Authorization
OpenId - Consumer
SAML - Enterprise
FIDO - Passwordless and Universal two factor

How it works?
Who uses it?
Pros
Cons
Resources

OAuth for login

Implicit vs Explicit
Use with SSL

Suggestions
Find
-->