#### Start a new Tmux session
```
tmux new -s setup
```
Once in the session type [Ctrl] + [B] and then [Shift] + [I], to install plugin.

Start logging with [Ctrl] + [B] and [Shift] + [P]

Split panes vertically with [ Ctrl] + [B] and [Shift] + [%]  or [Shift] + ["] to split horizontally.

Move from pane to pane with [Ctrl] + [B] + [o], finally we can clear the pane history with [Ctrl] + [B] followed by [Alt] + [c]

#### How to setup tmux
To easily setup tmux logging on Kali Linux, the most efficient method is using the tmux-logging plugin via the Tmux Plugin Manager (TPM). 

First, install TPM and the logging plugin by adding the following lines to your ~/.tmux.conf:
```
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-logging'

# Initialize TMUX plugin manager (keep this line at the very bottom)
run '~/.tmux/plugins/tpm/tpm'   
```

After saving the config, press Prefix + I (default Ctrl-a + I) in an active tmux session to install the plugins.  You can then toggle logging for the current pane using Prefix + Shift + P. 

Alternatively, for a quick, plugin-free setup, add this line to ~/.tmux.conf to log the current window to a file:
```
bind-key H pipe-pane -o "exec cat >>$HOME/'#W-tmux.log'" \; display-message 'Toggled logging to $HOME/#W-tmux.log'   
```

This binds the Prefix + H key combination to start/stop logging automatically. 

### How to check if tmux plugin manager (TPM) is installed
Check the Directory Run the following command in your terminal:
```
ls ~/.tmux/plugins/tpm
```

If the directory and its contents (such as bin/ and scripts/) are listed, TPM is installed. If the directory does not exist, TPM is not installed. 

Test Key Bindings If TPM is installed, the following key bindings should be active in your tmux session:

Prefix + I: Install plugins
Prefix + U: Update plugins
Prefix + Alt + u: Remove/uninstall plugins

If the directory is missing or the key bindings do not work, you may need to install TPM by cloning the repository:
```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm   
```

### How to Start a new Tmux session
To start a new tmux session, use the tmux new command (or its alias tmux new-session) directly in your shell.  This creates a session with a default numeric name (e.g., 0) and attaches to it immediately. 

For better management, especially with multiple sessions, it is recommended to name your session using the -s flag:
```
tmux new -s mysession   
```

Key Options for Starting Sessions
Named Session: tmux new -s name creates and attaches to a session named name. 
Detached Session: tmux new -d -s name creates a session in the background without attaching. 
Create or Attach: tmux new -As name creates a new session if it doesn't exist, or attaches to the existing one if it does. 
Specific Directory: tmux new -s name -c ~/path/to/dir starts the session in a specific working directory. 
Named Window: tmux new -s name -n windowname creates a session with a specific initial window name. 
Once inside, you can detach from the session using the prefix key (Ctrl+b) followed by d, and later reattach using tmux attach -t mysession.

Once the plugin is installed, start logging the current session (or pane) by typing `[Ctrl] + [B]` followed by `[Shift] + [P]` to begin logging.



