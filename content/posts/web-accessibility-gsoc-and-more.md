---
title: "Web Accessibility, GSoC, and More ft. Zendalona"
date: "2024-06-27"
summary: "A brief overview of web accessibility, Google Summer of Code, and more with Zendalona."
description: "A brief overview of web accessibility, Google Summer of Code, and more with Zendalona."
toc: true
readTime: true
autonumber: false
math: true
tags: ["gsoc", "accessibility", "web", "zendalona"]
showTags: false
hideBackToTop: false
---

## Intro

When I got the mail from Google Summer of Code a month ago, I was thrilled. I had been waiting for this moment for a long time. GSoC had almost been a lost hope for me this year too, but thanks to the stars (@Nalin, @Mukundan, @Sathyan, @Akshay), I was able to make it. The proposal I submitted was to work on a User Query Management System [^1] for [Zendalona](https://zendalona.com/). The idea was to take an existing ticketing system and make it more accessible, while also adding some new features for managing queries for Zendalona users. I was excited to work on this project and looked forward to the community bonding period.

During the community bonding period, I contacted polonel, the creator and maintainer of [Trudesk](https://trudesk.io), regarding the project and its aims. I also had a meeting with the Zendalona team to discuss the project and the timeline. The community bonding period was a great time to get to know the community and the project better. I also got to know the other GSoC students and the mentors. My mentors for the project are @Mukundan, @Akshay, and @Sathyan. They have been very helpful and supportive throughout the community bonding period.

## Web Accessibility

Web Accessibility is one of those things that is often overlooked by developers. It is important to make sure that the web is accessible to everyone, including people with disabilities. Web Accessibility is the practice of ensuring that websites are usable by people of all abilities and disabilities. Web standards have long evolved to include accessibility features, but many websites still do not follow these standards. This can be attributed to the fact that following those standards can be time-consuming and difficult. For the project, I will be working on making the User Query Management System more accessible. I know things might not be as easy as they seem, but I believe that it will be worth the effort.

For the past month, I have been going through the source code of Trudesk, finding accessibility issues, and trying to fix them. This might seem like a small task and, quite frankly, it did seem like that to me too. However, as I started working on it, I realized that it is not as easy as it seems. There are many places where the code is already screen reader-friendly, but there are also places where it is not even remotely accessible. Going through each component, checking where they're being used, identifying the type of component, and then deciding what ARIA roles to add is a tedious task, especially since I am new to this.

Another great challenge in starting was the sheer amount of work required just to set up the environment. The legacy JavaScript packages and code did not help! Thankfully, @Akshay came to the rescue. I bugged him a lot while trying to set up the development server on my system. Finally, after a lot of trial and error, we managed to get the server up and running. Our conversations actually taught me a lot about Node.js and a bit about its history, so that's a win-win.

Here's a link to my fork [anima-regem/trudesk](https://github.com/anima-regem/trudesk)

and

the original repo [polonel/trudesk](https://github.com/polonel/trudesk)

Here is the first ever commit I made [click me (edited)](https://github.com/polonel/trudesk/pull/679)




[^1]: User Query Management System: A system that helps the users to manage their queries and get the answers to their queries. It can also be called a ticketing system. Here's my proposal for the same:
[Proposal](https://summerofcode.withgoogle.com/programs/2024/projects/IMXwpDEG)
