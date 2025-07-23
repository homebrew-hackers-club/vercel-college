---
title: Chapter 5
order: 5
---

# What are HTTP Status Codes?

5

Chapter 5

HTTP response status codes indicate whether a specific HTTP request has been successfully completed.
There are many status codes, but only a handful are meaningful in an SEO context.

Let's take a look at them now.

#### 200

The HTTP 200 OK success status response code indicates that the request has succeeded.

In order for a page to be indexed on Google it must return status code 200. This is what you typically want to look for in
your pages in order for them to receive organic traffic. This is the default code that will be set when Next.js renders a page
successfully.

#### 301/308

The HTTP 301 Moved Permanently redirect status response code indicates that the resource requested has been definitively moved to the destination URL.

This is a permanent redirect. In general, this is the most widely used redirect type.

Redirects can be used for a variety of reasons, but the main one is to indicate that a URL has been moved from point A to point B. Redirects are needed to ensure that, if a content is moved from one place to the other, you do not lose current and potential clients and that the bots can continue to index your site.

Note: Next.js permanent redirects use 308 by default instead of 301 as it is the newer version and considered the better option.

The main difference between the two status codes is that a 301 allows for changing the request method from POST to GET, whereas a
308 does not.

You can trigger a 308 redirect in Next.js by returning a redirect instead of props in the getStaticProps() function.

```javascript
//  pages/about.js
export async function getStaticProps(context) {
  return {
    redirect: {
      destination: '/',
      permanent: true, // triggers 308
    },
  };
}
```

You can also use the permanent: true key in redirects set in next.config.js.

```
//next.config.js
 
module.exports = {
  async redirects() {
    return [
      {
        source: '/about',
        destination: '/',
        permanent: true, // triggers 308
      },
    ];
  },
};
```

#### 302

The HTTP 302 Found redirect status response code indicates that the resource requested has been
temporarily moved to the destination URL.

In most cases, 302 redirects should be 301 redirects. This may not be the case if you are redirecting users temporarily to a certain page (e.g. a promotion page) or if you are redirecting users based on location.

#### 404

The HTTP 404 Not Found client error response code indicates that the server can't find the requested
resource.

As noted above, pages that are moved should be redirected with a HTTP 301 status code to the new location. When this doesn't happen, URLs may return a 404 status code. 404 Status Codes are not necessarily bad by default, as it's the desired outcome if a user happens to visit a URL that doesn't exist, but they shouldn't be a frequent error within your pages as it could lead to lackluster search rankings.

Next.js will automatically return a 404 status code for URLs that do not exist in your application.

In some cases, you might also want to return a 404 status code from page. You can do this by returning the following in place of props:

```javascript
export async function getStaticProps(context) {
  return {
    notFound: true, // triggers 404
  };
}
```

You can create a custom 404 page that is statically generated at build time by creating pages/404.js.

Example:

```javascript
// pages/404.js
export default function Custom404() {
  return <h1>404 - Page Not Found</h1>;
}
```

#### 410

The HTTP 410 Gone client error response code indicates that access to the target resource is no longer available at the origin server and that this condition is likely to be permanent.

This is not used very often, but you might want to look for this status code if you are deleting content on your website that won't exist any more.

Examples where a HTTP 410 Gone might be wise to use include:

- E-Commerce: Products permanently removed from inventory.
- Forum: Threads that have been deleted by the user.
- Blog: Blog post removed from site.

This status code informs bots that they should never return to crawl this content.

#### 500

The HTTP 500 Internal Server Error response code indicates that the server encountered an unexpected condition that prevented it from fulfilling the request.

Next.js will automatically return a 500 status code for an unexpected application error. You can create a custom 500 error page that is statically generated at build time by creating pages/500.js.

Example:

```javascript
// pages/500.js
export default function Custom500() {
  return <h1>500 - Server-side error occurred</h1>;
}
```

#### 503

The HTTP 503 Service Unavailable server error response code indicates that the server is not ready to handle the request.

It's recommended to return this status code when your website is down and you predict that the website will be down by an extended period of time. This prevents losing rankings on a long-term basis.

### You've Completed Chapter 5

Next Up

6: What is a robots.txt File?

Was this helpful?