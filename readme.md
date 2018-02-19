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

> You can name the folder whatever you would like.

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

## Merging - We do

How do we merge our changes with the `master` branch? `git merge`

```bash
$ git checkout master
$ git merge feature-update-hello
```
