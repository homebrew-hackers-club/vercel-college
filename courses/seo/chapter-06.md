---
title: Chapter 6
order: 6
---

# What is a robots.txt File?


A robots.txt file tells search engine crawlers which pages or files the crawler can or can't
request from your site. The robots.txt file is a web standard file that most good bots consume before requesting anything from a specific domain.

You might want to protect certain areas from your website from being crawled, and therefore indexed, such as your CMS or admin, user accounts in your e-commerce, or some API routes, to name a few. These files must be served at the root of each host, or alternatively you can redirect the root /robots.txt path to a destination URL and most bots will follow.

#### How to add a robots.txt file to a Next.js project

Thanks to static file serving in Next.js we can easily add a robots.txt file. , we would create a new file named robots.txt the public folder in the root directory. An example of what you could put in this file would be:

```txt
//robots.txt
 
# Block all crawlers for /accounts
User-agent: *
Disallow: /accounts
 
# Allow all crawlers
User-agent: *
Allow: /
```

When you run your app with yarn dev, it will now be available at http://localhost:3000/robots.txt . Note that the public folder name is not part of the URL.

Do not name the public directory anything else. The name cannot be changed and is the only directory used to serve static assets.

#### Further Reading

- Google: Create and Submit a robots.txt File
