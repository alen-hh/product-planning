# Skill Test Report: product-planning

## Summary
The product-planning skill is a well-structured, research-driven skill that successfully transforms product ideas into comprehensive planning reports. It excels at the happy path — clear ideas produce high-quality, research-backed reports with actionable insights. However, it shows weaknesses in handling vague inputs (underspecified clarification workflow) and overly rigid output templates that don't adapt to the complexity or domain of the product idea (e.g., regulated industries need more risk coverage).

## Test Cases Executed

### Test Case 1: Happy Path — Clear Product Idea
- **Scenario**: User presents a well-defined personal finance app idea for college students with clear target audience and features.
- **Input**: "I have an idea for a personal finance app designed specifically for college students. It would help them track spending, split bills with roommates, and build credit history while still in school."
- **Expected Behavior**: Minimal clarifying questions → web research → framework analysis → complete product planning report.
- **Actual Result**: The skill executed flawlessly. The trigger matched immediately ("I have an idea for..."). The agent correctly determined the idea was clear enough to skip clarifying questions. Web research was performed following `references/web-research.md` guidance (3 targeted searches covering market size, competitors, and user pain points). Frameworks from `references/frameworks.md` were applied (JTBD, Lean Canvas, Competitive Analysis, MoSCoW). The output report followed the template exactly and was populated with real research data, including market size figures, competitor names, and actionable next steps. (See `test-case-1.md` for full execution trace and output.)
- **Rating**: **Strong**
- **Notes**: This is the skill's sweet spot. The workflow was clear, the research integration was smooth, and the output was professional and comprehensive.

### Test Case 2: Edge Case — Vague/Underspecified Idea
- **Scenario**: User provides an extremely vague product idea ("for remote teams") with no specific problem, features, or differentiator.
- **Input**: "help me plan a product for remote teams"
- **Expected Behavior**: Skill should ask clarifying questions, then proceed after receiving answers.
- **Actual Result**: The skill correctly triggered ("help me plan a product" matched) and correctly identified the idea as vague. The agent paused to ask clarifying questions per Step 1. **However**, the skill provided zero guidance on what clarifying questions to ask, how many, in what format, or what dimensions to cover. The agent had to entirely improvise 4 questions (problem space, target user, pain point, integration model). Different Claude instances would likely ask very different questions, leading to inconsistent user experiences. There is also no guidance for handling a second round of clarification if the user's response is still vague. (See `test-case-2.md` for full execution trace.)
- **Rating**: **Adequate**
- **Notes**: The skill correctly identifies the need for clarification but provides no structure for executing it. This is a significant degree-of-freedom gap — the skill is under-constrained in exactly the area where consistency matters most (the first interaction with the user).

### Test Case 3: Boundary/Stress — Complex Regulated Industry Product
- **Scenario**: User presents a multi-faceted product idea in healthcare (3 feature areas + HIPAA compliance requirement).
- **Input**: "I want to build an AI-powered platform that helps small medical clinics automate patient intake, manage electronic health records, and provide AI-assisted preliminary diagnosis suggestions. It needs to be HIPAA compliant."
- **Expected Behavior**: Extensive research covering healthcare IT market, competitors, HIPAA requirements, and AI healthcare trends. Comprehensive report with substantial risk coverage.
- **Actual Result**: The skill triggered correctly and the agent determined the idea was clear enough to proceed (not "vague"). Web research was performed covering AI healthcare market data, EHR competitors for small clinics, and HIPAA-compliant solutions. Frameworks were applied with extra attention to regulatory risk. The output report was comprehensive. **However**, several friction points emerged:
  1. The skill only tells the agent to ask questions if the idea is "vague" — but this idea, while clear, is **complex** and would have benefited from clarifying questions (e.g., medical specialty focus, technical team experience, existing systems). The skill conflates "vague" with "needs more context."
  2. The output template's Risks & Mitigation section is a simple 2-row table, which is grossly insufficient for a healthcare/regulated product. The agent had to expand it to 6 rows, going beyond the template.
  3. The Feature Roadmap doesn't account for regulatory phasing — the agent had to reorder features (pushing AI diagnostics to "Future Vision") based on FDA considerations, but the skill provides no guidance on regulatory-aware prioritization.
  4. The web research guide (`references/web-research.md`) includes "Regulatory / Compliance" as a research category in its table but the main SKILL.md workflow does not explicitly call out regulatory research as a step.
  (See `test-case-3.md` for full execution trace and output.)
- **Rating**: **Adequate**
- **Notes**: The skill produces a good output for complex products, but the rigid template and lack of domain-specific adaptation guidance means the agent must improvise significantly for regulated industries.

## Evaluation Summary

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Triggering & Description | **Strong** | Description covers primary triggers well ("I have an idea for...", "help me plan a product", etc.). Could miss less obvious phrasings like "brainstorm startup ideas" or "I need a business plan" but covers the core use cases comprehensively. |
| Instruction Clarity | **Adequate** | The 4-step workflow is clear and logical. Step 1 (clarification) is underspecified — no guidance on what/how to ask. Steps 2-3 benefit from excellent reference docs. Step 4 has a clear output template. The gap between "vague" and "complex" ideas is not addressed. |
| Degree-of-Freedom | **Adequate** | Output template is appropriately structured but somewhat rigid — doesn't adapt to domain complexity (a 2-row risk table works for a consumer app but not a healthcare platform). Clarification step is too loose (zero guidance). Research step is well-balanced (flexible but with clear strategies). |
| Resource Organization | **Strong** | Excellent progressive disclosure: SKILL.md is lean (~130 lines), frameworks and web research guidance are in separate reference files loaded on demand. No unnecessary inlining. The output template is in SKILL.md which is justified as it's the primary deliverable spec. |
| Script Quality | **N/A** | No scripts in this skill. |
| Output Quality | **Strong** | Reports produced are professional, comprehensive, research-backed, and actionable. The template ensures consistent structure across different product ideas. Market data, competitor analysis, and feature roadmaps are all high quality. |
| Error Handling | **Adequate** | Handles vague ideas (asks questions) but with no structured approach. Doesn't address: web search returning no results, product ideas outside scope (non-product requests), complex-but-clear ideas needing context, or what to do when research contradicts the user's assumptions. |

