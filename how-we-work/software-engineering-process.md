
# Software engineering process
In the following section we will showcase some of the engineering/process practices that we follow when we work in small or large teams.

## Git Flow
We adopted [one flow](http://endoflineblog.com/oneflow-a-git-branching-model-and-workflow) as a standard approach on all projects (small or large). 

Together with this, we follow a couple of rules when working on projects:
* Never push on **master**. Always create a branch, even for tiny changes.
* Always create feature branches linked with tickets (JIRA, redmine, gitlab)
* Ticket naming should be standard and should contain the ticket number at the end or at the beginning of the name. Examples: `12345_update_dependencies`, `CP-12345`. Optionally, the name can include a few words about the ticket or can just be the project identifier.
* Commit messages should reference the ticket numbers, based on the PM tool used, so that the commits are reflected in the tickets. Ex: `refs #12345`.
* The person that opens the MR/PR is responsible for merging the code once he/she gets the approval from the reviewer/team.
* Always enforce CI pipelines (linter, tests, bundlesize, etc.) **before** merging the branch.
* Always delete old branches after they are merged.
* Make use of CI pipelines to automatically deploy any changes to `master` in a **QA environment**.
* Use a simple tag naming convention, ex: 1.0.0.

## CI/CD
Coming soon
