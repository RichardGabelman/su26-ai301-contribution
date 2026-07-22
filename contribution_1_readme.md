# Contribution 1: [React Doctor] mouse-events-have-key-events: onMouseOver must be accompanied by onFocus for accessibility (2 occurrences)
 #27902

**Contribution Number:** 1
**Student:** Richard Gabelman 
**Issue:** [\[GitHub issue link\] ](https://github.com/wso2/product-is/issues/27902) 
**Status:** Phase 4 Resubmission

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

**PR Description:** 
The validation error boundary component included only mouse-based event handlers which wouldn't occur when users interacted via keyboard. This PR adds the event handling code to the respective keyboard event handlers.
Fix issue #27902 react-doctor/mouse-events-have-key-events accessibility warning by pairing onMouseOver and onMouseOut handlers with their keyboard equivalents onFocus and onBlur in ValidationErrorBoundary.

(Regarding the screenshot rubric point, it is a frontend change, yes, but one that would be basically invisible in a screenshot. It is an accessibility fix.)

**Maintainer Feedback:**
- [June 14th, 2026]: (automated PR review) Keyboard accessibility additionals wouldn't work when the div in question could not be 'tabbed' to. Divs don't have a tab-index by default.
- [June 14th, 2026]: Added an additional commit to my PR that conditionally adds a tab index to the div, provided there was a notification.

**Status:** Awaiting review

---

## Learnings & Reflections

### Technical Skills Gained

I learned how to choose a correctly scoped issue.
I navigated a large monorepo to find the impacted component.
I downloaded and utilized the third party React component checker (React Doctor) to verify issue reproduction and to verify that the fix addressed the issue.
I learned the correct Git workflow for proposing changes to existing substantial repositories (fork -> branch -> pr).

### Challenges Overcome

The tool they used to surface the issue (React Doctor) was not provided as a tool within the project.
I had to find the tool, download it (via the project's dependency manager), and learn how to use it properly in order to surface the same warning (and thus reproduce), fix the issue, use it to confirm the fix worked, and then remove it cleanly so it wouldn't appear as an addition to my PR.

### What I'd Do Differently Next Time

I would include a @ to a maintainer with my PR, or at least add a follow up comment with one, as my PR has gone some time without any message.
I'd pick an issue that was in a project I used or at least in a domain I knew more about. I indexed too heavily on language/tool familiarity and scope.

---

## Resources Used

- Helpful docs:
    https://github.com/wso2/identity-apps#setup-development-environment
    https://github.com/wso2/identity-apps?tab=contributing-ov-file
    https://www.react.doctor/
