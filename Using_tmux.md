# Using `tmux`

full guide: [link](https://wiki.rc.hms.harvard.edu/pages/viewpage.action?pageId=20676872)

author: Joshua Cook  
date: 2018-11-06  


## Main Commands

| Command | Meaning |
|---------|---------|
| `tmux new -s work` | create a new session called "work" |
| `Ctrl+b` then `c` | add a window to a session |
| `Ctrl+b` then `1` | switch to window 1 (or any other number |
| `Ctrl+b` then `%` | add a pane to a window |
| `Ctrl+b` then `o` | switch panes in the same window |
| `Ctrl+b` then `d` | detach a session |
| `tmux attach -t work` | re-attach to session "work" |
| `tmux a` | re-attach last session |
| `Ctrl+d` | kill a pane, window, or session |


## Use

Login to O2, note the login node number, and create a new `tmux` session using `tmux new -s project1`. Add a window by typing `Ctrl+b` (together) then `c` ("`c`reate"). To log out, detach from the `tmux` session using `Ctrl+b` then `d` ("`d`etach"). When you want to return, login into O2. If you don't land on the original login node,  `ssh` to that node using `ssh login01`. Then use `tmux a` to re-`a`ttach the last session or `tmux attach -t project1` to attach the session named `project1`.

To use multiple panes in one terminal window, use the command `Ctrl+b` then `%`. To switch between the panes, use `Ctrl+b` then `o`