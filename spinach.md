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
