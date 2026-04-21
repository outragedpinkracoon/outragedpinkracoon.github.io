---
title: Setting new branches to 'main' by default
description: Automatically default to 'main' instead of master in git for new repositories.
layout: post
categories: [git, programming]
---
You can use: `git init --initial-branch=main` to initialize a new branch called ‘main’ instead of master.

To set this globally for new repos you can use: `git config --global init.defaultBranch main`

Neat, make the magic happen.
