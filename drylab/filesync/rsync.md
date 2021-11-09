+++
title = "Using Rsync for file transfers"
+++

# File transfers with rsync

`rsync` is a ubiquitous and powerful file transfer system
that can be used to transfer individual files or whole drives
locally or over [`ssh`](/drylab/ssh), and provides

- **Incremental backup**:
  If you've already sync'd a directory, `rsync` won't re-transfer files (unless they've changed).
  This also means that interrupted transfers can be resumed.
- **include / exclude patterns**:
  You can set up patterns of files to transfer or not,
  based on glob patterns, or pass explicit lists of files.
  You can also save these patterns in particular directories for repeated use.
- **Destructive or non-destructive**:
  By default, rsync backups are non-destructive (that is, files won't be deleted),
  but you can choose to make source and destination mirrored
  (deleting files that don't exist at the source) using explicit commands.

