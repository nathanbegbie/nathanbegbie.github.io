# Project: ArtificiallyIntelligent.info

## Project Description
A static blog website a technical blog, written in raw HTML and CSS without a framework.

## Tech Stack
- HTML
- CSS

## Conventions
- Use semantic HTML5 elements that clearly describe content meaning to browsers, search engines, and assistive technologies.
- Use <main> only once per page - Contains the primary content
- Structure headings logically - <h1> for page title, <h2> for major sections, etc.
- Wrap standalone content in <article> - Blog posts, news articles
- Use <section> for thematic groupings - Related content with its own heading
- Place tangential content in <aside> - Sidebars, author bios, related links
- Add id attributes to headings - Enable table of contents navigation
- Keep the styling of the site simple and easy to read
- Always ensure that the following tags are included in the <head> of each article
  - title
  - <meta name="description" content="..." >
  - <meta property="article:published_time" content="...">
  - If updated, include: <meta property="article:modified_time" content="...">
  - If updated, include: <meta name="last-modified" content="...">
  - Any other <meta> tags that you think are relevant and can increase SEO

## Project Structure
- /docs - Main source code for the site
  - styles.css - The only CSS page for the site
  - index.html - The home page of the site. It should list all articles in the site
  - sitemap.xml
  - robots.txt
  - other HTML documents, which are all articles

# Page Structure
Add Structured Data (JSON-LD) in your <head> section to improve SEO.

Explicitly tell search engines about article updates
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "...",
  "datePublished": "2021-10-12",
  "dateModified": "2025-08-31",
  "author": {
    "@type": "Person",
    "name": "Nathan Begbie"
  }
}
</script>
```

# CSS Styling
- Always start with mobile styles and progressively enhance for larger screens
- Use CSS variables for consistency and easy theming
- Use the default document flow, rely on margins for spacing between elements, padding for internal spacing and max-width + auto margins for centering
- Keep all styles in the `docs/styles.css` files, unless instructed otherwise do not use inline styles
- Use CSS nesting where possible
