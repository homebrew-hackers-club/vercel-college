---
title: Chapter 31
order: 31
---

# Custom Reporting

31

Chapter 31

It is also possible to use the built-in relayer Next.js Speed Insights uses and send the data to your own service or push them to Google Analytics.

Let's look at how we might add that now. We can add it to the demo app we have been optimizing.

We will use a console.log to look at the metrics in real time.

To do this we can leverage the reportWebVitals function provided by Next.js

Note: This is NOT necessary if you’ve just finished the previous
lessons.

```bash
npx create-next-app@latest nextjs-lighthouse --use-npm --example "https://github.com/vercel/next-learn/tree/main/seo"
```

Open pages/\_app.js and export the following function:

```javascript
export function reportWebVitals(metric) {
  console.log(metric);
}
```

Then build and start your application:

```bash
npm run build && npm run start
```

If you open up Chrome, you will see the metrics inside the DevTools console. You will also notice that FID will only trigger once you
interact with the page.

#### Further Reading

- Next.js: Measuring Performance

### You've Completed Chapter 31

Next Up

32: Other Tools

Was this helpful?