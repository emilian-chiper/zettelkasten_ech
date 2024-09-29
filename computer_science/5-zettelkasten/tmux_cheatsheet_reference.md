### Meta
2024-09-26 22:43
**Tags:**
**Status:** #pending 

### Sessions
**Start a new session**
```BASH title:start_new_session.sh
tmux
tmux new
tmux new-session
```

**Start a new session or attach to an existing session named *mysession*.**
```BASH title:example.sh
tmux new-session -A -s mysession
```

**Start a new session with the name *mysession*.**
```BASH title:example.sh
tmux new -s mysession
```
or
`:new -s mysession`

**Kill/delete the current session**
`:kill-session`

**Kill/delete session *mysession*.**
```BASH
tmux kill-ses -t mysession
tmux kill-session -t mysession
```

**Kill/delete all sessions but the current**
```BASH title:example.sh
tmux kill-session -a
```

**Kill/delete all sessions but *mysession*.**
```BASH title:example.sh
tmux kill-session -a -t mysession
```

**Rename session**
`Ctrl` + `b` `$`

**Detach from session**
`Ctrl` + `b` + `d`

**Detach others on the session (Maximize window by detach other clients)**
`:attach -d`

Show all sessions
```BASH title:example.sh
tmux ls
tmux list-sessions
```
or
`Ctrl` + `b` + `s`

**Attach to last session**
```BASH title:example.sh
tmux a
tmux at
tmux attach
tmux attach-session
```

**Attach to a session with the name *mysession***
```BASH title:example.sh
tmux a -t mysession
tmux at -t mysession
tmux attach -t mysesssion
tmux attach-session -t mysession
```

**Session and window preview**
`Ctrl` + `b` `w`

**Move to previous session**
`Ctrl` + `b` `(`

**Move to next session**
`Ctrl` + `b` `)`

### Windows
**Start a new session with the name *mysession* and window *mywindow***
```BASH title:example.sh
tmux new -s mysession -n mywindow
```

**Create window**
`Ctrl` + `b` `c`

**Rename current window**
`Ctrl` + `b` `,`

**Close current window**
`Ctrl` + `b` `&`

**List windows**
`Ctrl` + `b` `w`

**Previous window**
`Ctrl` + `b` `p`

**Next window**
`Ctrl` + `b` `n`

**Switch/select window by number**
`Ctrl` + `b` `0`…`9`

**Toggle last active window**
`Ctrl` + `b` `l`

**Reorder window, swap window number 2(src) and 1(dst)**
`:swap-window -s 2 -t 1`

**Move current window to the left by one position**
`:swap-window -t -1`

**Move window from source to target**
`:move-window -s src_ses:win -t target_ses:win`
`:movew -s foo:0 -t bar:9`
`:movew -s 0:0 -t 1:9`

**Reposition window in the current session**
`:move-window -s src_session:src_window`
`:movew -s 0:9`

**Renumber windows to remove gap in the sequence**
`:move-window -r`
`:movew -r`

### Panes
**Toggle last active pane**
`Ctrl` + `b` `;`

**Split the current pane with a vertical line to create a horizontal layout**
`:spint-window -h`
`Ctrl` + `b` `%`

**Split the current with a horizontal line to create a vertical layout**
`:split-window -v`
`Ctrl` + `b` `"`

**Join two windows as panes (Merge window 2 to window 1 as panes)**
`:join-pane -s 2 -t 1`

**Move pane from one window to another (Move pane 1 from window 2 to pane after 0 of window 1)**
`:join-pane -s 2.1 -t 1.0`

**Move the current pane left**
`Ctrl` + `b` `{`

**Move the current pane right**
`Ctrl` + `b` `}`

**Switch pane to the direction**
`Ctrl` + `b` `↑`
`Ctrl` + `b` `↓`
`Ctrl` + `b` `→`
`Ctrl` + `b` `←`

**Toggle synchronize-panes (send command to all panes)**
`:setw synchronize-panes`

**Toggle between pane layouts**
`Ctrl` + `b` `Spacebar`

**Switch to next pane**
`Ctrl` + `b` `o`

**Show pane numbers**
`Ctrl` + `b` `q`

**Switch/select pane by numeber**
`Ctrl` + `b` `q` `0`…`9`

**Toggle pane zoom**
`Ctrl` + `b` `z`

**Convert pane into a window**
`Ctrl` + `b` `!`

**Resize current pane height (holding second key is optional)**
`Ctrl` + `b` + `↑`
`Ctrl` + `b` `Ctrl` + `↑`
`Ctrl` + `b` + `↓`
`Ctrl` + `b` `Ctrl` + `↓`

**Resize current pane width (holding second key is optional)**
`Ctrl` + `b` + `→`
`Ctrl` + `b` `Ctrl` + `→`
`Ctrl` + `b` + `←`
`Ctrl` + `b` `Ctrl` + `←`

**Close current pane**
`Ctrl` + `b` `x`

### Copy mode
**Use vi keys in buffer**
`:setw -g mode-keys vi`

**Enter copy mode**
`Ctrl` + `b` `[`

**Enter copy mode and scroll one page up**
`Ctrl` + `b` `PgUp`

**Quit mode**
`q`

**Go to top line**
`g`

**Go to bottom line**
`G`

**Scroll up**
`↑`

**Scroll down**
`↓`

**Move cursor left**
`h`

**Move cursor down**
`j`

**Move cursor up**
`k`

**Move cursor right**
`l`

**Move cursor forward one word at a time**
`w`

**Move cursor backward one word at a time**
`b`

**Search forward**
`/`

**Search backward**
`?`

**Next keyword occurrence**
`n`

**Previous keyword occurrence**
`N`

**Start selection**
`Spacebar`

**Clear selection**
`Esc`

**Copy selection**
`Enter`

**Paste contents of buffer_0**
`Ctrl` + `b` `]`

**Display buffer_0 contents**
`:show-buffer`

**Copy entire visible contents of pane to a buffer**
`:capture-pane`

**Show all buffers**
`:list-buffers`

**Show all buffers and paste selected**
`:choose-buffer`

**Save buffer contents to *buf.txt***
`:save-buffer buf.txt`

**Delete buffer_1**
`:delete-buffer -b 1`

### Misc
**Enter command mode**
`Ctrl` + `b` `:`

**Set OPTION for all sessions**
`:set -g OPTION`

**Set OPTION for all windows**
`:setw -g OPTION`

**Enable mouse mode**
`:set mouse on`

### Help
**List key bindings (shortcuts)**
```BASH title:example.sh
tmux list-keys
```
or
`:list-keys`
**0**
**Show every session, window, pane, etc**
```BASH title: example.sh
tmux info
```