# Happier Git Workflow

## General Rules

* If it’s possible, create branches over the JIRA (except the master branch)
* Every Release must have a *Release Package* on the JIRA
* Every Release, Feature or Bugfix …etc. must have an own branch
* Always add the JIRA Issue Key in the “commit description”
* Never push to the master without a Pull request
* After pushing to the master add a tag for that commit. You should always be able to back that specific release (time-traveling) for starting a hotfix 
* After pushing to the master close push option for the release branches
* Create the release branch as late as possible.

## Naming Convention

* All your branch names must be in lowercase
* Your master branch should be named as "master"
* Use this formatting for your release branches: release-1.3 or release-1.1.3
* Update your build number only if you send a build for Testflight or QA Team. If you have a freshly started project, start from number "1". 
Don't use a Build Phase script for increasing your build number for each build. 
* Use this tag formatting: 
```
[version].[build number]
```		
an example would be:
```
1.5.9.201
```

* Your branches must have formatting like the line below:

```
* feature/your-jira-issue-key-[short-title]
* bugfix/your-jira-issue-key-[short-title]
* release/release-1.5.9
```

# How to create a branch on the JIRA Software

Use the *Development > Create a branch* to create a new branch over the JIRA.

![Step 1](./CREATE-BRANCH-1.png)

Don't forget to select a branch type, check before submitting, currently JIRA won't select the correct type. Then click to the *Create Branch* button.

![Step 2](./CREATE-BRANCH-2.png) 

If you see formatting like below for the *Branch name*, please communicate your Product Owner, Project Manager or SCM Team (Software Configuration Management):


**Incorrect**
```
* feature-your-issue-key
* bug-your-issue-key
```

**Correct**
```
* feature/your-issue-key
* bug/your-issue-key
* release/your-[version]

```

# SCM (Software Configuration Management) Processes

For *SCM* tasks we should create a special tag like the line below: 

```
testflight-[version]
```

an example would be:

```
testflight-1.1.5
```

this should trigger your CD (Continuous Delivery) flow. Also, you can check the [Fastlane document](https://github.com/gurhub/fastlane).


# Exceptions

* Normally, after merging all branches you shouldn't push any commit to the *release branch*. But in practice that's not the case. You might need to update your IDE or increase the build number of your application under this branch. After updating your IDE, the application might update some of the configuration files. We can't put this commits in other branches. And that's not easy to create different JIRA issues for each *special case*. So, we need to use our *release branches* for this purpose too.

* If you need to delete your release branch for some reason. You have 2 options. You can redo all the updates. Or before deleting your branch you can create your desired branch, after that, you can take all config updates with the [cherry-pick](https://git-scm.com/docs/git-cherry-pick). Then you can delete your unwanted branch safely.

* If more than one version of Testflight is going to be released, we should make the following decision after the first submission:

  - If a branch is created for a new issue, it will normally be derived from the master.

  - If there is an improvement on the merged issue in the release branch; Instead of the master branch, a branch is created from the related issue.

  - If more than one issue is linked to the release branch; we need to create issues through the release branch. However, if we need to delete the release branch later, The responsible developers should consult with the solution plan in advance before deleting it.
