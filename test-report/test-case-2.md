# Test Case 2: Edge Case — Vague/Underspecified Idea

## Definition
- **Scenario**: A user provides a very vague product idea with no specific problem, features, or target audience details. The skill should first ask clarifying questions before proceeding with research and planning.
- **Input**: "help me plan a product for remote teams"
- **Expected Behavior**: The skill should (1) trigger on "help me plan a product", (2) recognize the idea is vague — "remote teams" could mean communication, project management, culture building, hiring, async collaboration, or many other domains, (3) ask clarifying questions per Step 1 of the workflow, (4) only after receiving clarification, proceed with research and analysis.

## Execution Trace

### Step 1: Read SKILL.md
- Read root `SKILL.md` — identified the 4-step workflow.
- The `description` field triggers match: "help me plan a product" is explicitly listed.

### Step 2: Understand the Idea
- Input: "help me plan a product for remote teams"
- **Decision**: The idea is vague. "Remote teams" is an extremely broad category. The skill instructs: "Ask clarifying questions if the idea is vague. Understand the core problem being solved."
- Must ask clarifying questions before proceeding.

### Step 3: Generate Clarifying Questions
The skill says to ask clarifying questions but does **not** specify:
- How many questions to ask
- What format to use (numbered list? one at a time?)
- Which aspects to prioritize clarifying
- Whether to offer options/suggestions or ask open-ended questions

**Decision made by the agent (inference required)**: Ask 3-4 focused questions covering the key unknowns — problem space, specific type of tool, target users, and differentiator.

Generated questions:
1. What specific challenge for remote teams are you trying to solve? (e.g., communication, project management, team culture, async collaboration, hiring, onboarding)
2. Who is your target user — team leads/managers, individual contributors, HR/People Ops, or the whole team?
3. Do you have a specific frustration with existing remote work tools that inspired this idea?
4. Are you thinking of a standalone tool or something that integrates with existing platforms (Slack, Zoom, Notion, etc.)?

### Step 4: Simulated User Response
Since this is a test simulation, no actual user response is available. The skill workflow **stops here** until clarification is received.

**However**, to test the full pipeline, I'll assume the user responds with:
> "I want to build an async video messaging tool for remote teams. The problem is that Slack messages get lost and Zoom meetings waste time. I want something in between — short video updates that team members can watch on their own time."

### Step 5: Research the Landscape (after clarification)
- Consulted `references/web-research.md` for research strategy.
- Would perform web searches for:
  1. "async video messaging tools remote teams market" → Competitors like Loom, Vimeo Record, Claap, Volley
  2. "Loom competitors async video communication 2025" → Market landscape
  3. "remote team communication pain points Slack fatigue" → User pain points

**Note**: Web research was not fully executed for this test case since the primary test is whether the skill handles vague input correctly.

### Step 6: Observations on Skill Behavior

**What went well:**
- The skill correctly identified that clarifying questions were needed.
- The trigger phrase "help me plan a product" matched the description.

**What was ambiguous/required inference:**
- The skill says "Ask clarifying questions if the idea is vague" but provides no guidance on:
  - **What constitutes "vague"** — no rubric or examples of vague vs. clear ideas
  - **What questions to ask** — no question templates or required dimensions to clarify
  - **How many questions** — could be 1 or 10
  - **Response format** — bullet list? conversational? structured form?
- The agent had to improvise the clarifying questions entirely, which means different Claude instances might ask very different questions, leading to inconsistent user experiences.
- There's no guidance on what to do if the user's clarification is still vague after the first round.

## Output

**Agent's response to the user (before clarification):**

---

Great, I'd love to help you plan a product for remote teams! Before I dive into research and planning, I have a few questions to make sure I understand your vision:

1. **What specific challenge for remote teams are you trying to solve?** For example: communication overload, project management, team culture/bonding, async collaboration, hiring/onboarding, or something else?

2. **Who is your target user?** Team leads and managers, individual contributors, HR/People Ops teams, or the entire team?

3. **Is there a specific frustration with existing remote work tools** (like Slack, Zoom, Notion, Asana) that inspired this idea?

4. **Are you envisioning a standalone product or something that integrates** with the tools remote teams already use?

Once I understand these aspects, I'll research the competitive landscape, analyze the market opportunity, and create a detailed product plan for you.

---

*Note: The full product planning report would be generated after receiving the user's clarification. The workflow correctly paused at Step 1 to gather more information.*
