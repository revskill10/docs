Empathic development process

1) Be empathic to the goals of client.
2) Be empathic to the needs of the project (usually the less the better).
3) Be empathic to the comfort of the other persons you work with.

General flow
- task is taken from Trello (PM tool) or LightHouse (issue tracker) or Sentry (exception tracker)
- code is commited via git to Github
- when merged to master, code goes to continuous integration server (CircleCI) and if tests are ok, is deployed do staging server

Task management
- discussions around WHAT should be kept in one place, in PM tool
- discussions around HOW should be discussed in code reviews in Github - review early, review often
- when task comes from LightHouse, discussions should be avoided as client shouldn't see them
- when task comes from Sentry, its allowed to fix directly in master

Git:
- read something about "git rebase workflow" and "github pull request workflow" - these are what we use
- create topic branch per logical unit (LightHouse task, Trello task,...)
- branch should be in format of YOUR_INITIALS-short-description-of-task, eg. PJ-add-draft-of-development-docs
- commit message should be according to https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit (take a look into history of code to see it in practical use, its not hard)
- if commit is fixing a LightHouse issue, the commit message should include text LH-ISSUE_NUMBER, eg. LH-394
- if commit is fixing a Sentry issue, the commit message should include text SN-ISSUE_NUMBER, eg. SN-44
- if commit is for a Trello card, a link to that card would be fine

Github
- before you send code to Github, rebase against master
- after you send code to Github, keep branch mergable by merging master in there (rebase-forcepush is allowed as well if you are the only person working in that branch)
- when the task is about a visual improvement, attach a screenshot of the result
- when the task is about a flow (= you need to click at least once), attach a video of result 

