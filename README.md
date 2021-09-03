# gitflow - for agile teams


A simple GitHub git workflow for agile teams based on issues and pull requests

This workflow does not guarantee a working master, if that is required a staging branch can be used, but that is beyond the scope of this document

#Rules
1. Never work on ``master``
2. Pulling ``master`` should never create a merge commit
3. Tests are run after ``pull`` and before ``commit``
3. Describe _Features_ in _Issues_
4. Work on _Issue Specific Feature Branches_
5. Regularly ``git rebase origin/master`` _Feature Branches_ to updated ``master``
6. _Interactive Rebase_ before _Creating Pull Request_
7. _Peer Review Pull Request_
8. _Delete Feature Branch_ after _Pull Request Approval_


#Getting Started
##Sprint Planning - Prioritize Issues
The team or Product Owner will need to decide what it is that we are doing and what are the priorities.

For the purposes of the simple workflow the terms _Feature_, _Story_ and _Issue_ are all conflated together to mean a small unit of work which can be completed by a single team member (or pair). In real world projects these terms may represent larger units of work. For this workflow we recommend that all work be iteratively broken down in to small units which can be accomplished relatively quickly by a single team member or pair, and for this documment we shall use the term _Feature_

The  _Features_ should be expressed in some ordered form in some system. In the simplest case this can be done directly in the _GitHub Issues_ for this repo, although in larger projects a more flexible system should be used. 

However it is acheived each _Feature_ should be a short unique indentifier (typically an integer or other code). This _Feature Id_ should be referenced in the _Commit Messages_ and _Feature Branches_

A number of _Features_ may be grouped together into a _Sprint_. 

Normally _Sprint_ are a repeating 1 to 4 week cycle, generally the team has some idea of how much work it can commit to for the specified amount of time and the team selects that amount of work for the _Sprint_. After a few cycles the team may develop a reasonable estimation process, but just do your best for the first iteration.

##Possibly Fork Repo
If you do not have write access to the the target repo, then fork it first and then proceed

##Clone the repo
```
git clone CLONE_URL
```

##Sprint - Workflow Notes
Following this start, the _Feature Process_ below should be followed repeatedly until the _Sprint_ is complete

#Feature Process (Repeat for each _Feature_)

##Identify the Feature
In _GitHub Issues_ identify the feature you want to work on and _Assign the Issue_ to yourself
Normally this would be the _Highest Priority Feature_ which is in the _Sprint_

##Pull master updates
Pull the latest updates on your local repo
```
git checkout master
git pull origin master
```
This should __never__ result in a _merge commit_ because no one is ever working in ``master``

##Create a Feature Branch
Make sure you are on master
```
git checkout master
```
Create a _Feature Branch_ with a well formated branch name:
* The _Feature Id_ (or GitHub Issue Number)
* A hyphonated lower case human readable short feature name
```
git checkout -b 123124-short-feature-name
```

##Work on the Feature Branch
Actually do the coding and testing
* Write Tests
* Write Code to make Tests Pass
* ``git add -p`` or ``git add .``
* ``git commit -m'Useful commit message'``

##Keep Feature Branch up-to-date with master
As you work periodically, after you know of changes to master or when your feature is complete -
Fetch the remote master and rebase your _Feature Branch_ to those changes: 
```
git fetch origin master
git rebase origin/master
```

##Complete your Feature
__OPTIONAL__ Skip rebase/squash if you are just getting started with git 

Once you have completed your feature you may wish to squash some of your commits together so that your feature can be seen as single commit in the remote repo

* Begin the squash:
```
git rebase -i origin/master
```
* Inside this first editor session edit the ``pick`` to ``squash`` for all but the top commit, save and quit
```
pick 4dce685 Adding view
squash 1f5d362 Editing controller
squash 8ce4813 Adding migration
squash f66a754 Adding name and role to model
```

* Inside the send editor session edit the whole commit message to incldue the _Feature Id_ and the _Feature Description_
```
[#123124] Short Feature Description

... other commit messages should be retained below:

* Adding view ...
* Editing controller ...
```

##Push Your Feature Branch
``` git push origin 123124-short-feature-name```


##Create a Pull Request
On GitHub create a Pull Request to the master branch

##Peer Review Pull Request
Review code and suggest fixes
* Fixes would be made locally on the feature branch and then the updates pushed with
``` git push origin 123124-short-feature-name```
* This will automatically update the pull request

##Approve Pull Request
This will update master on the remote repo

##Check the Master Merge
Get the updates
```
git checkout master
git pull origin master
```

##Re-Run the Test suite
* Run the test suite on the master branch
* If problems are found then fix on a new _Feature Branch_

##Close The Issue
The issue should be automatically linked by the commit comment, close the issue

##Delete Feature Branch (Optional)
You can do this immediately to keep the repo tidy, but you may also choose to wait until later
* Locally - Using ``git branch -d 123124-short-feature-name``
* On GitHub - Using the option on the _Pull Request_

##Now Repeat for the Next _Feature_ 
At least until the end of the _Sprint_

#Sprint Wrapup

##Review
After the 1 to 4 week cycle the _Sprint_ concludes and the team should conduct a _Review_ of what worked well, what did not and how things might be improved

##Now Repeat for the Next _Sprint_
