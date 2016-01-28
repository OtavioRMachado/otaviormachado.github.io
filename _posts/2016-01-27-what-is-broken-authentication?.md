---
layout: post
title: "What is a Broken Authentication flaw?"
date: 2016-01-27 17:46:37
image: '/assets/img/'
description:
tags:
- OWASP
- Security
categories:
- OWASP Top10
twitter_text: What is a Broken Authentication/Session Management flaw and what are their implications? - On Code Bucket
---

This post is part of a compilation talking about the ten most common security flaws for web applications. To see them all, [click here](/tags/#OWASP).

***

### What is a Broken Authentication flaw?
[OWASP](https://www.owasp.org) defines Broken Authentication and Session Management flaws as

> Application functions related to authentication and session management are often not implemented correctly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users' identities.

So, for example, if your application supports **URL rewriting**, putting session IDs in the URL, like:

```
http://example.com/sale/saleitems;jsessionid=2P0OC2JSNDLPSKHCJUN2JV?dest=Hawaii
```

When an authenticaded user of the example site sends the URL to one of their friends, they are also sending away their session ID. When one of their friends use the link, they will be able to use his session ID and credit card information;

Or when you don't set your application's timeouts are not set properly and one of your users access your application from a public computer and instead of logging out of their account, they simply close the browser tab. There's a good chance that any other person that tries accessing the same website in the same browser they just used, will be able to use their account;

Or even if an external attacker gains access to the system's password database and user passwords are not properly hashed, the attacker will be able to see all users' passwords;

If any of those scenarios define **Broken Authentication/Session Management flaws** in your application.

### What can be the impacts of Broken Authentication/Session Management flaws?
Flaws like this one may allow some, or even **all** accounts to be attacked. Once successful, the attacker can do anything the victim could do. Privileged accounts are frequently targeted.

### How can I prevent this from happening?
Having strong authentication and session management controls. Those controls should strive to:

- Meet the requirements defined in OWASP's [Application Security Verification Standards](https://www.owasp.org/index.php/ASVS) (ASVS) in the areas V2 and V3;
- Have a simple interface for developers. Consider [these](http://owasp-esapi-java.googlecode.com/svn/trunk_doc/latest/org/owasp/esapi/Authenticator.html) as good examples to emulate, use or build upon.
- Strong efforts should also be made to avoid XSS flaws which can be used to steal session IDs.

