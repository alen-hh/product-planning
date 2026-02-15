# Skill Evaluation Criteria

Use this rubric when evaluating a skill's effectiveness after test case execution.

## 1. Triggering & Description Quality

| Rating | Criteria |
|--------|----------|
| Strong | `description` clearly states what the skill does AND when to use it; covers all intended trigger scenarios |
| Adequate | `description` covers most triggers but misses edge cases or is slightly vague |
| Weak | `description` is too generic, missing key triggers, or would cause false positives/negatives |

## 2. Instruction Clarity & Completeness

| Rating | Criteria |
|--------|----------|
| Strong | Instructions are unambiguous; Claude can execute without guessing; all steps covered |
| Adequate | Mostly clear but some steps require inference; minor ambiguity |
| Weak | Missing critical steps; confusing flow; Claude must improvise significantly |

## 3. Degree-of-Freedom Calibration

| Rating | Criteria |
|--------|----------|
| Strong | Constraints match task fragility — strict where needed, flexible where beneficial |
| Adequate | Mostly appropriate but some areas over- or under-constrained |
| Weak | Too rigid for variable tasks or too loose for fragile operations |

## 4. Resource Organization

| Rating | Criteria |
|--------|----------|
| Strong | Progressive disclosure used well; SKILL.md is lean; references loaded only when needed |
| Adequate | Reasonable structure but some content could be split out or better organized |
| Weak | SKILL.md is bloated; references missing or all content inlined; no progressive disclosure |

## 5. Script Quality (if applicable)

| Rating | Criteria |
|--------|----------|
| Strong | Scripts run correctly; handle edge cases; well-documented parameters |
| Adequate | Scripts work for common cases; minor edge case gaps |
| Weak | Scripts fail or produce incorrect results; missing error handling |

## 6. Output Quality

| Rating | Criteria |
|--------|----------|
| Strong | Output matches expected format and content; professional quality; addresses the test case fully |
| Adequate | Output is mostly correct but has minor gaps, formatting issues, or incomplete coverage |
| Weak | Output is wrong, incomplete, or doesn't address the test case |

## 7. Error Handling & Edge Cases

| Rating | Criteria |
|--------|----------|
| Strong | Skill handles unexpected input gracefully; provides helpful error messages or fallbacks |
| Adequate | Handles common errors but may struggle with unusual inputs |
| Weak | Fails silently or produces confusing results on edge cases |

## Test Report Template

```markdown
# Skill Test Report: [Skill Name]

## Summary
[1-2 sentence overall assessment]

## Test Cases Executed

### Test Case 1: [Name]
- **Scenario**: [Description]
- **Input**: [What was provided]
- **Expected Behavior**: [What should happen]
- **Actual Result**: [What happened]
- **Rating**: [Strong / Adequate / Weak]
- **Notes**: [Observations]

### Test Case 2: [Name]
[Same structure]

### Test Case 3: [Name]
[Same structure]

## Evaluation Summary

| Criterion | Rating | Notes |
|-----------|--------|-------|
| Triggering & Description | | |
| Instruction Clarity | | |
| Degree-of-Freedom | | |
| Resource Organization | | |
| Script Quality | | |
| Output Quality | | |
| Error Handling | | |

## Strengths
- [Key strength 1]
- [Key strength 2]

## Weaknesses
- [Key weakness 1]
- [Key weakness 2]

## Characteristics
- [Notable characteristic 1]
- [Notable characteristic 2]

## Optimization Suggestions
1. [Priority suggestion with rationale]
2. [Additional suggestion]
3. [Additional suggestion]
```
