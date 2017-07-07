---
layout:     post
title:      Command Line Shortcuts
author:     Nia
tags: 		  Terminal
subtitle:  	Daily Review
category:   daily
---

Today I figured out how to implement some shortcuts to use in Terminal. I've always found it annoying to move among directories from the command line, and especially getting to my projects folder which is nested pretty deeply. I've also seen other people type shorter commands than I was using, and I wanted to do it to! Lots of googling and I came up with a result.

### Show Hidden Files

The first step is to make it so that Finder displays hidden files with these two lines in Terminal:
```
defaults write com.apple.Finder AppleShowAllFiles true
killall Finder
```

Then open a Finder window and navigate to the root user folder (for me it's what shows up on the command line before `$`). There are three files to open: `.gitconfig`, `.bash_profile`, and `.bashrc`.

### Add git shortcuts to .gitignore

I started here from some bad googling--the steps below can make this redundant--but here it is anyway. I added the following lines into `.gitignore` to simplify my git commands:
```
[alias]
  a = add .
  c = commit -am
  p = push
  s = status
  cob = checkout -b
```

So now instead of typing `git checkout -b branchName` I can just type `git cob branchName`. Better!

But there is a better way yet...

### First Direct .bash_profile to .bashrc

When a Terminal window opens it uses one of two settings, and the two settings are managed by these two files (explained better in [this YouTube video](https://www.youtube.com/watch?v=vDOVEDl2z84)). To make sure the shell sees the shortcuts no matter which way Terminal opens, direct `.bash_profile` to `.bashrc` by adding this line to the file:
```
if [ -f ~/.bashrc ]; then
	source ~/.bashrc
fi
```

### Then add shortcuts to .bashrc

First I added a function to change a 2-step process into 1: making a new directory and then changing into it:
```
# mkdir, cd into it
mkcd () {
mkdir -p "$*"
cd "$*"
}
```

Then I went a step further and made a specific function to open my dev projects folder from root:
```
# Go to dev folder & list
function dev {
    cd ~/really/long-And-cOmpliCated/path/to/my/dev-projects/
    ls
}
```

I also want to be able to see all of the folders and files in a directory as soon as I cd into it:
```
# cd, then ls directory
function cdl {
    cd $1
    ls
}
```

And finally a bunch of shortcuts to make life easier:
```
# Aliases
alias ..="cd .."
alias gaa="git add ."
alias gb="git branch"
alias gcm="git commit -m"
alias gcob="git checkout -b"
alias gl="git log"
alias gp="git push"
alias gs="git status"
alias lsa="ls -a"
alias t="touch"
```

So I one-upped my .gitignore shortcut and now type `gcob branchName` in the example above. Win!

### Hide Hidden Files

Most of the time I'd rather not see all of the hidden files in Finder so to wrap up, undo the first step by entering the below in Terminal:
```
defaults write com.apple.Finder AppleShowAllFiles false
killall Finder
```

### Shell Errors

This is the final output, but initially I got some errors from copying other people's suggestions. Still a lot to learn about shell scripting but I can say for sure that it prefers double quotes `" "` to single `' '`! Also there is this great tool which will tell you what the errors are and how to fix them: [ShellCheck](http://www.shellcheck.net/).

## Other Stuff

Got started on the big capstone project for my bootcamp class, a Yelp clone showing campgrounds. I'm calling mine [FireCamp](https://github.com/niamurrell/firecamp-yelp-clone). Should be fun!

## Up Next

Still pausing on the group [Metro project](https://github.com/CodingForProduct/metro_reward) until we figure out our framework so for now working on the bootcamp. Next section is about databases so should be getting into MongoDB.
