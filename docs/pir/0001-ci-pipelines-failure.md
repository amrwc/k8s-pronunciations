# Post-Incident Review 0001: CI Pipelines Failure

## Incident summary

[The pull request #6](https://github.com/amrwc/k8s-pronunciations/pull/6) introduced changes to the `README.md` file.
The continuous integration pipelines responsible for detecting the linting errors silently failed.
The failures became apparent after merging the pull request into trunk.

## Lead-up

1. An external pull request has been opened.
1. Additional commit has been pushed to the remote branch.

## Fault

The GitHub status checks were not displayed for individual commits.

## Impact

Absolutely none, because it’s a meme repository.

## Detection

The pipeline failures surfaced after the status checks turned red in trunk.

## Response

At 2137h, the maintainer of the repository opened [pull request #7](https://github.com/amrwc/k8s-pronunciations/pull/7) with relevant fixes, along with miscellaneous changes.

## Recovery

At 2153h, the pull request has been merged into trunk.
All the checks turned green afterwards.

## Timeline

On 2023-04-21 at 1707h GMT+2, [the pull request #6](https://github.com/amrwc/k8s-pronunciations/pull/6) was opened.

On 2023-04-24 at 1027h GMT+2, the PR has been _thoroughly_ reviewed by the maintainer.

On 2023-05-02 at 1605h GMT+2, the review has been responded to by the committer.

On 2023-05-02 at 1606h GMT+2, additional changes have been pushed to the remote branch.

On 2023-06-06 at 2129h GMT+2, the pull request has been approved by the maintainer, and merged into trunk immediately after.
Both pipelines failed just seconds later.

On 2023-06-06 at 2130h GMT+2, the maintainer noticed the failed status checks, and began investigation.

On 2023-06-06 at 2137h GMT+2, [the pull request #7](https://github.com/amrwc/k8s-pronunciations/pull/7) containing the fixes has been opened.

On 2023-06-06 at 2153h GMT+2, after _rigorous_ checks and review, the fixes have been merged into trunk.
The status checks turned green right after.

## Root cause identification – the 5 whys

1. The status checks failed because a line in `README.md` was too long.
1. The checks failed for this reason because their configuration required them to do so.
1. The tools were configured in such a way by default.
1. Overriding the defaults was not necessary when the tools have been initially set up.
1. It was not necessary because there were no lines in the `README.md` file longer than 80 characters.

## Root cause

A line in `README.md` was too long.

## Backlog check

There was no backlog for this repository.

## Recurrence

Not applicable.

## Lessons learned

- If the status checks don’t appear in pull requests, check [the Actions tab](https://github.com/amrwc/k8s-pronunciations/actions) of the repository.
- Don’t merge a pull request until all checks are green.

## Corrective actions

1. Fix the root cause – either wrap the line, or change the linting configuration.
1. Prevent merging until all status checks are green.

   This may be impossible when the actions don’t run at all for unrelated reasons.
