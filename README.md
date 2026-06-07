# Contribution 1: Reporting/Bug: Fixtures for 2025 should not include "Apr-Dec production data" field

**Contribution Number:** 1
**Student:** Richard Gabelman 
**Issue:** [\[GitHub issue link\] ](https://github.com/bcgov/cas-registration/issues/4633) 
**Status:** Phase I Complete

---

## Why I Chose This Issue

I was looking through the provided list of issues with tech stacks I have experience in. I noticed the organization that controls the repository for this issue was listed as bcgov. Looking into it, that refers to the actual government of British Columbia, Canada. 

I thought it was interesting that a government would have open-source codebases where anybody (even a foreign national like me) could contribute. I have a passion for civic tech and have created projects myself that deal with the interface of technology and public policy. 

I hope to learn both the typical lessons of navigating and contributing to a large codebase while also learning any potential unique aspects of contributing code to government services.

---

## Understanding the Issue

### Problem Description

A generated supplementary report `Review Changes` erroneously indicates some data was deleted due to the presence of a field in a previous state that isn't included (as it isn't necessary) in the current state. This only impacts developers as the previous state in production will never include the field.

### Expected Behavior

`Review Changes` should only show actual changes. The field `Production Data for Apr 1 - Dec 31 2024` should not appear, and should not show as deleted.

### Current Behavior

`Review Changes` shows a field `Production Data for Apr 1 - Dec 31 2024` as having been deleted when that field isn't relevant.

### Affected Components

This impacts the Reporting Page. I already believe the issue to be within `/bc_ops/reporting/fixtures/mock/report_product.json`.

---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]

### Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
