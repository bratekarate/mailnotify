# mailnotify
Fire notifications when new emails appear in your offline mailboxes. Needs a notification service such as `dunst` to be usable.

Dependencies: [`inotify-tools`](https://github.com/inotify-tools/inotify-tools)(`inotifywait`), [`libnotify`](https://github.com/GNOME/libnotify)(`notify-send`), python(module `email.header`)

**TODO**: get rid of python dependency for decoding the email header. Seems to be non-trivial with awk or sed. Since python 3 is usually installed on most systems, it's not high on the priority list.

Should be POSIX compliant and work in most shells (tested in `dash`, `bash` and `zsh`)

## Installation
Copy or symlink all sh scripts to `bin` directory of your choice (names must be kept the same).

When using the systemd unit file, the choice of `bin` directory matters. See section [Systemd unit](#systemd-unit) for further instructions.

## Usage
```
mailnotify [OPTION]... [DIR_TO_WATCH]

    Options:
      -e, --exclude-dir       Directory to exclude from watching. Mail files
                              created in this directory will not trigger a
                              notification. May be applied multiple times for
                              multiple directories.

```

Directory that should be watched for new emails may hold multiple email accounts. Specify one additional argument per subdirectory that should be excluded, e.g. for `Trash`, `Sent`, `Read Later`, `[Gmail]/Sent Items` etc.

## Example
```
mailnotify \
    -e Trash \ 
    -e Sent \
    -e 'Read Later' \
    -e '[Gmail]/Sent Items' \
    ~/.local/share/mail
```

## Systemd unit
To run mailnotify as a systemd service, the executable `mailnotify-run` is used. This script is a wrapper for mailnotify and should be run it with the desired options. 

First create a shell script named `mailnotify-run`. The unit file's `ExecStart` expects the script to sit at `~/.local/bin/mailnotify-run`, so change the path accordingly if necessary. Also, if the path to the binaries is not in the unit file's `Environment` option, the path must be added there as well.

Copy or symlink `mailnotify.service` to `~/.config/systemd/user/` and run `systemctl --user enable mailnotify.service && systemctl --user start mailnotify.service`. 

## Limitations

- Multiple recipients can not be included in the notification. The string may be malformed in this case.
- HTML content will be rendered as-is and may result in unreadable notifications.

Ideas and/or PRs to address these limitations are always welcome.
