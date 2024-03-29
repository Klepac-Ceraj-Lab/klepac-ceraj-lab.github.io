+++
title="File Sync and Backup"
+++

# File Sync and Backup

All of the primary [lab drives](computers/) are regularly synced to the cloud using google drive
(since we have unlimited storage there).
There is a Shared Drive[^shareddrive] on google drive for backed up directories.
The content of these drives can not be accessed directly,
they are encrypted chunks of bytes.

Many sensitive files are also duplicated across physical drives on campus,
since transferring to/from the cloud is much more time-intensive
than transfers within the Wellesley network,
and this should be sufficient for most failure points
(it is unlikely that all drives will fail at the same time).

## Instructions

- If you are transferring files between lab servers,
  or between your own computer and lab servers,
  you probably want to use `rsync` - [see here](rsync).
- If you are backing up to or restoring drives from google drive, you will use `duplicity`.
  - If you have never set up sync before, [follow the instructions below](#setting_up_duplicity).
  - If you need to sync from a local drive to the cloud (eg as part of the [download and archive protocol](../download)), then [go here](backup).
  - If you need to restore a backup from the cloud to your local drive, [go here](restore).

## Setting up duplicity

`duplicty`[^duplicity] is a command-line tool that enables encrypted and incremental backup
with a number of different services, including google drive
(which is important, since we have unlimited storage on Wellesley's gdrive).

`duplicity` should already be installed on lab servers.
If you need it on your own machine,
your best bet is to use [Home Brew](http://brew.sh) (`brew install duplicity`).

### Set up google api and duplicity

There are a bunch of guides online to setting up google drive
as a backend for `duplicity`.
If you're setting up gdrive for the first time, follow the tutorial [found here][dupgdrive].
The basic procedure is

1. Make yourself an app using google developer console that has
   the ability to manage gdrive folders
   (I was able to make one that only had read/write permission on its own folders).
   More info at the link above.
2. Get the credentials, and save them in a file on your local drive.
3. Make sure to install right versions of python dependencies[^pydrive] -
   you need `httplib2` v.0.15.0 and `google-api-python-client` v1.6.
   If you're using a lab computer like `hopper` or `ada`, this should already be done.

## Next steps

- [Back up a drive to Google Drive using `duplicity`](backup)
- [Restore a drive from Google Drive using `duplicity`](restore)

## References

[^duplicity]: [Duplicity](https://gitlab.com/duplicity/duplicity) is a program for making encrypted backups. Install it with `sudo apt install duplicity` (linux) or `brew install duplicity` (mac)
[^pass]: See [this page](/drylab/pass/) for info on setting up `pass`.
[^pydrive]: https://stackoverflow.com/a/61188575/3742902
[^shareddrive]: https://drive.google.com/drive/u/1/folders/0AAFXKrJrjeBbUk9PVA

[dupgdrive]: https://rgarth.github.io/2017/10/29/Grive-and-Duplicity/