# Source Control

Git is the version control system implemented within the organisation. Where necessary, GitFlow has also been implemented to organise branches.

Where GitFlow has been implemented, the following rules need to be followed:

* All feature branches should be created from the `develop` branch. In case of module repositories (plugins, core) the `master` branch should be used as the base branch for features.
* All hotfix branches must always be created from the `master` branch.
* All hotfixes for library repositories (any modules or plugins) should be created from the latest live tag used in production. Please talk to the Release Manager to see if there is a branch that could be used instead.
* Fixes to code in a release candidate branch (aka.: `uat/version_number` branch, eg: `uat/2.2.0`) should be created from the corresponding release candidate branch and the PR with the fix needs to be merged back to the release candidate branch.

## Choosing the correct repository for your changes
It is essential that coded solutions are placed within the appropriate Git repositories.

## Branch naming conventions
The following convention must be used when creating new branches.


```
hotfix/{jira issue key}_{description lowercase, spaces replaced by _ or -}

feature/{jira issue key}_{description lowercase, spaces replaced by _ or -}
```
E.g.

```
hotfix/OPW-111_fixed_checkout_issue

feature/OPW-888_deploy_book_live
```

###Valid branch prefixes

```
hotfix/  -  for production related fixes uses the master ratchet for PHPCS

feature/ -  for any new features etc. uses the develop ratchet for PHPCS

bugfix/  -  for develop/uat branch related fixes uses the develop ratchet by defaulf for PHPCS

uat/     -  for release candidate branches to be deployed to the test environment uses the uat ratchet for PHPCS will automatically update the ratchet in case there is an improvement.

release/ -  for a concreate release branch to be merged and deployed to production uses the uat ratchet for PHPCS
```
Bug fixes for the release candidate branches should have uat somewhere in the name. For PHP solutions, this will allow the pipelines to use the correct phpcs ratchets.

E.g. ```feature/JP-9875_fixed_uat_bug```
#### Commit messages
Each commit message must include the ticket reference the change is related to and a short description of the change. This helps months later in identifying which ticket introduced the change. (Squashed commits should also have the ticket reference in the commit message when merging PRs.)

Eg.: ```JP-12345: short description of change.```

### Pull requests (PR’s)
Pull Requests are necessary for moving coded solutions between branches. All code that is to be deployed to a production environment MUST be code reviewed and approved before it can be merged (e.g. into the develop or master branches).

The following needs to be followed when working with PR’s:

1. Always select squash as the merge type when merging PRs.
2. For features going into the develop branch the PR can be merged when it has the necessary approvals.
3. Merging of hotfixes is performed by the Release Manager at the time of deployment. Please DO NOT merge hotfix PRs into the master branches.

We follow semver, please use the guidelines laid out there (Semantic Versioning 2.0.0 ) for choosing the appropriate version number for library repositories. If in doubt please contact one of the tech leads to help out in choosing the correct one.

### Code review feedback
Feedback on proposed solutions is very important. It helps in making sure that the final solution getting into the mainline works as expected and potential problems and issues are avoided. Feedback can also be very opinionated and discussions can drag on for a long time. To alleviate this we implemented the MoSCoW prioritisation system for feedback.

Name | Value
--- | ---
***Mo*** Must have | Describes a requirement that must be satisfied in the final solution.<br> Start the PR comment with ```Must:```
***S*** Should have | Represents a high priority requirement that should be included in the final solution if possible<br>Start the PR comment with ```Should:```
***Co*** Could have | Describes a requirement that is desirable, but not necessary<br>Start the PR comment with ```Could:```
***W*** Won’t have (this time) | Describes a requirement that will not be implemented in the current solution, but may be considered for a future ticket<br>Can be left off from a PR and discussed separately or start the PR comment with ```Won’t:```

### Working with big features
Working on big changes like payment provider integration, major refactoring, game provider integration etc should be done with an integration branch created from the develop branch. All your small feature branches should be PR'ed to this integration branch.
This allows releases to continue without partial solutions holding anything up. It also allows QA to spend as much time as needed to test the integration in isolation on a separate environment.

### Composer and dependency management
Only update specific packages. Blanket composer updates should never be performed and the PR will be declined.
