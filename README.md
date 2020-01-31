# mailnotify
Fire notifications when new emails are found in your offline mail folders. 

Dependencies: `inotifywait`

Should be POSIX compliant and work in most shells (tested in `dash`)

# Installation
Copy or symlink to bin folder of your choice

# Usage
`mailnotify <DIR_TO_WATCH> <SUBDIR_TO_EXCLUDE_1> <SUBDIR_TO_EXCLUDE_2> ...`

Directory that should be watched for new emails may hold multiple accounts. Specify one additional argument per subdirectory that should be excluded, e.g. "Trash", "Sent", "Read Later", etc.

`Example: mailnotify ~/.local/share/mail Trash Sent 'Read Later'`
