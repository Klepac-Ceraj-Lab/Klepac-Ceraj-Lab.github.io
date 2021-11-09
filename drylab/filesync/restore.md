+++
title="Restore from cloud"
+++

So, everything has gone to hell,
all of your hard-drives are destroyed or corrupted,
Kevin is dead, incapacitated, or just not responding to email,
and you need to restore files from the cloud backup.

First, I'm so sorry.
Things must be in bad shape right now.
Don't worry, it will be OK! 🤗

## Set up machine for restoring backup

If things are so borked that you need the cloud backup,
there's a good chance you'll need to re-install the software.

Go back to [this page](../index/#setting_up_duplicity) and make sure you have

1. Installed `duplicity`
2. Set up a developer app with read/write credentials (for this part, you only need read)
3. Installed `pydrive` and other dependencies
4. Remember the decryption password (Diamond sutra)

## Downloading

To restore the backup, just reverse the source and destination arguments, eg:

```sh
$ GOOGLE_DRIVE_SETTINGS=~/.duplicity/credentials duplicity --exclude-filelist ~/.duplicity/excludes "pydrive://developer.gserviceaccount.com/<Subdir on Shared Drive>/?driveID=<Shared Drive ID>" <destination directory> 
```