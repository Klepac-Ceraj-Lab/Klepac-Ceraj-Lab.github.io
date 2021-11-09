+++
title = "Using Rsync for file transfers"
+++

# File transfers with rsync

[`rsync`][explainshell] is a ubiquitous and powerful file transfer system
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
  By default, `rsync` backups are non-destructive (that is, files won't be deleted),
  but you can choose to make source and destination mirrored
  (deleting files that don't exist at the source) using explicit commands.
- **Preview**: you can review what is going to be transferred
  before actually initiating the transfer.

But all this power also means a lot of complexity,
and the software was released before most of you were born (1996),
so it takes a bit of effort to unlock that power.
This page will hopefully make that process a bit easier.

[explainshell]: https://explainshell.com/explain/1/rsync
## Getting started

### Installation

`rsync` should already be installed on your system.
The version that comes installed on MacOS is pretty old,
but should work just fine.
If you want a shiny new version, you can [use homebrew](http://brew.sh):
`brew install rsync`.

### SSH access

If you're transferring files between different computers
(eg from a lab server to your laptop),
you should have [set up `ssh`](/drylab/ssh) connections.
Throughout this page,
instructions assume that you have a `~/.ssh/config` file
that includes aliases for different machines,
eg `ada` for `your-user-name@vkclab-ada.wellesley.edu`.

## Transferring files

Like the shell utilities `mv` and `cp`,
the basic invocation is

```sh
$ rsync <source> <destination>
```

Where `<source>` is the location (path) of the file(s) that you are transferring **from**,
and `<destination>` is the location (path) of the directory that you're transferring **to**.

Unlike `mv` and `cp`, either `<source>` or `<destination>` (though not both)
can be a remote machine, and files can be transferred using the ssh protocol.
For example, if I want to transfer a file on `/lovelace`,
[which is a drive](/drylab/computers/#ada) attached to `ada`,
to the desktop on my local machine, I would write:

```sh
$ rsync ada:/lovelace/myfile.txt ~/Desktop/
```

Here `ada` is filled in with `kevin@vkclab-ada.wellesley.edu`,
because of my ssh configuration.
The `:` separates the "hostname" of the remote machine
and the path on that machine.

Also unlike `mv` and `cp`, you cannot use "glob" patterns (eg `/lovelace/*.txt`)
to transfer all files matching a particular pattern.
But there are other ways of accomplishing this (and even more powerful things)
using some different options.

Read on!

### The -a (--archive) flag for transferring whole directories

