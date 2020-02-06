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

Directory that should be watched for new emails may hold multiple email accounts. Specify one additional argument per subdirectory that should be excluded, e.g. for "Trash", "Sent", "Read Later", "[Gmail]/Sent Items" etc. The `[` Character (and possibly more) must be escaped.

## Example: 
```
mailnotify \
    -e Trash \ 
    -e Sent \
    -e 'Read Later' \
    -e '\[Gmail\]/Sent Items' \
    ~/.local/share/mail
```

## Systemd unit
To run mailnotify as a systemd service, the executable `mailnotify-run` is used. This script is a wrapper for mailnotify and should be run it with the desired options. 

First create a shell script named `mailnotify-run`. The unit file's `ExecStart` expects the binaries to sit at `~/.local/bin`, so change accordingly if necessary. Also, if the path to the binaries is not in the unit files' `Environment` option, the path must be added there as well.

Copy or symlink `mailnotify.service` to `~/.config/systemd/user/` and run `systemctl --user enable mailnotify.service && systemctl --user start mailnotify.service`. 
