---
layout: post
title: All About Authentication and Authorization
excerpt: "This is a brief overview of some the types of authentication and authorization when creating web and mobile apps."
tags: [authentication, authorization, web applications, mobile, oauth, openid]
modified: 2015-02-08
comments: true
---

What is Authentication?

What is Authorization?

Older type of Authentication considered insecure for modern apps

Current Types
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

How it works?
Who uses it?
Pros
Cons
Resources

Implicit vs Explicit
Use with SSL

Suggestions
Find
-->