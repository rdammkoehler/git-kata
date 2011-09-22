The purpose of this project is to provide practice kata for git to help people learn good and effective habits for source control while using git.

* Reviewing A Change List
* Finding out who deleted a file
* Moving a file while preserving history
* Moving a file and then merging the move into another branch
* Finding Checkins related to a particular bug number
* Finding checkins by a particular person in a particular date range
* Reverting a change list
* Pushing some but not all commits
* How to force a checkout to a branch that has all kinds of wacky changes but no local content

# Basic kata

## Creating feature branch and pushing

    git pull --rebase # ensure we are up-to-date
    git checkout -b pants # create a feature branch called "pants"
    echo some > left-leg
    echo more > right-leg
    git add left-leg
    git add right-leg
    git commit -mv 'I added legs'
    git push origin pants

## Finding out who deleted a file

    $ git log -n 1 -- README
    commit 4a7f8ae2993278fa710a8f286ff92a636c6950d7
    Author: magnus stahre <ms@xy.org>
    Date:   Wed Aug 31 20:29:23 2011 -0400
    
        Rename README to README.md.

Hence, `README` was removed (actually renamed) in commit *4a7f8ae2993278fa710a8f286ff92a636c6950d7*.

## Finding commits based on commit message

This finds all commits related to issue [SPR-8570](https://jira.springsource.org/browse/SPR-8570) in spring-framework:

    $ git log --oneline --grep SPR-8570
    7c1c497 Fix typo in SmartLifecycle Javadoc
    8760c83 Clarify Lifecycle#stop documentation
    e7cb561 Document Lifecycle#stop concurrency semantics

Since this repository was actually cloned from svn, we can also find the corresponding svn commits:

    $ git svn log --oneline --grep SPR-8570
    r4836 | Fix typo in SmartLifecycle Javadoc
    r4831 | Clarify Lifecycle#stop documentation
    r4822 | Document Lifecycle#stop concurrency semantics

## Create a log of the work you did over the past week
    $ git log --author me --since "1 week ago" --date=local > gitlog.me
    commit 331a41e0d40754f0d504372182882176e5323bfa
    Author: me <me@c2b1cd26-5903-11df-92e7-4b0514d33ac5>
    Date:   Thu Sep 15 15:14:50 2011

        Me/You: PRQ-735, consolidated common testing bits for resources into a parent class in the test harness to make maintainance of tests less tedious, cuz thats how we roll.
    
        git-svn-id: svn://svn.our.com/REPO/ourproject/trunk@16959 c2b1cd26-5903-11df-92e7-4b0514d33ac5o

    commit 03a6c145784327ef0617a43c30d228f0dcdf48fc
    Author: me <me@c2b1cd26-5903-11df-92e7-4b0514d33ac5>
    Date:   Mon Sep 12 17:10:04 2011

        You, Me: PRQ-735, began refactoring resources to new convention by collapsing duplicates, currently reside in NewResource; more class name changes to come.
    
        git-svn-id: svn://svn.our.com/REPO/ourproject/trunk@16742 c2b1cd26-5903-11df-92e7-4b0514d33ac5


