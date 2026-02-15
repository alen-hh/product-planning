---
name: skill-testing
description: Test and evaluate skill projects during development. Use when the user wants to test, evaluate, or assess a skill that is currently being developed in the workspace — i.e., the skill project in the current directory or a specified skill folder. This skill generates test cases, executes them against the target skill, and produces an evaluation report with strengths, weaknesses, and optimization suggestions. Triggers on requests like "test this skill", "evaluate my skill", "run skill tests", "assess skill quality", or "check if my skill works".
---

# Skills Testing

Evaluate a skill project's effectiveness by generating test cases, executing them, and producing an expert assessment report.

## Workflow

Testing a skill project involves these steps:

1. Discover the target skill project
2. Deep-read and understand the skill
3. Generate test cases
4. Execute each test case against the skill
5. Evaluate results and produce report

## Step 1: Discover the Target Skill Project

Locate the skill being tested. The target is the **current project (workspace)**, not a skill already in the skill list.

- Look for `SKILL.md` in the workspace root or common skill locations (`.cursor/skills/*/`, `.agents/skills/*/`, `skills/*/`).
- If multiple skill projects exist, ask the user which one to test.
- If no `SKILL.md` is found, inform the user and stop.

**Critical**: The skill under test is the one being **developed** in the workspace, not one from the installed skill list.

## Step 2: Deep-Read and Understand the Skill

Read all key files of the target skill project:

1. **SKILL.md** — Parse frontmatter (`name`, `description`) and body (instructions, workflow, examples).
2. **references/** — Read all reference docs to understand domain knowledge and supplementary guidance.
3. **scripts/** — Read all scripts to understand automation and tooling capabilities.
4. **assets/** — List asset files (do not read binary files) to understand templates and resources.

Build a mental model of:
- What the skill does (purpose and scope)
- When it triggers (description triggers)
- How it works (workflow, instructions, decision points)
- What resources it uses (scripts, references, assets)
- What output it produces

## Step 3: Generate Test Cases

Generate **2-3 test cases** from different perspectives. Each test case must include:

- **Name**: Short descriptive title
- **Scenario**: What the user is trying to accomplish
- **Input**: Concrete user message or request that should trigger the skill
- **Expected Behavior**: What the skill should do (steps, resources used, output)

### Test Case Selection Strategy

Choose test cases that cover different dimensions:

1. **Happy path** — A straightforward use case that matches the skill's primary purpose. Tests whether core functionality works correctly.
2. **Edge case / variation** — A less common but valid use case. Tests the skill's flexibility and handling of variations.
3. **Boundary / stress** — A request at the boundary of the skill's scope, or one requiring multiple features together. Tests robustness and completeness.

### Using Project Test Cases

Check for user-provided test case files:

1. If the user specifies files to use as test cases, use those.
2. Otherwise, look for a `/test-case` or `/test-cases` directory in the project root.
3. If test case files are found, read them and incorporate their content into the generated test cases.
4. If no test case files exist, generate all test cases from the skill understanding built in Step 2.

### Web Search for Test Cases (when applicable)

If the skill involves a specific domain, library, or technology where real-world context would improve test quality:

- Use available web search tools (tavily, brave, linkup.so, exa, serpapi, etc.) to find realistic scenarios.
- Use available URL fetch tools (fetch, tavily, jina reader, etc.) to retrieve relevant page content.
- Only do this when it meaningfully improves test case realism.

## Step 4: Execute Test Cases

For each test case, simulate the skill execution:

1. **Pretend to be a user** sending the test case's input message.
2. **Follow the skill's instructions** exactly as another Claude instance would — read the SKILL.md, follow the workflow, use referenced scripts/resources.
3. **Execute any scripts** referenced in the skill using the shell. Capture output and errors.
4. **Produce the output** the skill would generate for the user.
5. **Record** the full execution trace: which files were read, which scripts were run, what decisions were made, and the final output.

**Important**: Execute the skill faithfully. Do not shortcut or skip steps. The goal is to see how the skill actually performs, not how it ideally should perform.

## Step 5: Evaluate and Report

Read `references/evaluation-criteria.md` for the evaluation rubric and report template.

Evaluate each test case execution against the 7 criteria:

1. Triggering & Description Quality
2. Instruction Clarity & Completeness
3. Degree-of-Freedom Calibration
4. Resource Organization
5. Script Quality (if applicable)
6. Output Quality
7. Error Handling & Edge Cases

### Output: `/test-report` Folder

Create a `test-report/` folder in the project root with all test artifacts:

```
test-report/
├── TEST-REPORT.md          # Main evaluation report
├── test-case-1.md          # Test case 1 definition + execution result
├── test-case-2.md          # Test case 2 definition + execution result
└── test-case-3.md          # Test case 3 definition + execution result (if applicable)
```

#### Strict Output Rules

> **MANDATORY**: The `test-report/` folder and its `.md` files are the **sole deliverables** of this skill. You MUST follow these rules exactly:
>
> 1. **Only create the `test-report/` folder** — do NOT create any other folders (e.g., no `output/`, `results/`, `reports/`, `logs/`, `tmp/`, etc.).
> 2. **Only create `.md` files** inside `test-report/` — do NOT create any other file types (no `.json`, `.html`, `.txt`, `.csv`, `.yaml`, `.log`, or any other format).
> 3. **Only create the files listed above** — `TEST-REPORT.md` and `test-case-N.md` files. Do NOT create extra files like `summary.md`, `index.md`, `raw-data.md`, or anything beyond the specified structure.
> 4. **Do NOT modify any existing project files** — this skill is read-only with respect to the skill project under test. The only writes allowed are creating the `test-report/` folder and its `.md` files.
> 5. **Do NOT create scripts, configs, or helper files** — no shell scripts, no temporary files, no intermediate artifacts. All analysis and evaluation must be written directly into the markdown reports.
> 6. **If the `test-report/` folder already exists**, overwrite its contents rather than creating a differently named folder.

#### Test case files (`test-case-N.md`)

Each test case file must contain:

```markdown
# Test Case N: [Name]

## Definition
- **Scenario**: [description]
- **Input**: [user message]
- **Expected Behavior**: [what should happen]

## Execution Trace
[Which files were read, scripts run, decisions made — step by step]

## Output
[The actual output the skill produced]
```

#### Main report (`TEST-REPORT.md`)

Follow the template in `references/evaluation-criteria.md`. The report **must** include:

- Per-test-case results with ratings (referencing the individual test case files)
- Evaluation summary table
- **Strengths** — what the skill does well
- **Weaknesses** — where it falls short
- **Characteristics** — notable traits or patterns observed
- **Optimization Suggestions** — concrete, actionable improvements ranked by priority

## References

- **Evaluation rubric and report template**: See [references/evaluation-criteria.md](references/evaluation-criteria.md)
