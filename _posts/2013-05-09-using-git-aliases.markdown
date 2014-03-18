---
layout: post
title: "Using git aliases"
date: 2013-05-09
category: technology
---

Git aliases provide a way to create shortcuts for complex git commands.
 
To create a git alias:
* Open your ~/.gitconfig file
* Find or Add the \[alias] section of the file.
* Add the aliases you would like to use.
 
Aliases are added in the following form:
>
>alias_name = git command to be run
>
After adding an alias, it can be executed using the git command, 'git alias_name'
 
Here are a few aliases from my ~/.gitconfig file:

    [alias]
        lol = log --pretty=oneline --abbrev-commit --graph --decorate 
        pr  = pull --rebase
