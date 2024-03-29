# Happier Git Workflow


## Summary

This document describes Mobile Workflow for the mobile department and the outsourced resources. From now we'll use the term Developer to describe someone working directly or as an outsource for TMRW or its sub-companies.

Your responsibility as a developer is to follow this repository via your favorite git tool for future updates

# Git Workflow

## Basics

* No code can commit to the repository, without a JIRA issue and a commit related to that issue
* Create all branches over the JIRA
* Every Release must have a *Release Package* on the JIRA
* Every Release, Feature or Bugfix …etc. must have an own branch
* For each commit add the JIRA Issue Key in the "commit description"
* Never push to the master without a Pull request
* After pushing to the master add a tag for that commit. You should always be able to back that specific release (time-traveling) for starting a hotfix
* After pushing to the master close push option for the release branches
* Create the release branch as late as possible.
* While you're working with a dependency manager (SPM, Cocoapods, Gradle ...etc.) for 3rth party libraries, be sure you specify the current version that has been used in your app via a fixed version number. With this method, all developers will fetch the same version of that repository. Also, if you back to another tag in your master branch sometime in the future, you'll get the same exact version same as the market version. This is very critical for hotfix scenarios.

## Naming Convention

* All your branch names must be in lowercase
* Your master branch should be named as "master" or "main"
* Use this formatting for your release branches: release-1.3 or release-1.1.3
* Update your build number only if you send a build for Testflight or QA Team. If you have a freshly started project, start from number "100". 
* Don't use a Build Phase script for increasing your build number for each build. 
* Use this tag formatting:  **v[version].[build number]**. Example: **v1.5.9.201**
* Your branches must have formatting like the line below:
  * feature/your-jira-issue-key-[short-title]
  * bugfix/your-jira-issue-key-[short-title]
  * release/release-1.5.9
  
  *⚠️ **short-title** is a maximum of 5 words that describe what that issue is about.*

* Avoid long descriptive names for long-lived branches
  * ../wip_login_module_which_will_used_in_the_internal_website **Incorrect**
  * ../wip_feature_login_module **Correct**
  
# Versioning 

Sometimes we're finishing a sprint but not sending any version to the market. But we've to track every version and know exactly which version is tested and released on the market. If not any way we need to track those too.

To solve this issue, we're adding a small step for standard Semantic Versioning, but only for branch naming. For the market version, we'll stick with the Semantic Versioning.

#### Formats

| Type       | Example                                    |
| :---       | :---                                       |
| Branch     | release-[MAJOR].[MINOR].[PATCH].[SPRINT]** |
| Market     | [MAJOR].[MINOR].[PATCH]                    |
| IDE        | [MAJOR].[MINOR].[PATCH].[BUILD]            |
| Tag on Git | v[MAJOR].[MINOR].[PATCH].[BUILD]           |

**release-[MAJOR].[MINOR].[PATCH].[SPRINT]**
**[MAJOR].[MINOR].[PATCH]**

#### Scenario 1

We're on alpha phase, not sending to market. Sprint number is **2**. Build number is **123**.

| Type       | Example         |
| :---       | :---            |
| Branch     | release-1.0.0.2 |
| Market     | 1.0.0           |
| IDE        | 1.0.0.123       |
| Tag on Git | v1.0.0.123      |


#### Scenario 2

We're sending to the market. Sprint number is **3**. Build number is **127**.

| Type       | Example         |
| :---       | :---            |
| Branch     | release-1.0.1.3 |
| Market     | 1.0.1           |
| IDE        | 1.0.1.127       |
| Tag on Git | v1.0.1.127      |

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
* feature/your-jira-issue-key-[short-title]
* bug/your-jira-issue-key-[short-title]
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
