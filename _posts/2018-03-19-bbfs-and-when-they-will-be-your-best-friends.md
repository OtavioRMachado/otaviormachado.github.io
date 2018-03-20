---
layout: post
title: "BFFs and when they will be your best friends."
date: 2018-03-19 22:57:40
image: '/assets/img/'
description:
tags:
- TIL
- BFFs
- Architecture
- Patterns
categories:
- TIL
twitter_text: 'What are BFFs and when they will be your best friends.'
---

**tl;dr:**

BFF stands for **Back-end For Front-end**, now you can go on with your life.

**long version:**

I can tell you straight away what exactly a BFF is and what it is used for, but I think doing some reasoning before will help you understand why it exists and when you should apply it. This is why I may be going **way** back, but bear with me.
### What is the responsibility of the front-end?
Basically, what runs on the user's end. A webpage, for example.

When you think of the front-end responsibilities, which words come to mind?

I am hoping you answered at least some of these:

* User experience;
* Appearance;
* Information Architecture;
* Usability;
* Accessibility;
* Validating inputs.

So, yeah. In my understanding, the front-end is (ideally) basically where you interact with your user, where you expose user-related information and where you do some basic validation to understand if your user is not doing anything unexpected before asking something to who actually owns everything: **the back-end**.

### What is the responsibility of the back-end?
What about the back-end? What are its responsibilities?

* CRUD (Creates/Reads/Updates/Deletes) data;
* Validates inputs;
* Organizes data;
* Has lots and lots of business logic;
* Usually accesses different services to get different kinds of data;

When you're logging into Facebook, it's a back-end service that verifies whether your username and password are correct. And there is another service that shows you your profile data, and another one that loads your news feed, and the list goes on.

Can they all be the same service underneath? Yes, they can. But they are, essentially, different services, and it does not matter whether they are the same service or not.

### When the BFF comes into play.
If you take facebook's example, there is a noticeable difference between a user's experience in the web client, in the mobile web, in the mobile app for Android and in the mobile app for iPhone. Here are two examples:

(Image web client)
(Image iPhone app client)

You can see that, on the web client, we have advertisements (suprise: this comes from an ad service), whereas on the iPhone app, we have the market store icon (that also comes from where? **a service**!)

This means that there are different data that have to be loaded for each different way a user accesses Facebook. This is the situation where the **back-end for front-end** pattern shines.

The BFF comes as an alternative for this problem. I am not saying that you cannot have a big back-end that gives all different kinds of front-ends their data, but if you do have that, you may run into some problems, like **multiple teams messing with the same code base**, **specific business logic crammed together in a blob of awful code** or **performance issues**.

You should not need to load the market store for the web client. You should not have to find advertisements for the iPhone app if you are not showing them. And most of all, different teams should not be messing with the same back-end if you don't want to end up with spaghetti code.

![The saviour](http://philcalcado.com/img/2015-09-back-end-for-front-end-pattern/sc-bff-2.png)

<center>_Example of a BFF architecture_ ([thanks, Phil](http://philcalcado.com/2015/09/18/the_back_end_for_front_end_pattern_bff.html))</center>

This way, you can focus on getting only the right data, formatting the data exactly the way you are going to need it in the front end, and give your team all the freedom they want and need to develop things without needing to integrate with others, align backlogs and all that.

You may have some questions, as:


* **But I am a front-end/back-end only developer! (angry/sad face)**

You can keep being specialized. It just means that the team organization should be more diverse.

* **But there will be a lot of duplicated code!**

There **may** be a lot of duplicated code. I mean, there is always a trade-off, right? I would prefer having duplicated code than spaghetti code and angry development teams fighting to keep a unique back-end.

If it is still not the case, that is okay. If your different kinds of application access the same data and the teams are organized in a way that no one screams with each other, that is fine for now.

This is not a silver bullet. You should not use a BFF for every possible problem you can apply. There are always upsides and downsides to every solution and the path you take may be the right one for now, but you may have to change it in the future.

I hope you are now able to understand what a BFF is and when you should use it. If something is not well explained, please, leave me a message.

If you want a deeper introduction to the subject, you can start [here](https://samnewman.io/patterns/architectural/bff/), [here](https://nordicapis.com/building-a-backend-for-frontend-shim-for-your-microservices/) and [here](http://philcalcado.com/2015/09/18/the_back_end_for_front_end_pattern_bff.html).
