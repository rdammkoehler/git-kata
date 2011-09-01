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
