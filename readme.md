# Git Workshop

## Preferred Requirements

- Basic CLI
- a github account

## Learning Objectives (5/5)

- Define version control and identify what problems it solves for developers
- Define a repository (aka repo) is, and identify what the parts of a repo are
- Differentiate between a local repository and a remote repository
- Synchronize a local repository with a remote repository using git with Github

## Framing (5/10)

Simply put, version control is a way of *tracking changes* made to a file or group of files over time.

It's very likely that each of us has tried to keep track of changes made to a file by creating different versions of that file. This however can be messy or complicated especially when working in teams.

### Think Pair Share 5/15

Think about the following questions for 2 minutes:

- What are some reasons we might want different versions of a project?
- What are some strategies you've used in the past? (outside of VC)
- What problems, if any, did you encounter?
- How can version control software be leveraged to solve these problems?

Then share with someone sitting next to you about your thoughts.

## Git - Git solves problems. 5/20
- I wrote some code to implement a feature, but I broke a bunch of stuff in the process. **I want to be able to go back in time to a point where my code works!**
- I'm trying to see how my codebase or some files have changed over time. **I'd like to be able to compare various states of my files.**
- I want to work on someone else's project, but don't want to break their code and ruin everything. **I want to have my own 'area' where I can try out code or build out a feature without adversely affecting another developer's project I'm working on.**
- I'm working on a project with a team, and **I want to have an easy way to collaborate with my team**

## Git - Some basic definitions

- Git - It is version control software. Today we'll be using the CLI to use git.
- Repositories - Git stores information about a project in a data structure called a repository.
- Commit - records changes to the repository
- Branch - A branch in Git is simply a lightweight movable pointer to one of these commits.
- the index - also called the staging area. It is where we add changes to be committed

> There will be more defintions, we'll spread them throughout the lesson but also conglomerate them into an appendix at the bottom of this lesson.

## Local git - We do
Lets GIT started .... open your terminal.

Creating a git repository:

```bash
$ mkdir git-workshop
$ cd git-workshop
$ git init
```

> You can name the folder whatever you would like. `$` will be used to indicate the start of the command prompt

You should see something like this:

```
Initialized empty Git repository in /Path/to/git-workshop/.git/
```

Create a file and add some content to it:

```bash
$ touch hello.txt
$ echo "hello" > hello.txt
```

Stage it:

```bash
$ git add hello.txt
```

Commit it:

```bash
$ git commit -m "git init; adds hello.txt"
```

> Commit commands must always be accompanied by a commit message. Generally try to write commit messages in the imperative. As when you check out to a commit, you are "executing" that commit message

## Branching

Well this is amazing, we're successfully tracking our extremely complicated project in git. As developers, we like to keep places in our projects that are "pristine" and protect it through code reviews. Every team probably practices these workflows a bit differently, but everyone uses branches in order to solve this problem. 

Branches quite literally point to a commit. Turns out we can branch locally as well.

Creating a git branch

```bash
$ git checkout -b feature-update-hello
```

> `feature-update-hello` is the name of the new branch were checking out. 

### You do - Commit a change to `hello.txt`

- Make edits to `hello.txt`
- Stage the changes
- Commit the changes

### Git diff aside

- Make another change to `hello.txt`
- **Before staging and committing** Run this command:
```
$ git diff
```

What does git diff do?

## Merging - We do

How do we merge our changes with the `master` branch? `git merge`

```bash
$ git checkout master
$ git merge feature-update-hello
```

you should see something like this depending on what you edited: 

```
Updating bd9e339..c9f4b8c
Fast-forward
 hello.txt | 1 +
 1 file changed, 1 insertion(+)
```

## Git logs

We've made a couple of commits at this point. In order to see a history of the changes we've made, we can run `git log`

```
$ git log
commit c9f4b8c355e2604149e4a6a20d7e042507cb9cac
Author: Andy <andrew.sunglae.kim@gmail.com>
Date:   Sun Feb 18 22:22:00 2018 -0500

    updates

commit bd9e339bf4242c7fd47c3e8b89af917ffee57503
Author: Andy <andrew.sunglae.kim@gmail.com>
Date:   Sun Feb 18 22:21:37 2018 -0500

    initial commit

```

It may look diferrent than your's, but the same types of information are present.

In reverse chronological order(most recent commits first):
- git SHA-1 checksum
- author's name and email
- Date
- commit message

> Check out the end of the lesson plan for a quick reference on how to pretty the PS1. 

The important thing to note here is the `git SHA-1 checksum` but that's getting troublesome to say, so we'll say git SHA from here on out. In more or less words, it is a unique pointer to a snapshot in your projects history. We won't use this immediately, but we'll reference back to this when we revert commits.

## MERGE CONFLICTS

> Stop. Take a breath. Don't run. Don't be afraid. Except ... be a little afraid.

Merge conflicts are a reality of development. They will happen and frequently. 

First off, How do merge conflicts occur? They occur when two branches are merging and both branches change the same file.

## We do - CREATE THE CONFLICT

Since we have recently merged `feature-update-hello`. The history of `master` and `feature-update-hello` should be identical. 

```
$ git checkout master
$ echo "master changes" > hello.txt
$ git add hello.txt
$ git commit -m "changes hello.txt with master changes"
$ git checkout feature-update-hello
$ echo "feature branch changes" > hello.txt
$ git add hello.txt
$ git commit -m "changes hello.txt with feature branch changes"
```
> **Don't** do this step in an actual merge conflict. 