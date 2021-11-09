+++
title="Cloud Backup"
+++

This page contains instructions for doing **incremental backup**
of lab hard drives to google drive.
If you're looking for information on transferring files
between different computers, [see here](rsync.md).

## Before getting started

Before getting started,
you should have followed [these instructions](../index/#setting_up_duplicity)
## Run sync

Assuming you followed the post linked above[^dupgdrive],
and have your credentials stored in `~/.duplicity/credentials`,
and a list of files to exclude stored in `~/.duplicity/excludes`,

```sh
$ GOOGLE_DRIVE_SETTINGS=~/.duplicity/credentials duplicity --exclude-filelist ~/.duplicity/excludes <source directory> "pydrive://developer.gserviceaccount.com/<Subdir on Shared Drive>/?driveID=<Shared Drive ID>"
```

- `<source directory>` should be replaced with the local path to the drive you want to backup,
  eg `/lovelace/`
- `<Subdir on Shared Drive>` should be replaced with a subdirectory on the shared drive,
  eg `lovelace`
- `<Shared Drive ID>` should be replaced with the drive ID from google, which is the last part
  of the URL when you're in the team drive online, eg `0AAFXKrJrjeBbUk9PVA`

  ![Shared Drive ID](/assets/img/gdrive_shared_id.png)

I (Kevin) sent the decryption password to both Vanja and Shelley - hint = "Diamond Sutra"