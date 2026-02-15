# Web Research Tools & Methods

When product planning requires external information — market data, competitor intelligence, industry trends, pricing benchmarks, or user sentiment — use the web research tools described below.

---

## When to Use Web Research

Use web research during these product planning stages:

| Planning Stage | What to Research | Example Queries |
|----------------|------------------|-----------------|
| **Market Opportunity** | Market size, growth rates, industry reports | "global meal-kit delivery market size 2025" |
| **Competitive Analysis** | Competitor features, pricing, positioning | "[competitor name] pricing plans features" |
| **Trend Validation** | Emerging trends, technology shifts | "AI-powered fitness app trends" |
| **User Research** | User complaints, reviews, forum discussions | "[competitor] user reviews pain points reddit" |
| **Pricing Strategy** | Comparable product pricing, willingness to pay | "SaaS project management tool pricing comparison" |
| **Go-to-Market** | Distribution channels, marketing strategies | "[industry] customer acquisition channels" |
| **Regulatory / Compliance** | Legal considerations, data privacy rules | "[industry] regulatory requirements [region]" |

---

## Web Search Tools

Use web search tools to find information across the internet. Pick the tool available in your environment.

### Recommended Tools

| Tool | Best For | How It Works |
|------|----------|--------------|
| **Tavily** | Deep research, comprehensive results | MCP server or API; returns relevant search results with extracted content, supports `search` and `extract` |
| **Brave Search** | General web search, privacy-respecting | MCP server or API; returns web results, news, and discussions |
| **Exa** | Semantic search, finding similar content | MCP server or API; uses meaning-based search (not just keywords), great for finding competitor products and similar tools |
| **SerpAPI** | Google results, structured data (SERP features) | API-based; returns Google search results including featured snippets, "People Also Ask", and knowledge panels |
| **Linkup.so** | Real-time web search with source links | MCP server or API; returns sourced results with direct links for citation |

### Search Strategy

1. **Start broad, then narrow** — Begin with a general query to understand the landscape, then refine with specific terms.
2. **Use multiple queries** — Don't rely on a single search. Cross-reference findings from different angles:
   - Market size query + competitor landscape query + user sentiment query
3. **Verify with multiple sources** — Cross-check data points (e.g., market size) from at least 2 sources before including them in the report.
4. **Search with time context** — Append the current year or "latest" to queries when recency matters (e.g., market data, funding rounds).
5. **Use domain-specific searches** — Target specific sites when useful:
   - `site:reddit.com [topic]` for user sentiment
   - `site:g2.com [product]` for software reviews
   - `site:crunchbase.com [company]` for funding data

### Example Workflow

```
Step 1: Search "meal kit delivery market size 2025"
        → Extract TAM/SAM/SOM estimates

Step 2: Search "top meal kit delivery services comparison"
        → Identify direct competitors and their positioning

Step 3: Search "meal kit subscription complaints reddit"
        → Discover unmet needs and pain points

Step 4: Scrape competitor websites for pricing and feature details
        → Build competitive comparison matrix
```

---

## Webpage Scraping / Content Extraction

When you need to read the full content of a specific webpage (e.g., a competitor's pricing page, a blog post, a product listing), use content extraction tools.

### Recommended Tools

| Tool | Best For | How It Works |
|------|----------|--------------|
| **Tavily Extract** | Extracting clean content from URLs | Part of Tavily's API; pass a URL and get structured content back |
| **Jina Reader** | Reading any webpage as clean markdown | Prefix any URL with `https://r.jina.ai/` to get a clean, readable version; also available as MCP server |
| **Fetch (built-in)** | Quick page retrieval | Use the built-in `WebFetch` tool to retrieve and read webpage content in markdown format |
| **Firecrawl** | Crawling multiple pages from a domain | MCP server; can crawl an entire site or specific pages, returns structured markdown |
| **Browserbase / Browser-use** | Dynamic pages requiring JavaScript rendering | For SPAs or pages behind client-side rendering that simple fetch cannot handle |

### When to Use Scraping

- **Competitor pricing pages** — Extract current pricing tiers, feature comparisons
- **Product feature pages** — Understand what competitors highlight and how they position
- **Blog posts / Articles** — Read industry analysis, thought leadership, market reports
- **Review aggregators** — Extract user reviews and ratings from G2, Capterra, Product Hunt
- **Job postings** — Analyze competitor hiring patterns to infer product direction
- **Landing pages** — Study messaging, value propositions, and target audience language

### Content Extraction Strategy

1. **Prefer structured extraction** — Use Tavily Extract or Jina Reader for clean, structured content rather than raw HTML.
2. **Handle dynamic content** — If a page loads content via JavaScript (SPAs, infinite scroll), use a browser-based tool (Browserbase, Browser-use).
3. **Respect rate limits** — Don't send excessive requests to a single domain. Space out requests when scraping multiple pages.
4. **Extract what you need** — Focus on extracting specific data points (pricing, features, reviews) rather than entire page contents.
5. **Fallback chain** — If one tool fails to extract content, try the next:
   ```
   Jina Reader → Tavily Extract → Fetch (built-in) → Browser-use
   ```

---

## Integrating Research Into the Product Plan

After gathering external data, incorporate findings into the product planning report:

| Research Output | Goes Into Report Section |
|-----------------|------------------------|
| Market size data | Strategic Planning → Market Opportunity |
| Competitor features & pricing | Strategic Planning → Competitive Landscape |
| User pain points from reviews | Product Concept → Core Problem |
| Industry trends | Strategic Planning → Timing ("Why now?") |
| Comparable pricing models | Strategic Planning → Business Model |
| Distribution channel insights | Strategic Planning → Go-to-Market Strategy |
| Regulatory findings | Risks & Mitigation |

### Citation Practice

When including external data in the report, note the source:
- *"The global meal-kit market is projected to reach $XX billion by 2027 (Source: [Report Name])"*
- This adds credibility and allows the user to verify or dive deeper.

---

## Tool Setup Notes

Most web research tools are available as **MCP servers** that can be added to Cursor's configuration. To enable them:

1. **Tavily** — Add the Tavily MCP server with an API key from [tavily.com](https://tavily.com)
2. **Brave Search** — Add the Brave Search MCP server with an API key from [brave.com/search/api](https://brave.com/search/api)
3. **Exa** — Add the Exa MCP server with an API key from [exa.ai](https://exa.ai)
4. **Jina Reader** — No API key required for basic usage; prefix URLs with `https://r.jina.ai/`
5. **Firecrawl** — Add the Firecrawl MCP server with an API key from [firecrawl.dev](https://firecrawl.dev)
6. **Linkup.so** — Add the Linkup MCP server with an API key from [linkup.so](https://linkup.so)

If no external MCP search tools are available, fall back to the built-in `WebSearch` and `WebFetch` tools provided by the environment.
