Empathic development process
============================

1. Be empathic to the goals of client

2. Be empathic to the needs of the project ( = usually equal to "the less the better")

3. Be empathic to the comfort of the other persons you work with

General flow
------------

- Task is usually taken from Trello (PM tool) or LightHouse (issue tracker) or Sentry (exception tracker).
- When there doesn't exist a Github issue for it, you should create it and mention original task in the issue name like T-XX, LH-XX, S-XX where XX is ID in source system
- Code is commited via git to Github.
- When merged to master ( = accepted), code goes to continuous integration server (CircleCI) and if tests are ok, is deployed on staging server.

Good to know
---------------

- review early, review often
- when there is a critical bug, its fine to hotfix in master, but in all other cases we strictly go with Pull Requests
- please use english across all systems
