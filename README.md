# mailnotify
Fire notifications when new emails are found in your offline mailboxes. Needs a notification service such as `dunst` to be usable.

Dependencies: `inotifywait`, `notify-send`

Should be POSIX compliant and work in most shells (tested in `dash`)

## Installation
Copy or symlink to bin folder of your choice

## Usage
`mailnotify <DIR_TO_WATCH> <SUBDIR_TO_EXCLUDE_1> <SUBDIR_TO_EXCLUDE_2> ...`

Directory that should be watched for new emails may hold multiple accounts. Specify one additional argument per subdirectory that should be excluded, e.g. "Trash", "Sent", "Read Later", etc.

`Example: mailnotify ~/.local/share/mail Trash Sent 'Read Later'`

## Known Issues
As of now there is no mechanism to differentiate between newly arrived emails and those that have been moved to the `new` folder after being read before. So if `toggle-new` is called on old mails with `mutt` and `sync-mailbox` is called, a notification will be fired as well. 

Possible future fix: Only listen to `create` event with inotify, not `moved_to`. Figure out where new mails are initially created before moved to `new` folder (tmp folder? any side effects to this approach?).
