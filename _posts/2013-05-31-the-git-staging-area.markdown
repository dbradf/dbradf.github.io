---
layout: post
title: "The git staging area"
date: 2013-05-31
category: tools
---

Git encourages users to think about what they are committing and one of the ways that it does this is with the "staging area."

Staging changes allows you to mark what changes should be included in the next commit. If no changes are staged, by default git commit won't do anything. 
 
### git status

The 'git status' command can be used to show the contents of the staging area. There are three areas where a file may show up in git status:

* Changes to be committed

This is the list of files in the staging area. These file have been modified and the user has told git to stage the changes.

* Changes not staged for commit

This is the list of files that have been modified, but have not been staged.

* Untracked files

These are files that do not belong to the git repository.


Here is some sample output from the git status command:
 
    $ git status
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #       modified:   vimrc
    #
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   vim/colors/molokai.vim
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #       untracked_file.txt
 
This output shows 4 files. One is the staging area (disk.c). One that has been modified, but not staged (diskworker.c). And two that are untracked (cscope.files and cscope.out).

In addition to showing the state of files in the repository, git status also shows what commands to run change the file state.

When the 'git add' command is run on a file, it will add the changes to that file to the staging area. If the file was previously untracked, then it will be staged to start tracking that file.

When 'git reset HEAD' command is run on a file, the changes to that file will be removed from the staging area. It is important to note that the changes are not removed from the file, the only change is that the file is no longer marked to be committed. The file will not show up in the 'changes not staged for commit' section.
 
### git commit

After some changes have been added to the staging area, you can change your staging area to a commit with the 'git commit' command. Running 'git commit' will no arguments will commit the contents of the staging area in a new commit. When 'git commit' is run, it will take you to an editor to create a commit message. The editor will be loaded with the output from 'git status', which will provide a summary of what is being committed.
 
#### Using hunks

It is interested to note that the staging area is not based on files, but based on changes. Which means that you can stage some changes to a file, but not all changes to a file. 

This can be useful if you have unrelated changes that you would like to commit to 2 separate commits, or if you have extra code that is useful for testing, but you don't want to be committed. (Note: when crafting commits this way, I strongly recommend ensuring that the commit builds on its own before pushing it to other people. The git stash can be useful for doing this type of testing).

The 'git add -p' command will take you through a file's changes hunk by hunk and let you specify whether that hunk should be staged or not. Here is an example:

    $ git add -p
    diff --git a/vimrc b/vimrc
    index 0febac4..944ccde 100644
    --- a/vimrc
    +++ b/vimrc
    @@ -3,6 +3,8 @@
    
     let mapleader = ","
    
    +" Change 1
    +
     " ======= General Options ========
    
     set nocompatible " Don't need vi compatibility
    Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]? n
    @@ -27,6 +29,9 @@ set directory=$HOME/tmp " Use a temporary directory for swp files
     " ======= Setup for terminials =======
     set t_Co=256
    
    +
    +" Change 2 here
    +
     " ======= Setup Pathogen =======
     " Note that you need to invoke the pathogen functions before invoking
     " 'filetype plugin indent on' if you want it to load ftdetect files.
    Stage this hunk [y,n,q,a,d,/,K,g,e,?]? 

There are a lot of choices. The two most command are 'y' to add a change to the staging area and 'n' to not a changes to the staging area.

A final note on hunks, using 'git add -p' can be somewhat cumbersome (especially for a large amount of changes). There are, however, a lot of 3rd party tools and plugins that can make committing in hunks much easier. I frequently use the fugitive plugin for vim.

 
### git diff

While 'git status' provides a nice summary of the current status of your changes, frequently you will want to see more details of what the actually changes are. The 'git diff' command can show you what the actually changes are. There are three useful invocations of the 'git diff' command:

* git diff

By default, 'git diff' will show you changes that have not been staged. This corresponds to the 'Changes not staged for commit' section of 'git status'.

* git diff --staged

Adding the --staged flag to git diff will show you changes that have been staged. This corresponds to the 'Change to be committed' section of 'git status'.

* git diff HEAD

The 'git diff HEAD' invocation of 'git diff' will show you both the staged and unstaged changes. This will show you all changed from the last commit.

By adding '' to the end of any of the 'git diff' commands will only display changes for the specified file.
