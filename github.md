Git
---

Before commiting, read something about "git rebase workflow" and "github pull request workflow", these flows we use.

1. Create new branch

2. Branch name should be in format of ISSUE-IDENTIFIER-short-description-of-task, eg. RM4242-add-draft-of-development-docs.
Each project can personalize the branch name to better suite that particular project (at the end of the standard name):

- Environment name
- Originating branch
- Developer initials

3. Commit message format we use is nicely described in [angular contribution guide](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commit-message-format).

- The commit message should start with a verb (try using one of these preferably:  add/remove/fix/update)
- Short description: WHAT the commit does
- Long description: The commit message should explain WHY the code is changed not how, as that should be apparent from the code itself

Github
------

1. Before you send code to Github, rebase against master

2. After you send code to Github, keep branch mergeable by rebasing against master (!!!rebase-forcepush is allowed as well if you are the only person working in that branch!!!)

3. When the task is about a visual improvement, attach a screenshot of the result

4. When the task is about a flow (= you need to click at least once), attach a video of result

5. In PR description ALWAYS mention Github Issue like https://help.github.com/articles/closing-issues-via-commit-messages/

Simplified template for PR
--------------------------

```
## Description
<!--- Describe your changes in detail if it is needed-->

## Related Issue
<!--- Example: Closes #123; or fix #432 and #567 -->
<!--- Docs: https://help.github.com/articles/closing-issues-via-commit-messages/ -->
<!--- OR write url to issue in other system, e.g. Redmine -->
Closes  #

## How Has This Been Tested?
- [ ] Unit tests
- [ ] Spinach feature
- [ ] Manually

## Screenshots or Screencast
```

Extended template for PR
------------------------
```
## Description
<!--- Describe your changes in detail -->

## Related Issue
<!--- This project only accepts pull requests related to open issues -->
<!--- If suggesting a new feature or change, please discuss it in an issue first -->
<!--- If fixing a bug, there should be an issue describing it with steps to reproduce -->
<!--- Example: Closes #123, closes #432 and #567 -->
<!--- Docs: https://help.github.com/articles/closing-issues-via-commit-messages/ -->
Closes  #

## How Has This Been Tested?
<!--- Please describe in detail how you tested your changes. -->
<!--- Include details of your testing environment, and the tests you ran to -->
<!--- See how your change affects other areas of the code, etc. -->
- [ ] Unit tests
- [ ] Spinach feature
- [ ] Manually on localhost
- [ ] Manually on Staging environment
- [ ] Manually on DEV / UAT environment (if applicable)

## Screenshots

<!--- Its very helpful to show the results of your frontend-facing work in a visual manner. -->
<!--- If this PR is adding a "flow" functionality, a video is handy as well.  -->

## Types of changes
<!--- What types of changes does your code introduce? Put an `x` in all the boxes that apply: -->
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to change)

## Checklist:
<!--- Go over all the following points, and put an `x` in all the boxes that apply. -->
<!--- If you're unsure about any of these, don't hesitate to ask. We're here to help! -->
- [ ] My change requires a change to the documentation so I updated it accordingly (README, etc).
- [ ] My change requires a change to the config files so I updated example config files accordingly.
- [ ] I have added unit tests to cover my changes.
- [ ] This change affects the way user uses UI, so I added Spinach feature to cover that.
- [ ] All new and existing tests passed.
- [ ] HoundCI is happy or exceptions has been approved.
- [ ] I have a code review from another team member.
```
