# mailnotify
Fire notifications when new emails are found in your offline mailboxes. Needs a notification service such as `dunst` to be usable.

Dependencies: `inotifywait`, `notify-send`

Should be POSIX compliant and work in most shells (tested in `dash`)

## Installation
Copy or symlink all sh scripts to bin folder of your choice (names must be kept the same).

## Usage
```
mailnotify [OPTION]... [DIR_TO_WATCH]

    Options:
      -e, --exclude-dir       Directory to exclude from watching. Mail files
                              created in this directory will not trigger a
                              notification. May be applied multiple times for
                              multiple directories.

```

Directory that should be watched for new emails may hold multiple accounts. Specify one additional argument per subdirectory that should be excluded, e.g. for "Trash", "Sent", "Read Later", "[Gmail]/Sent Items" etc. The `[` Character (and possibly more) must be escaped.

## Example: 
`mailnotify --exclude-dir Trash --exclude-dir Sent --exclude-dir 'Read Later' '\[Gmail\]/Sent Items' ~/.local/share/mail`
