# Using `tmux`

full guide: [link](https://wiki.rc.hms.harvard.edu/pages/viewpage.action?pageId=20676872)  
advanced guide: [How to Use tmux the Terminal Multiplexer](https://www.linode.com/docs/networking/ssh/persistent-terminal-sessions-with-tmux/)  

author: Joshua Cook  
date: 2018-11-06  


## Main Commands

| Command | Meaning |
|---------|---------|
| `tmux new -s work` | create a new session called "work" |
| `Ctrl+b` then `c` | add a window to a session |
| `Ctrl+b` then `1` | switch to window 1 (or any other number |
| `Ctrl+b` then `%` or `"` | split a window vertically or horizontally |
| `Ctrl+b` then `o` | switch panes in the same window |
| `Ctrl+b` then `d` | detach a session |
| `tmux attach -t work` | re-attach to session "work" |
| `tmux a` | re-attach last session |
| `Ctrl+d` | kill a pane, window, or session |


## General Use in O2

Login to O2, note the login node number, and create a new `tmux` session using `tmux new -s project1`. Add a window by typing `Ctrl+b` (together) then `c` ("`c`reate"). To log out, detach from the `tmux` session using `Ctrl+b` then `d` ("`d`etach").  

When you want to return, login into O2. If you don't land on the original login node, `ssh` to that node using `ssh login01`. Or, you can specifically `ssh` into a specific login node using `ssh jc604@login01.o2.rc.hms.harvard.edu`. Then use `tmux a` to re-`a`ttach the last session or `tmux attach -t project1` to attach the session named `project1`.  

To use multiple panes in one terminal window, use the command `Ctrl+b` then `%` or `"`. To switch between the panes, use `Ctrl+b` then `o`.

## More Commands

Shortcuts can be accessed by using the *prefix key* `Ctrl+b` followed by a single key. Command mode can also be used by `Ctrl+b` then `:` letting you enter any `tmux` commands. 

### Sessions

| Command | Meaning |
|---------|---------|
| `tmux new -s session name` | make a new session called `session_name` |
| `Ctrl+b` + `(` or `)` | switch to the previous or next session |
| `Ctrl+b` + `s` | display list of sessions |
| `tmux ls` | list all available sessions |
| `tmux a` | re-attach last session |
| `tmux attach -t session_name` | re-attach a session called `session_name` |


### Windows

| Command | Meaning |
|---------|---------|
| `Ctrl+b` + `c` | add a new window to a session |
| `Ctrl+b` + `p` | switch to previous window |
| `Ctrl+b` + `n` | switch to next window |
| `Ctrl+b` + `1` | switch to window 1 (or any other number) |
| `Ctrl+b` + `w` | choose window from a list |
| `Ctrl+b` + `&` | force-kill all processes in an unresponsive window |
| | `Ctrl+b` + `+` | rename a window |

### Panes

| Command | Meaning |
|---------|---------|
| `Ctrl+b` + `%` or `"` | split a window vertically or horizontally |
| `Ctrl+b` + `o` | to switch panes
| `Ctrl+b` + `arrow key` | navigate to a pane |
| `Ctrl+b` + `Alt+arrow key` | resize the active pane |
| `Ctrl+b` + `z` | zoom in on the active window; repeat to zoom back out |
| `Ctrl+b` + `x` | force-kill an unresponsive pane |
