Empathic development process
============================

1. Be empathic to the goals of client

2. Be empathic to the needs of the project ( = usually equal to "the less the better")

3. Be empathic to the comfort of the other persons you work with

General flow
------------

- Task is usually taken from Trello (PM tool) or LightHouse (issue tracker) or Sentry (exception tracker).
- Code is commited via git to Github.
- When merged to master ( = accepted), code goes to continuous integration server (CircleCI) and if tests are ok, is deployed do staging server.

Task management
---------------

- Discussions around WHAT should be kept in one place (PM tool).
- Discussions around HOW should be discussed in code reviews in Github - review early, review often.
- When task comes from LightHouse, discussions should be avoided as client shouldn't see them.
- When task comes from Sentry, its good to hotfix directly to master.

Git
---

Before commiting, read something about "git rebase workflow" and "github pull request workflow", these flows we use.

1. Create topic branch per logical unit (LightHouse task, Trello task,...)
2. Branch should be in format of YOUR_INITIALS-short-description-of-task, eg. PJ-add-draft-of-development-docs
3. Commit message format we use is nicely describede in [angular contribution guide]( https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit). If not sure, take a look into history of code to see it in practical use, its not hard.
  - if commit is fixing a LightHouse issue, the commit message should include text LH-ISSUE_NUMBER, eg. LH-394
  - if commit is fixing a Sentry issue, the commit message should include text SN-ISSUE_NUMBER, eg. SN-44
  - if commit is for a Trello card, a link to that card would be fine

Github
------

1. Before you send code to Github, rebase against master
2. After you send code to Github, keep branch mergable by merging master in there (rebase-forcepush is allowed as well if you are the only person working in that branch)
3. When the task is about a visual improvement, attach a screenshot of the result
4. When the task is about a flow (= you need to click at least once), attach a video of result 

Spinach features
----------------

**What is BDD?**
- unit tests (TDD) describe and test code itself
- features (BDD) describe behavior and test if the app does what its supposed to do

**In general**

- It should be as much descriptive as possible.
- Its meant to be read by humans (computer only parses it).
- Its a documentation, not just a set of testing scenarios.

**Every scenario has**

- 5 steps at most
- "Given" section - a premise of what must be true before action could be performed, you can compare this to "setup" or "before" block in Minitest and Rspec respectively
- "When" (with possible following "And") section - moment where the tested flow should happen - usually consists of fill_in, click_link, etc - progression
- "Then" (with possible following "And") section - verification that action caused the right consequenses - acceptance

**As for login, lets just lazyload users:**

```
def user
  @user ||= begin
    u = create(:user)
    visit login_path
    fill ...
    page.assert_text 'logged in'
    u
  end
end
```


**Few examples:**

```
Scenario: User is notified about new comment
Given I enter administration
When I create question
And another user comments my question
Then I will see notification on homepage
```

```
Scenario: Admin can create tags
Given I enter administration
When I create a tag
Another user can use it
```

```
Scenario: Admin can edit tags
Given I enter tag administration
When I edit an existing tag
Another user can see it changed
```
