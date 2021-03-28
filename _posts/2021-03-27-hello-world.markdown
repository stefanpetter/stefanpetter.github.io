---
layout: post
title:  "Hello World!"
date:   2021-03-27 18:55:05 +0200
categories: website blog
---
Hello World! Welcome to my brand spanking new website. For some time now, I wanted to write blogs about awesome Azure/tech related stuff, and here we are! A proper introduction of myself will follow later. Let's talk tech! How did this website came to life? 

There are a million different ways of creating and hosting a website. The choice we make is often influenced by experience. I created a lot of websites in the past based on free HTML templates, backed by a custom PHP framework and a good 'ol MySQL database. However, this time I wanted to do things differently. 

This website wil host blogs. Blogs are simple static content, so a database is not needed. Whilst searching for ways to host a static website, I came across [Github Pages][github-pages]. A free and simple way to host a static website.

< Insert story about WSL2 not working nicely here >

After a lot of struggling with getting ruby/bundler/jekyll to work, blogs now can easily be added by writing it in a markdown file and pushing it to a repository :) Github (Actions) will take care of the CI/CD stuff and before you know it, the blog is live!

[github-pages]: https://pages.github.com/