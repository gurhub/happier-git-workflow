# Happier Git Workflow

## Description
A happier Git Workflow for most of us.

## General Rules

* Always create the branches over the JIRA (except master branch and release branches)
* Every Release, Feature or Bugfix …etc.  must have an own branch
* Always start your first “commit description”  with the JIRA Issue Key.
* Never push to the master without a Pull request
* After pushing to the master add a tag for that commit. You should always be able to back that specific release (time-traveling) for starting a hotfix 
* After pushing to the master  close push option for the release branches
* Create the release branch as late as possible.

## Naming Convention

* All your branch names must be in lowercase
* Your master branch should be named as "master"
* Use this formatting for your release branches: release-1.3 or release-1.1.3
* Update your build number only if you send a build for Testflight or QA Team. If you have a freshly started project, start from number "1". 
Don't use a Build Phase script for increasing your build number for each build. 
* Use this tag formatting: 
```
[version].[build number].
```		
For example:
```
1.5.9.201
```

* Your JIRA issues must have a formatting like line below:

```
* feature/your-jira-issue-key
* bugfix/your-jira-issue-key
```

# How to create a branch from JIRA 

Use the Development > Create a branch to create a new branch over JIRA:

![Step 1](./CREATE-BRANCH-1.png)

Don't forget to select a branch type, check before submitting, currently JIRA won't select the correct type. Then click to the Create Branch button.

![Step 2](./CREATE-BRANCH-2.png) 

If you see formatting like below for "Branch name", please communicate your Project Owner/Manager or SCM Team (Software Configuration Management):

```
* feature-your-issue-key
* release1-1
```
