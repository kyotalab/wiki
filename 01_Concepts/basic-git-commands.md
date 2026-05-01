---
title: "Basic Git Commands"
tags: [git, version-control, workflow]
source: "https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/how-to-basic-git.html"
created: 2026-04-30
related: [git-branching, git-commits, remote-repositories]
---

# Basic Git Commands

Basic Git commands are the core operations used to configure repositories, track changes, and synchronize local work with remote repositories.

## How It Works

Git command usage usually follows a lifecycle: configure identity and defaults, initialize or clone a repository, inspect and stage changes, commit snapshots, and then exchange commits with a remote. Configuration commands such as `git config --list` and `git config --global init.defaultBranch main` define behavior before daily work begins, while repository setup commands like `git init`, `git clone`, and `git remote add` establish where project history lives.

During active development, status and diff commands make repository state visible. `git status` and `git status -sb` show what is modified, staged, or untracked, and `git diff HEAD` compares working changes against the latest commit. Staging and committing with `git add` and `git commit` then turn selected edits into a durable history entry. Log commands such as `git log --graph` help developers understand commit structure over time, not only individual commits.

Branch and tag commands extend this model for parallel work and release markers. Branch commands create isolated lines of development, switch context, merge completed work, and remove obsolete branches. Tag commands mark specific commit points for versioning, and can be fetched, pushed, and deleted independently from branches.

## Why It Matters

A practical command set reduces friction in everyday collaboration. Teams can move faster when everyone shares a predictable workflow for checking status, committing clean history, and syncing with remotes.

These commands also improve safety. Clear visibility into staged versus unstaged changes lowers accidental commits, while explicit branch, merge, and tag operations make release and integration steps easier to audit. In hosted environments such as AWS CodeCommit, the same command model provides a consistent bridge between local development and centralized repository management.

## Related Concepts

`[[git-commits]]` explains how snapshots and commit history are structured. `[[git-branching]]` covers parallel development and merge strategy. `[[remote-repositories]]` describes synchronization mechanics such as push, pull, and tracking branches.
