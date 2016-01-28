---
layout: post
title: "SQL Injection attack - Why should I care?"
date: 2016-01-27 15:55:41
image: '/assets/img/'
description:
tags:
- OWASP
- Security
categories: 
- OWASP Top10
twitter_text: What is an SQL Injection and why should I care? - On Code Bucket
---

This post is part of a compilation talking about the ten most common security flaws for web applications. To see them all, [click here](/tags/#OWASP).

***

### What is an injection attack?  
[OWASP](https://www.owasp.org) defines the SQL Injection flaws as

> Injection flaws, such as SQL, OS, and LDAP injection occur when untrusted data is sent to an interpreter as part of a command or query. The attacker's hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.

So, if your application uses untrusted data in the construction of SQL calls, like
```java
String query = "SELECT * FROM accounts WHERE custID=" + request.getParameterId("id");
```

Or if your application is trusting blindly in frameworks, using queries such as:
```java
Query HQLQuery = session.createQuery("FROM accounts WHERE custID=" + request.getParameterId("id");
```

Then your application is vulnerable to a SQL Injection Attack.

### What can be the impacts of an Injection Attack?
They vary greatly from getting restricted information, to data loss or corruption, lack of accountability, or denial of access. It can, sometimes, lead to complete host takeover.

### How can I protect my application from Injection?
The best way to protect your application is guaranteeing that all commands your interpreter is running are separating untrusted data from the command or query.

There are several ways to do that. You can use a parameterized API - just be careful with APIs like stored procedures - to avoid the use of the interpreter entirely, escape special characters using the specific escape syntax for that interpreter or even have a "white list" input validation. 
OWASP provides us some [escaping routines](http://owasp-esapi-java.googlecode.com/svn/trunk_doc/latest/org/owasp/esapi/Encoder.html) as well as some [white list input validation routines](http://owasp-esapi-java.googlecode.com/svn/trunk_doc/latest/org/owasp/esapi/Validator.html) to use.

