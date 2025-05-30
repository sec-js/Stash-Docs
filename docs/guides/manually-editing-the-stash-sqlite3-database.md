---
title: Manually editing the Stash sqlite3 database
---

## Location

The Stash Sqlite3 database file is located at `~/.stash/stash-go.sqlite`.

Before making changes to the Stash sqlite3 database - **please make a backup first!**

You can use the `sqlite3` client to directly edit this file.

## Opening the database file

```
cd ~/.stash
sqlite3 stash-go.sqlite
```

## Examples

### Deleting all tags

If you need to delete all tags, you can use the following commands:

```
sqlite> DELETE FROM scenes_tags;
sqlite> DELETE FROM tags;
```

!!! note
    This will not work if you have Scene marker tags.