# SEO & Discoverability Strategy

Building a beautiful, modern website is only half the battle. This project will serve as a practical deep dive into **Technical and On-Page Search Engine Optimization (SEO)** to ensure "Quattrini Colori Belle Arti" dominates local search queries and broader art supply keywords.

---

## Technical SEO Implementation Checklist

### 1. Semantic Architecture & HTML Structure
* Ensure strict adherence to document outline rules: only one `<h1>` per page representing the core topic.
* Use sectioning elements (`<main>`, `<nav>`, `<article>`, `<section>`, `<footer>`) to help search engine crawlers contextualize the page sections.

### 2. Local SEO Optimization
* Implement advanced **JSON-LD Schema Markup** directly into the PHP template headers.
  * Target Schema type: `LocalBusiness` or `ArtSupplyStore`.
  * Properties to include: Geolocation coordinates, opening hours, exact physical address, telephone number, and official social media profile connections.
* Optimize for local search intent (e.g., "negozio belle arti", "colorificio near me", "colori per pittura").

### 3. Core Web Vitals & Speed Performance
Search engines heavily penalize slow websites. This refactor will target a **95+ performance score** on Google PageSpeed Insights:
* **LCP (Largest Contentful Paint):** Optimize above-the-fold content delivery; inline critical CSS and pre-load core brand fonts.
* **FID / INP (Interaction to Next Paint):** Write non-blocking, asynchronous modern JavaScript to keep input latency under 50ms.
* **CLS (Cumulative Layout Shift):** Ensure every image and dynamic container has explicit height and width attributes reserved in the CSS to prevent layout jumping during render.

---

## On-Page content Strategy
* **URL Structuring:** Migrate from messy, query-string URLs to human-readable, keyword-rich slug patterns (e.g., `/prodotti/colori-olio/` instead of `/?p=412`).
* **Meta Management:** Create a dynamic PHP meta-tag builder that automatically populates optimized `<title>` and `<meta description>` strings based on the active page or product category, respecting strict character limits (under 60 characters for titles, under 160 for descriptions).