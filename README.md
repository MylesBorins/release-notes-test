# Versioning Strategies @ WLCR

## Why

**More managable, maintainable, & intelligible change logs / versioning**

## :book: Table of Contents
[Auto generate release notes from within the github UI](#auto-generate-release-notes-from-github-ui) |
[Main Branch Workflow](#main-branch-workflow) |
[Develop Branch Workflow](#develop-branch-workflow) |
[Semantic Versioning](#semantic-versioning) |


## Auto generate release notes from within the github UI

### Step 1

* Add `.github/release.yml` config file to your project ([github docs](https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes))

### Step 2
* In your `release.yml` file set categories, titles & labels in the following format:

example `.github/release.yml` config:
```yml
changelog:
  categories:
  - title: Breaking Changes
    labels:
    - breaking-change
  - title: Features
    labels:
    - feature
    - enhancement
  - title: Bug fixes
    labels:
    - bug
    - patch
  - title: Docs
    labels:
    - docs
    - documentation
  - title: Refactor
    labels:
    - refactor
  - title: Config
    labels:
    - config
    - configuration
  - title: Other Changes
    labels:
       - "*"
```

**Important** *make sure that any labels you use in your config are also added to the repo ([managing labels
](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels))*

### Step 3
Once you've setup your `release.yml` file and added the correlating [labels](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels) development on the project should follow either our [Main Branch Workflow](#main-branch-workflow) or [Develop Branch Workflow](#develop-branch-workflow) making sure that all branch names correlate with labels and that those same labels are added to their respective PRs.

### Step 4
After a PR has been merged, release notes should then be generated following these instructions [github docs](https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes)

## Branching Strategies
Generally speaking most of our projects start out using a [Main Branch Workflow](#main-branch-workflow) and when needed (QA, Version freezes, etc) will shift into a [Develop Branch Workflow](#develop-branch-workflow). Read their respective sections to learn more about each flow and when and how to use them.

  *IMPORTANT: regardless of which branching strategy is being used, in order to keep our repos and our versioning more clear & better organized branch names should always correlate to a label used in the [`release.yml`](#step-2) file and that same label should be attatched to the PR for that branch. For example: `feature/hp-hero`*

### Main Branch Workflow
In this branching strategy the main branch always contains production-ready code and all other branches will start from and merge back into the main branch. This is a strategy popularized by [github flow](https://githubflow.github.io/) that is well suited for small teams, CI/CD, & web projects. This workflow is how we typically start our projects.

### diagram
![Github Flow Diagram](/assets/github-flow-diagram.svg)

### Limitations of the Main Branch Workflow

* Unable to support multiple versions of code in production at the same time.

* Lack of a dedicated development branch makes makes it more susceptible to bugs in production.


### Develop Branch Workflow
When our main branch needs to remain unchanged we adapt our workflow to be more aligned with another very popular branching strategy by the name of [gitflow](https://nvie.com/posts/a-successful-git-branching-model/).

The key difference in this workflow is that all new work should be performed on a `develop` branch that is itself a branch off of the main branch. In this flow all new branches (features, bugs, etc) start from the develop branch and all PRs should be merged back into that same develop branch (an exception could be when a hotfix is needed on main).

When the main branch is at a point it's ready to be updated again -- ie QA has finished, or it's time for an updated version of a site to launch -- then the develop branch should be merged into the main branch.

**IMPORTANT** while it's good practice to continually be generating change logs / versioning during development it is especially important at this time (see [Auto generate release notes from within the github UI](#auto-generate-release-notes-from-within-the-github-ui))

### diagram
![Git Flow Diagram](/assets/git-flow-diagram.svg)

Drawbacks to the Develop Branch Workflow:

* It can overcomplicate & slow the development process & release cycle (recommended reading [Note of reflection](https://nvie.com/posts/a-successful-git-branching-model/) by the creator of this workflow).

## [Semantic Versioning](https://semver.org/)

#### MAJOR.MINOR.PATCH

* _MAJOR_
  * breaking changes from the previous version
* _MINOR_
  * added functionality in a backwards compatible manner
* _PATCH_
  * backwards compatible bug fixes & trivial updates

![Semantic Versioning Structure](/assets/semvar-structure.png)



