---
layout: post
title: "Creating a Free Blog with Jekyll"
date: 2020-01-30 16:38:50
tags: Development Guide
image: jekyll-notext-light-transparent.png
---

 [Jekyll](https://jekyllrb.com/) is a free static site generator providing the functionality to write posts in markdown (a simple format of typing out plain text) for streamlined content creation. Since the generator outputs HTML files, no back-end is necessary. This lets the server to simply store your files as opposed to having to run processes on it, allowing for low cost hosting. For basic sites like this one, it's all you need.

This guide will provide the essential resources I use for creating and maintaining a free blog, along with a few tips.

## Getting Started with Jekyll

As they do a better job than I could, the steps to get Jekyll going are outlined in the [Jekyll docs](https://jekyllrb.com/docs/). From there, you can start designing your site. There are some free Jekyll themes, but I found the default minima theme to be a great starting point that gives enough functionality while leaving plenty of room to customize to your liking. Keep in mind that HTML and CSS knowledge are a prerequisite here. 

There is plenty of documentation on the Jekyll site and around the web to figure out how to do things, but I'll give one of my own tips. 

If you're using minima, check out the _includes and _layouts folders within the minima folder installed wherever Ruby was installed on your computer. This should be something like YOUR-RUBY-FOLDER/lib/ruby/gems/2.5.0/gems/minima-2.5.1. These are the files you're going to overwrite within your website folder to get personalized aspects of your website. This way, you can get an understanding of how their Liquid language works and how you can take advantage of it.

## Writing Posts

If you want to be able to update the site without knowing anything about web development, it can be done. In the folder _posts, you can write markdown posts. Markdown is quite simple to learn, with only a few syntactic additions to make a basic post. The main requirement for a markdown post in Jekyll is something called front matter. Front matter contains the variables for your post. For example, this is the front matter for this post.

```
---
layout: post
title: "Creating a Free Blog with Jekyll"
date: 2020-01-30 16:38:50
tags: Development Guide
image: jekyll-notext-light-transparent.png
---
```
Once you've made a new markdown post, it will automatically be added to your local website! Jekyll does this by using the language Liquid to create page templates and pull front matter from your posts. To actually have all these changes go on the internet, you'll have to host your website somewhere. 

## Hosting

Jekyll works intrinsically with [GitHub Pages](https://pages.github.com/) or can be hosted on some other provider like [Netlify](https://www.netlify.com/), which I use. Both of these options are free for static sites. I like Netlify as it is scalable, provides the potential to go beyond static (for a price), and maintains a clean workflow with Github (A software management system). Some other free options would be [Google Firebase](https://firebase.google.com/), [Amazon S3](https://aws.amazon.com/s3/), and [Zeit](https://zeit.co/). I don't have personal experience with these options. 

## Domain Name

A domain name is your address on the internet. For a completely free website, you could use a free one provided by the hosting company. If you would like a clean domain name without .netlify or your hosting equivalent appended to the end, then you'll have to buy one. I would suggest staying away from companies like GoDaddy or Domains.com, as they add on charges for services that come standard with [Google Domains](https://domains.google/). 

## Conclusion

This is a pretty barebones guide to getting a website going. There are some great fully fledged guides already out there, but I hope the resources are enough to let you know how to get a website going for free. 