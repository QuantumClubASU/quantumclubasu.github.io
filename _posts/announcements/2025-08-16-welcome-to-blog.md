---
title: Welcome to our Blog
description: Introducing to our Club's Blog
author: vinayak
date: 2025-08-16 01:03:00 -0700
categories: [Announcements, General Information]
tags: [announcements, general]
pin: true
math: true
comments: true
mermaid: true
render_with_liquid: true
---
{% assign parts = page.path | split: '/' %}
{% assign filename = parts[2] | split: '.' | first %}
{% assign image_path = site.post_image_path | append: '/' | append: parts[1] | append: '/' | append: filename %}


![Light mode only]({{image_path}}/LogoBoxDark.png){: .light }{: width="500" }
![Dark mode only]({{image_path}}/LogoBox.png){: .dark }{: width="500" }
