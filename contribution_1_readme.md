# Contribution 1: [React Doctor] mouse-events-have-key-events: onMouseOver must be accompanied by onFocus for accessibility (2 occurrences)
 #27902

**Contribution Number:** 1
**Student:** Richard Gabelman 
**Issue:** [\[GitHub issue link\] ](https://github.com/wso2/product-is/issues/27902) 
**Status:** Phase 4 Complete

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

**Implement:** https://github.com/RichardGabelman/identity-apps/tree/fix/issue-27902-mouse-events-have-key-events

**Review:** Follows project contribution guidelines

**Evaluate:** I will run React Doctor on the related file and will confirm it works when no warning is produced.

---

## Testing Strategy

### Manual Testing

I installed React Doctor and will run it on the related file. A "clean" report indicating no warnings or errors will indicate the fix was successful.

---

## Implementation Notes

### Week 3 Progress

I made my first set of changes. I pushed my branch and opened a pull request on the main repository. I received an automated AI pull request review that indicated an additional change needed to occur for my original changes to work. I then added a new commit with those changes and updated my pull request. Currently awaiting human review.

### Week 4 Progress

Still awaiting human review on my pr. I've begun the process of looking for my next contribution opportunity.

### Code Changes

- **File modified:** 

```features/admin.flow-builder-core.v1/components/validation-panel/validation-error-boundary.tsx```
- **Key commits:**
[Original change](https://github.com/wso2/identity-apps/pull/10407/changes/6ee4ece1b80d7b3b2ea9d89b1b967c28b399589b) 
|
[Additional commit with changes satisfying automated pr review](https://github.com/wso2/identity-apps/pull/10407/changes/843f5c00aec0ecddb25e13f93fc3e6d33eb46772)
- **Approach decisions:** N/A

---

## Pull Request

**PR Link:** https://github.com/wso2/identity-apps/pull/10407

**PR Description:** They provided a PR template that I modified due to the brevity of the changes I made.

```
Purpose
Fix react-doctor/mouse-events-have-key-events accessibility warning by pairing onMouseOver and onMouseOut handlers with their keyboard equivalents onFocus and onBlur in ValidationErrorBoundary.

Related Issues
#27902
Related PRs
N/A
Checklist
 e2e cypress tests locally verified. (for internal contributers)
 Manually ran React Doctor and the warning no longer appears
 UX/UI review done on the final implementation.
 Documentation provided. (Add links if there are any)
 Relevant backend changes deployed and verified
 Unit tests provided. (Add links if there are any)
 Integration tests provided. (Add links if there are any)
Security checks
 Followed secure coding standards in http://wso2.com/technical-reports/wso2-secure-engineering-guidelines
 Ran FindSecurityBugs plugin and verified report
 Confirmed that this PR doesn't commit any keys, passwords, tokens, usernames, or other secrets
Developer Checklist (Mandatory)
 Complete the Developer Checklist in the related product-is issue to track any behavioral change or migration impact.
No behavioural change
No migration impact
No new configuration introduced
```

**Maintainer Feedback:**
- [June 14th, 2026]: (automated PR review) Keyboard accessibility additionals wouldn't work when the div in question could not be 'tabbed' to. Divs don't have a tab-index by default.
- [June 14th, 2026]: Added an additional commit to my PR that conditionally adds a tab index to the div, provided there was a notification.

**Status:** Awaiting review

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
