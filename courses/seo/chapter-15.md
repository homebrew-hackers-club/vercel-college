---
title: Chapter 15
order: 15
---

# On Page SEO


At a high level, on page SEO refers to the headings and links that make up the overall structure of the page. Headings indicate importance in the document and links connect the web together.

#### Headings and H1

Headings help users understand the structure of a page and what they are going to read in the next paragraphs. They also facilitate the search engine's job
of understanding which parts of the page are the most important.

Headings go from 1-6 and Heading 1 tends to be thought of as the most important. It's recommended to use the H1 heading tag in each page. H1 should represent what the page is about and be similar to your title tag.

```javascript
function Page() {
  return <h1>Your Main Page Heading</h1>;
}
```

#### Internal Links

The internet is connected by links. Without links from one website to another, the internet probably wouldn't exist. Websites that receive more links tend to
represent websites that are more trusted by users.

Google started this principle with the invention of the PageRank Algorithm
.

The PageRank algorithm, at a high level, is an algorithm that goes through every link on a database and scores domains based on how many links they
receive (quantity) and from which domains (quality). Lots of links from spam websites most likely have little to no value.

A link from a big national press website, however, is likely very valuable for search engines. This is why links are important and you should always include them both internally between your page, and also externally to other websites. Links always need to use href in order to be used for PageRank calculations.

#### next/link

Next.js provides the Link component that enables client-side transitions between routes. A simple use case would look something like the following:

```html
function NavLink({ href, name }) {
  return (
    <Link href={href}>
      <a>{name}</a>
    </Link>
  );
}
 
export default NavLink;
```

The href prop is required and will correctly add the link to the anchor tag, which is vital for SEO. When Google crawls a page, it will crawl
and follow this link without relying on JavaScript.

However, if the child of Link is a custom component that wraps an a tag, you must add passHref to Link. This is necessary if you’re using libraries like styled-components. Without this, the a tag will not have the href attribute, which affects your site’s SEO.

How to use passHref:

```html
import Link from 'next/link';
import styled from 'styled-components';
 
// This creates a custom component that wraps an <a> tag
const RedLink = styled.a`
  color: red;
`;
 
function NavLink({ href, name }) {
  // Must add passHref to Link
  return (
    <Link href={href} passHref>
      <RedLink>{name}</RedLink>
    </Link>
  );
}
 
export default NavLink;
```

If you use ESLint, Next.js has a rule to protect against this happening.

#### Further Reading

- Next.js: Link
- Next.js: eslint-plugin-next
