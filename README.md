# Contribution 2: Update browserlist


**Contribution Number:** 2 
**Student:** Richard Gabelman 
**Issue:** [\[GitHub issue link\]](https://github.com/HHS/simpler-grants-gov/issues/5289)
**Status:** Phase 2 Complete

---

## Why I Chose This Issue

  After getting familiar with the entire contribution progress from my first contribution, I wanted my second contribution to be more closely tied to a field (or mission) that I am passionate about.
  I selected this issue as a good entry point into further contributions within this repository (the Department of Health and Human Services). I can learn their process and make connections with the current maintainers that I can leverage when I make more substantial contributions in the future.
  The issue is a simple dependency-related update that will involve reproduction (and thus required building of the project), investigation into existing dependency-update mechanisms, and the opportunity to provide guidance on making sure the warning doesn't reoccur in the future.

---

## Understanding the Issue

### Problem Description

According to the issue description, when building the frontend application, a warning appears indicating that some data is old and that a command needs to be run to update the data. 

### Expected Behavior

Building the frontend should surface no warning indicating that the browsers data is old.

### Current Behavior

I have tried to replicate the issue by building the frontend myself. I followed the instructions in their Development.md for building the frontend locally. I was successful in getting the frontend to build but did not see the warning described in the issue.

### Affected Components

The frontend application which is a specific directory in their monorepo. This impacts the build process specifically.

---

## Reproduction Process

### Environment Setup

I made sure my node version matched the node version as specified in the Development.md which required moving to an older version.

### Steps to Reproduce

1. Clone repo
2. Go to the frontend directory of the monorepo
3. ```npm install```
4. ```npm run local```

### Reproduction Evidence

- **Commit showing reproduction:** It's not something that can be reproduced in a commit, it's a warning surfaced in the build process. Here is my branch in the forked repo: 
https://github.com/RichardGabelman/simpler-grants-gov/tree/RichardGabelman/5289-update-browserlist
- **Screenshots/logs:**
```
apollo@DESKTOP-I5JVOAJ:~/repos/simpler-grants-gov/frontend$ npm run local
npm warn Unknown user config "min-release-age". This will stop working in the next major version of npm.

> frontend@0.1.0 local
> ENVIRONMENT=local NEW_RELIC_ENABLED=false next dev

▲ Next.js 16.2.6 (Turbopack)
- Local:         http://localhost:3000
- Network:       http://10.255.255.254:3000
- Environments: .env.development
✓ Ready in 295ms
⚠ `eslint` configuration in next.config.js is no longer supported. See more info here: https://nextjs.org/docs/app/api-reference/cli/next#next-lint-options
⚠ Invalid next.config.js options detected:
⚠     Unrecognized key(s) in object: 'api', 'eslint'
⚠ See more info here: https://nextjs.org/docs/messages/invalid-next-config
- Experiments (use with caution):
  · proxyClientMaxBodySize: "2000mb"
  · serverActions
  ✓ testProxy


```
- **My findings:** The warning identified in the Issue Description did not appear. I have since commented on the issue description inquiring if the warning was still appearing for others. I also inquired as to whether this may be an intermittent issue that could be fixed with a recurring script.

---

## Solution Approach

### Analysis

I cannot reproduce the issue so I am not sure at this point. My belief is that this may be something that occurs when the ```package-lock.json``` goes awhile without being regenerated.

is incidentally fixed along other updates and perhaps a dedicated update to this data should be implemented on a recurring basis.

### Proposed Solution

The project already has a Renovate script which handles the automatic updating of dependencies. There is a mechanism within Renovate called ```lockFileMaintenance``` in which the ```package-lock.json``` could be periodically refreshed and thus reset the timer on which the warning would appear.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** Data used by a dependency will throw a warning when the data hasn't been updated in a certain amount of time.

**Match:** The codebase uses Renovate to automatically update project dependencies.

**Plan:**
1. Add the ```lockFileMaintenance``` feature to their existing Renovate setup to periodically refresh the lockfile, which would refresh the data used by the dependency.

**Implement:** https://github.com/RichardGabelman/simpler-grants-gov/tree/RichardGabelman/5289-update-browserlist

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
- [x] Branch name follows given convention
- [x] Pull Request will follow given convention
- [x] Will assign reviewers applicable to the domain of the pr
- [x] Will squash merge

**Evaluate:** I will reinstall and rebuild the frontend and ensure no errors on rebuild.

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



---
---
---
---
---

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
