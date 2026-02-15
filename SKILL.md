---
name: product-planning
description: Inspires and guides product ideation by transforming ideas into structured product concepts with design, planning, features, and actionable reports. Use when the user shares a product idea, wants product planning help, asks to develop a product concept, or requests product feature brainstorming. Triggers on phrases like "I have an idea for...", "help me plan a product", "what features should this product have", or "create a product plan for".
---

# Product Planning

Transform product ideas into actionable plans with design concepts, strategic planning, and feature roadmaps.

## Workflow

When a user shares a product idea, follow these steps:

1. **Understand the Idea** - Ask clarifying questions if the idea is vague. Understand the core problem being solved.

2. **Research the Landscape** - Use web research tools (see `references/web-research.md`) to:
   - Search for existing competitors and alternatives
   - Gather market size and growth data
   - Read competitor websites for pricing, features, and positioning
   - Find user pain points from reviews, forums, and social media
   - Identify relevant industry trends and timing signals

3. **Analyze & Expand** - Use frameworks from `references/frameworks.md` combined with research findings to:
   - Identify target users and their pain points
   - Define the value proposition
   - Explore market positioning

4. **Generate Outputs** - Produce:
   - Product design concept
   - Strategic planning elements
   - Feature recommendations
   - Brief product planning report (backed by research data where available)

## Output Structure

Generate a product planning report following this structure:

```markdown
# Product Planning Report: [Product Name]

## Executive Summary
[2-3 sentences capturing the essence of the product opportunity]

## Product Concept

### Vision Statement
[One inspiring sentence about what this product will become]

### Target Users
- Primary: [User segment with specific characteristics]
- Secondary: [Additional user segments if applicable]

### Core Problem
[Clear articulation of the problem being solved]

### Value Proposition
[Unique value this product delivers]

## Product Design

### Key Design Principles
1. [Principle 1 - e.g., Simplicity first]
2. [Principle 2 - e.g., Privacy by design]
3. [Principle 3 - e.g., Delightful micro-interactions]

### User Experience Highlights
[2-3 key UX elements that differentiate the product]

## Strategic Planning

### Market Opportunity
- **Market size**: [TAM/SAM/SOM estimates if relevant]
- **Competitive landscape**: [Key competitors and differentiation]
- **Timing**: [Why now? Market trends supporting this]

### Business Model
[How the product makes money - subscription, freemium, marketplace, etc.]

### Go-to-Market Strategy
[Initial channels and growth approach]

## Feature Roadmap

### MVP Features (Must-Have)
1. [Feature 1] - [Brief description and user benefit]
2. [Feature 2] - [Brief description and user benefit]
3. [Feature 3] - [Brief description and user benefit]

### Phase 2 Features (Should-Have)
1. [Feature] - [Description]
2. [Feature] - [Description]

### Future Vision (Nice-to-Have)
1. [Feature] - [Description]
2. [Feature] - [Description]

## Success Metrics
- [Key metric 1]: [Target and rationale]
- [Key metric 2]: [Target and rationale]

## Risks & Mitigation
| Risk | Mitigation Strategy |
|------|---------------------|
| [Risk 1] | [How to address it] |
| [Risk 2] | [How to address it] |

## Next Steps
1. [Immediate action item]
2. [Immediate action item]
3. [Immediate action item]
```

## References

### Frameworks
For deeper analysis, consult `references/frameworks.md` which contains:
- Jobs-to-be-Done framework
- Lean Canvas methodology
- Feature prioritization methods
- User persona templates
- Competitive analysis frameworks

### Web Research
For external data gathering, consult `references/web-research.md` which covers:
- **When to research** — Which planning stages benefit from external data
- **Web search tools** — Tavily, Brave Search, Exa, SerpAPI, Linkup.so and search strategies
- **Webpage scraping** — Tavily Extract, Jina Reader, Fetch, Firecrawl, Browser-use for reading specific pages
- **Integration guidance** — How to map research findings into the product planning report
- **Tool setup** — How to configure MCP servers for each tool
