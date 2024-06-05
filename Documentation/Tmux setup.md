```sh
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
touch .tmux.conf
```
```sh
echo "# List of plugins

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-logging'

# Initialize TMUX plugin manager (keep at bottom)
run '~/.tmux/plugins/tpm/tpm'" > .tmux.conf
```
```sh
tmux source ~/.tmux.conf 
```

`prefix + Shift + I` - Install plugins
`prefix + Shift + P` - start/stop loggging
`prefix + Alt + Shift + P ` - capture entire pane
`prefix + Alt + P` - capture current screen