## Strengths
- **Excellent resource organization** — Progressive disclosure via separate reference files means the agent only loads frameworks and web research guidance when actually needed, reducing context window usage.
- **Research-driven output** — The explicit web research step, backed by a detailed `references/web-research.md` guide with tool recommendations, search strategies, and example workflows, produces genuinely data-backed reports rather than generic AI-generated content.
- **Comprehensive output template** — The structured report template ensures professional, consistent output that covers all essential product planning dimensions (concept, design, strategy, features, metrics, risks, next steps).
- **Strong trigger description** — The description field includes both what the skill does AND specific trigger phrases, making it likely to activate correctly in most product planning scenarios.
- **Framework depth** — `references/frameworks.md` provides a rich toolkit (JTBD, Lean Canvas, MoSCoW, RICE, Kano, Value Proposition Canvas, Competitive Analysis) that enables multi-dimensional product analysis.

## Weaknesses
- **Underspecified clarification workflow** — Step 1 says "Ask clarifying questions if the idea is vague" but provides no question templates, required dimensions to cover, example questions, or guidance on format. This creates high variance in the first user interaction.
- **No distinction between "vague" and "complex"** — The skill only handles two states: idea is clear (proceed) or vague (ask questions). Complex-but-clear ideas (like healthcare AI) that would benefit from additional context gathering have no explicit handling.
- **Rigid output template for varying complexity** — The Risks & Mitigation table (2 example rows) and flat Feature Roadmap structure don't adapt to domain complexity. Regulated industries, hardware products, or marketplace models all have different risk and feature phasing needs.
- **No fallback for failed web research** — If web search tools are unavailable or return poor results, the skill provides no guidance on how to proceed (use general knowledge? inform the user? skip the section?).
- **Regulatory considerations not in core workflow** — `references/web-research.md` mentions regulatory research in its table, but the main SKILL.md workflow doesn't call out compliance/regulatory analysis as a distinct step, making it easy to overlook for regulated products.

## Characteristics
- **Research-first philosophy** — The skill prioritizes external data gathering over pure AI generation, which is a strong differentiator. Most product planning skills would produce generic reports; this one pushes for real market data.
- **Tool-agnostic research guidance** — `references/web-research.md` lists multiple search and scraping tools (Tavily, Brave, Exa, Jina, Firecrawl) with fallback chains, making the skill functional across different MCP configurations.
- **Lean main file, rich references** — SKILL.md at ~130 lines is concise; the depth comes from reference files. This is a textbook example of progressive disclosure in skill design.
- **Framework-heavy analysis** — The skill leans heavily on established business/product frameworks (JTBD, Lean Canvas, etc.) which gives the analysis rigor but may feel formulaic for experienced product managers who want more creative/unconventional analysis.
- **Single-pass workflow** — The skill is designed as a one-shot flow (understand → research → analyze → generate) with no iteration loop. Once the report is generated, there's no guidance for refinement based on user feedback.

## Optimization Suggestions

1. **[High Priority] Add a clarification question template or minimum dimensions to cover.** Include a list of required dimensions to clarify when the idea is vague: (a) core problem, (b) target user, (c) desired solution type, (d) differentiator from existing solutions. Optionally provide 2-3 example questions per dimension. This would dramatically reduce variance in the first user interaction.

2. **[High Priority] Add a complexity assessment step between Understand and Research.** After understanding the idea, the agent should assess: Is this a simple consumer product, a B2B SaaS, a regulated industry product, or a hardware/marketplace model? This assessment should influence which frameworks are applied, how deep the risk analysis goes, and whether regulatory research is performed.

3. **[Medium Priority] Make the output template adaptive.** Add conditional sections or guidance like: "For regulated industries (healthcare, finance, education), expand the Risks & Mitigation section to cover regulatory, compliance, and liability concerns in detail." Similarly, for marketplace/platform products, add a "Network Effects & Chicken-and-Egg" section.

4. **[Medium Priority] Add a web research fallback path.** Include a brief note in the workflow: "If web search tools are unavailable or return insufficient results, proceed with general knowledge and clearly mark sections as 'based on general industry knowledge — verify with current market data.' Inform the user that web research tools were unavailable."

5. **[Low Priority] Add an iteration/refinement loop.** After the initial report is generated, provide guidance for incorporating user feedback: "If the user requests changes, identify which sections need updating and whether additional research is needed. Regenerate only the affected sections rather than the entire report."

6. **[Low Priority] Add explicit regulatory research as a conditional workflow step.** When the product idea involves healthcare, finance, education, or other regulated sectors, insert a dedicated research step for regulatory requirements between the general market research and the analysis step. Reference this in the web-research.md guide's existing "Regulatory / Compliance" row.
