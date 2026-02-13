---
title: Backup and restore database
---

## Backup


To back up your database, always use the Stash UI. Do not manually copy the database file while Stash is running.

Stash uses an SQLite database in `WAL` (Write-Ahead Logging) mode. In addition to the main `stash-go.sqlite` file, there may also be `-shm` and `-wal` files present. These files can remain even after stopping Stash. For this reason, you should never manually copy the database files as a backup method.

??? info "WAL mode"
    Learn more about `WAL` mode in SQLite [here](https://sqlite.org/wal.html){:target="_blank"}.

The **Backup** or **Download Backup** tasks are the proper way to create a backup file.

1. Go to :fontawesome-solid-gear: **Settings** > **System**.
2. Under the Application Paths heading, scroll down to **Backup directory path**.
3. Set the directory to store your backups.
4. Go to :fontawesome-solid-gear: **Settings** > **Tasks**.
5. Under the Backup heading, you will find two tasks.
6. Select either the **Backup** or **Download backup** task.

### Backing up blobs

If you have binary data stored outside the database file, you need to back it up independently. This can be done by copying the relevant folder.

1. Go to :fontawesome-solid-gear: **Settings** > **System**.
2. Under the Database heading, look for **Binary data storage type**.
3. If it's set to `Filesystem`, look below for **Binary data path**. This is the directory where your blobs are stored.
4. Use your file browser to copy the entire directory to your backup location.

## Restore

Assuming you have properly created a backup file, you can use it to restore your database if needed.

!!! info
    The restore procedure uses the default `stash-go.sqlite` filename. If you changed that when configuring Stash, adjust accordingly.

The following steps are recommended when restoring a database file:

1. Go to :fontawesome-solid-gear: **Settings** > **System**, scroll down to the Database heading, and check your **Database path** location.
1. Check what your **Binary data storage type** is set to.
2. If it's set to `Filesystem`, look below for **Binary data path** and move your backed up blobs to that location. If set to `Database`, skip this step.
3. Create a backup of the current database (optional).
4. Stop Stash.
5. In your file browser, go to the location of your database path.
6. Move or delete the `stash-go.sqlite` database file (along with the `-shm`, `-wal`, and `.journal` files if present).
7. Copy the backup file that you want to restore to `stash-go.sqlite`.
8. Make sure that you now have a `stash-go.sqlite` file and that no `-shm`, `-wal`, or `.journal` files are present.
9. Start Stash.

You should now have Stash running with a working and restored database.

## Advanced troubleshooting

If you get a "database malformed" message during upgrade or backup, that probably means the database is already corrupt. One way to get past this is to do a full export and check the error log. If there are not a lot of errors, you can then try to do a full import and get a working database with minimal losses. As the full import is destructive, proceed with caution.
For cases like this, it is better to ask for [support](/#support).