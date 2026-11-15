fix corrupted ~.zsh kali terminal history

1. Back up your corrupted history file
```
cp ~/.zsh_history ~/.zsh_history.bak
```

2. Attempt to recover the history
```
strings ~/.zsh_history.bak > ~/.zsh_history
```

This extracts readable strings from the corrupted file and writes them into a fresh history file. Note: This can recover most readable commands, but may lose timestamps and other history metadata.

3. Fix permissions
```
chmod 600 ~/.zsh_history
```

4. Reload Zsh
```
exec zsh
```

5. Verify
```
history | tail -20
```

Close your terminal, reopen it, and press the Up arrow to see whether your commands persist.

6. Optional: Enable shared history across terminal tabs
Your output shows:
sharehistory off
incappendhistory off

You can enable both by adding these lines to ~/.zshrc:
```
setopt APPEND_HISTORY
setopt INC_APPEND_HISTORY
setopt SHARE_HISTORY
```

Then reload:
```
source ~/.zshrc
```

