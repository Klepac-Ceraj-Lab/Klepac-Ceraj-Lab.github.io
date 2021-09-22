+++
title="File Sync and Backup"
+++

# File Sync and Backup

All of the primary [lab drives](computers/) are regularly synced to the cloud using google drive
(since we have unlimited storage there).

There is a [Shared Drive][^shareddrive] on google drive for backed up directories.
## Setting up duplicity

`duplicty`[^duplicity] is a command-line tool that enables encrypted and incremental backup
with a number of different services, including google drive
(which is important, since we have unlimmited storage on Wellesley's gdrive).

### Set up google api and duplicity[^dupgdrive]

There are a bunch of guides online[^dupgdrive] to setting up google drive
as a backend for `duplicity`.
If you're setting up gdrive for the first time, follow the tutorial [found here](https://rgarth.github.io/2017/10/29/Grive-and-Duplicity/).
The basic procedure is

1. Make yourself an app using google developer console that has
   the ability to manage gdrive folders
   (I was able to make one that only had read/write permission on its own folders)
2. Get the credentials, and save them in a file on your local drive.
   I used `pass`[^pass] to encrypt these credentials.
3. Make sure to install right versions of python deps[^pydrive] -
   you need `httplib2` v.0.15.0 and `google-api-python-client` v1.6
4. ????
5. Profit

## Run sync

Assuming you followed the post linked above[^dupgdrive],
and have your credentials stored in `~/.duplicity/credentials`,
and a list of files to exclude stored in `~/.duplicity/excludes`,

```sh
$ GOOGLE_DRIVE_SETTINGS=~/.duplicity/credentials duplicity --exclude-filelist ~/.duplicity/excludes <source directory> "pydrive://developer.gserviceaccount.com/<Subdir on Shared Drive>/?driveID=<Shared Drive ID>"
```

- `<Drive to backup>` should be replaced with the local path to the drive you want to backup,
  eg `/lovelace/`
- `<Subdir on Shared Drive>` should be replaced with a subdirectory on the shared drive,
  eg `lovelace`
- `<Shared Drive ID>` should be replaced with the drive ID from google, which is the last part
  of the URL when you're in the team drive online, eg `0AAFXKrJrjeBbUk9PVA`

  ![Shared Drive ID](/assets/img/gdrive_shared_id.png)

I (Kevin) sent the decryption password to both Vanja and Shelley - hint = "Diamond Sutra"

## Downloading

To restore the backup, just reverse the source and destination arguments, eg:

```sh
$ GOOGLE_DRIVE_SETTINGS=~/.duplicity/credentials duplicity --exclude-filelist ~/.duplicity/excludes "pydrive://developer.gserviceaccount.com/<Subdir on Shared Drive>/?driveID=<Shared Drive ID>" <destination directory> 
```

## References

[^duplicity]: [Duplicity](https://gitlab.com/duplicity/duplicity) is a program for making encrypted backups. Install it with `sudo apt install duplicity` (linux) or `brew install duplicity` (mac)
[^dupgdrive]: [Follow this tutorial](https://rgarth.github.io/2017/10/29/Grive-and-Duplicity/) when setting up GDrive and duplicity for the first time
[^pass]: See [this page](pass/) for info on setting up `pass`.
[^pydrive]: https://stackoverflow.com/a/61188575/3742902
[^shareddrive]: https://drive.google.com/drive/u/1/folders/0AAFXKrJrjeBbUk9PVA