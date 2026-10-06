---
title: A whole new blog!
date: 2026-10-05T20:32:00
description: ''
tags: []
---

I decided to reset my blog from scratch! It all started because [I happened to mention how easy it is to start a blog on GitHub Pages](https://ursal.zone/@gustavo/117372789749280829) while mine was completely abandoned. So I decided to fix mine up: threw everything I had away and now it's a brand new blog.

This blog started way back on Tumblr. It was a simple time: you could post images, schedule posts, it was simple, but it worked. Only it was terrible too, that Tumblr post editor was terrible, and I didn't have much control over the blog style either.

Then I migrated to GitHub Pages using Jekyll. In the beginning, I posted by writing Markdown, but it didn't last about five or seven posts, I made a script that allowed me to write in Google Docs and it posted using a scheduled task. Back then I had a plan to post every day, and I wrote about all those anime I watched. Actually, I just wanted to earn an achievement for committing to GitHub every day.

Except there was one thing I didn't like: sometimes I would write something in Google Docs and when it appeared on the site, there was some bug caused by the Google Docs→Markdown conversion. So I decided to migrate the site to WordPress, keeping the hosting on GitHub Pages. There are plugins for that (WP2Static, Simply Static) but they suck, so I ended up using HTTrack and a script to fix the issues that popped up (removing wp_json, wp_admin, and other things from the code).

It lasted a little while like that, but I found it kind of a pain: I couldn't edit posts on my phone at all (the WordPress app wouldn't connect to my local instance no matter what) and it was very slow. That's when I thought about moving to a more robust solution:

I thought: if the blog was generated in JavaScript, I could have the same code that runs during blog generation in the editor, so I can have an editor that is faithful to how the posts will appear on the blog. Besides that, I could already implement a multi-language blog and post in English too. Only it was more complicated than it seemed: I tried using Nuxt, made a veeery simple site, and abandoned it. I didn't have time to make a specific editor for my case nor finish fixing the layout.

Now I'm using Hugo and Sveltia CMS. Hugo is fast and, unlike the others, already has native support for multi-language blogs. I found a good theme that was easy to tweak the way I like and I can improve it in the future. I'm using Sveltia CMS to write this post and it's very practical: no Netlify account needed, actually, better than that, it allows editing the blog without messing with any account, it's very good.

The only thing I end up missing is that I can't view the post on the blog in real-time like I could in WordPress, nor do I have the blocks to align images to the left or right or even full screen. But, better to have something simpler than to abandon it again.

And that's it, a whole new blog! Whoever got the reference, know that in the Portuguese post the reference is from another song. And that's the cool thing about multi-language blogs: it's not a machine translation from one language to another, I give it my own touches here and there.
