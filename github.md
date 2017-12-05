Git
---

Before commiting, read something about "git rebase workflow" and "github pull request workflow", these flows we use.

1. Create new branch

2. Branch name should be in format of YOUR_INITIALS-short-description-of-task, eg. PJ-add-draft-of-development-docs

3. Commit message format we use is nicely described in [angular contribution guide]( https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit). If not sure, take a look into history of code to see it in practical use, its not hard.
  - if commit is fixing a LightHouse issue, the commit message should include text LH-ISSUE_NUMBER, eg. LH-394
  - if commit is fixing a Sentry issue, the commit message should include text SN-ISSUE_NUMBER, eg. SN-44
  - if commit is for a Trello card, a link to that card would be fine

Github
------

1. Before you send code to Github, rebase against master

2. After you send code to Github, keep branch mergable by merging master in there (rebase-forcepush is allowed as well if you are the only person working in that branch)

3. When the task is about a visual improvement, attach a screenshot of the result

4. When the task is about a flow (= you need to click at least once), attach a video of result

5. In PR description ALWAYS mention Github Issue like https://help.github.com/articles/closing-issues-via-commit-messages/
