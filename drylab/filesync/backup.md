+++
title="Cloud Backup"
+++

This page contains instructions for doing **incremental backup**
of lab hard drives to google drive.
If you're looking for information on transferring files
between different computers, [see here](rsync.md).

## Before getting started

Before getting started,
you should have followed [these instructions](../index/#setting_up_duplicity).
In particular, you should have

1. Installed `duplicity` (if on a lab server, this should already be done).
2. Set up a developer app with read/write credentials
3. Installed `pydrive` and other dependencies (if on a lab server, this should already be done).
4. Remember the encryption password (search slack for "Diamond sutra")

## Uploading 🔼

### 1. Identify drive to restore

All of the lab drives are stored in the same
[google shared drive](https://drive.google.com/drive/u/1/folders/0AAFXKrJrjeBbUk9PVA),
with drive ID `0AAFXKrJrjeBbUk9PVA` (the last part of the URL above).

Find the name of the directory that you are backing up.
(for a list of lab severs and their hard drives, [see here](../../computers)).
For example, if you are backing up the 8 Gb drive on `ada`,
you will use `lovelace`.

### 2. Find the path to your google credentials

From [this tutorial](https://rgarth.github.io/2017/10/29/Grive-and-Duplicity/),
you should have saved your google app credentials
somewhere like `~/.duplicity/credentials`:

```sh
❯ cat ~/.duplicity/credentials
───────┬────────────────────────────────────────────────────────────────
       │ File: .duplicity/credentials
───────┼────────────────────────────────────────────────────────────────
   1   │ client_config_backend: settings
   2   │ client_config:
   3   │    client_id: {{LONG ALPHANUMERIC STRING - HIDDEN}}
   4   │    client_secret: {{SHORTER ALPHANUMERIC STRING - HIDDEN}}
   5   │ save_credentials: True
   6   │ save_credentials_backend: file
   7   │ save_credentials_file: gdrive.cache
   8   │ get_refresh_token: True
```

### 3. Use duplicity to sync

In the following command, replace:

- `$DRIVEID` with the shared drive ID, eg `0AAFXKrJrjeBbUk9PVA`, from [step 1](#identify_drive_to_restore)
- `$SUBDIR` with the name of the directory you're backing up, eg `lovelace`, from [step 1](#identify_drive_to_restore)
- `$CREDENTIALS` with the path to your google credentials, eg `~/.duplicity/credentials` from [step 2](#ol_start2_find_the_path_to_your_google_credentials)
- `$SOURCEDR` with the path on your local system that you want to back up. Eg `/lovelace/`

```sh
$ export GOOGLE_DRIVE_SETTINGS=$CREDENTIALS
$ duplicity $SOURCEDIR "pydrive://developer.gserviceaccount.com/$SUBDIR/?driveID=$DRIVEID" 
```

So, following the examples above,
if you want to back up the `lovelace` drive on `ada`,
you might do:

```sh
$ export GOOGLE_DRIVE_SETTINGS=~/.duplicity/credentials
$ duplicity /lovelace "pydrive://developer.gserviceaccount.com/lovelace/?driveID=0AAFXKrJrjeBbUk9PVA"
```

### 4. Authenticate (possibly)

You may be asked to authenticate via your browser.
Eg - there will be a prompt like:

```
Go to the following link in your browser:

    https://accounts.google.com/o/oauth2/auth?client_id={{STUFF}}.apps.googleusercontent.com&redirect_uri={{SOME_OTHER_STUFF}}%2Fauth%2Fdrive&access_type=offline&response_type=code&approval_prompt=force

Enter verification code:
```

Copy the text of the url and paste it into a browser,
then sign in to your Wellesely account, and click "approve."
There will then be a long alphanumeric string that you need to copy
and paste back in your terminal.

### 5. Enter encryption password

You will then be prompted to enter the encryption password twice.
