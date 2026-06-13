# Contribution 1: [React Doctor] mouse-events-have-key-events: onMouseOver must be accompanied by onFocus for accessibility (2 occurrences)
 #27902

**Contribution Number:** 1
**Student:** Richard Gabelman 
**Issue:** [\[GitHub issue link\] ](https://github.com/wso2/product-is/issues/27902) 
**Status:** Phase 2 Complete

---

## Why I Chose This Issue

I was looking through the provided list of issues with tech stacks I have experience in. I found this project which uses two technologies I'm very familiar with (JS and CSS), and a technology that I was familiar with a long time ago where I could use a refresher.

The issue was in a cluster of issues from the same repository. Most of these other issues had many times more occurrences of the specified issue. This one only has two occurrences (and really after looking into it, really could be considered just one occurence). That seems managable and completable in the time alotted. 

---

## Understanding the Issue

### Problem Description

A React component contains a div with the onMouseOver and onMouseOut props that toggle the active state. React Doctor is a tool which detects anti-patterns in React apps. One of the uses seems to be identifying accessibility issues like this where a mouse is assumed when that is not necessarily a tool a user has the ability of using. Thus, we need to add the corresponding keyboard versions of onMouseOver and onMouseOut so the functionality is identical when using the component with a keyboard.

### Expected Behavior

Mousing on and off the div should result in the same behavior (the toggling of the active state) as focusing and unfocusing the div using a keyboard.

### Current Behavior

Focusing and unfocusing the div using a keyboard never toggles the active state. 

### Affected Components

This impacts the `validation-error-boundary.tsx` component which is located at `admin.flow-builder-core.v1/components/validation-panel/validation-error-boundary.tsx`.

---

## Reproduction Process

### Environment Setup

Used the project's `Setting Up Development Environment` and `Build & Run` guides.

React Doctor is the tool used to identify the issue. It is not provided in the project.

### Steps to Reproduce

1. Install React Doctor's CLI
2. Run React Doctor on the file in question
3. Observe the warning on Lines 114-115 of `admin.flow-builder-core.v1/components/validation-panel/validation-error-boundary.tsx`

### Reproduction Evidence

Running React Doctor against the package reveals the accessibility warning:

```
$ pnpm dlx react-doctor --lint --verbose features/admin.flow-builder-core.v1 2>&1 | grep -A 5 "mouse"
```

```
⚠ Accessibility: mouse-events-have-key-events
  Keyboard users miss this `onMouseOver` because it only fires with a mouse,
  so add an `onFocus` handler too.
  → Pair mouse events with keyboard ones so keyboard users are not left out.

  components/validation-panel/validation-error-boundary.tsx:114-115
```

- **My findings:** React Doctor isn't included in the devDependencies of the project. Some external entity ran React Doctor and generated the various GitHub issues based off of the resulting warnings/errors.

---

## Solution Approach

### Analysis

A React component has functionality associated with the mouseOver and mouseOff events. The same functionality should exist for users of the component who are interacting with it via a keyboard. This involves doing the same thing for the keyboard interactions.

### Proposed Solution

Add the current mouseOver and mouseOff functionality to additional props for onFocus and onBlur.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** Mouse events should have key events.

**Match:** N/A

**Plan:** 
1. Add onFocus and onBlur props to the div in the file
2. Copy the onMouseOver and onMouseOff functionality to these new props

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
