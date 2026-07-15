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


