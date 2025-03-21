# ZSH native configurations without Oh My Zsh!

[![Watch the video](./assets/ZSH%20Thumb.png)](https://youtu.be/Lik1bsq8RpI)

### ZSH dot files

| File         | Usage                                                       |
| ------------ | ----------------------------------------------------------- |
| .zshenv      | Contains user’s environment variables                       |
| .zprofile    | Used to execute commands just after logging in              |
| .zshrc       | Used for the shell configuration and for executing commands |
| .zlogin      | Like .zprofile, but runs just after .zshrc                  |
| .zsh_history | History file                                                |

### .zshenv

```sh
#.zshenv

# Default configurations directory ~/.config directory
export XDG_CONFIG_HOME="$HOME/.config"
# Default cache directory ~/.cache directory
export XDG_CACHE_HOME="$HOME/.cache"
# ZSH default config directory ~/.config/zsh/
export ZDOTDIR="$XDG_CONFIG_HOME/zsh"
# ZSH history file path
export HISTFILE="$HOME/.cache/.zsh_history"
# ZSH number of history commands stored in memory (current session)
export HISTSIZE=10000
# ZSH number of history commands saved to disk (`HISTFILE`) after session ends
export SAVEHIST=10000
# Ignore theses commands from history
export HISTIGNORE="exit:clear"
# Set KEYTIMEOUT if bindkey -v this makes the switch between vi modes INSERT and NORMAL quicker
# export KEYTIMEOUT=1
# CLI-based minimal editing
export EDITOR="vim"
# GUI/full-screen editing
export VISUAL="vim"
```

### .zshrc

```sh
# .zshrc

# Completion official documentations
# https://zsh.sourceforge.io/Doc/Release/Completion-System.html#Completion-System
# Enable autocomplete and loads a function only when needed instead of at startup
autoload -Uz compinit
# faster Zsh startup by caching auto completion
compinit -d "$XDG_CACHE_HOME/zsh/.zcompdump"

# Use cache for faster autocomplete suggestions
zstyle ':completion:*' use-cache on
# Ensures that Zsh automatically refreshes its command cache when using tab completion for executables
zstyle ':completion:*' cache-path "$XDG_CACHE_HOME/zsh/.zcompdump"

# Sync other sessions with installed or updated plugins
zstyle ':completion:*' rehash true

# Allow menu selection
zstyle ':completion:*' menu select

# Files and directories are sorted by modification time, newest first instead of alphabetical order
zstyle ':completion:*' file-sort modification

# case senstive correction and complete partial words
zstyle ':completion:*' matcher-list '' 'm:{a-zA-Z}={A-Za-z}' 'r:|[._-]=* r:|=*' 'l:|=* r:|=*'

# -----------
# OPTIONS
# https://zsh.sourceforge.io/Doc/Release/Options.html#Options
# -----------
# Spelling correction
setopt CORRECT
# Remove duplicate commands from history
setopt HIST_IGNORE_ALL_DUPS
# Remove duplicate commands
setopt HIST_SAVE_NO_DUPS
#By default, Zsh overwrites the history file when closing a session. To append new history instead Prevent history loss when multiple terminal sessions are open
setopt APPEND_HISTORY
# By default each terminal has it's own history this shares all history across all terminals
setopt SHARE_HISTORY
# Ignores commands start with space from history
setopt HIST_IGNORE_SPACE

# -----------
# ALIASES
# -----------
# [[ -f "$ZDOTDIR/aliases" ]] && source "$ZDOTDIR/aliases"
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias rm='rm -rf -i'
alias v='vim'
alias ll='ls -la --color=auto'
alias gst='git status'
alias vsc='code .'
# Reloads zsh configuration
alias zreload='source ~/.config/zsh/.zshrc && echo "🔄 Zsh reloaded!"'

# -----------
# KEYBINDING
# -----------
# Activate vim mode
bindkey -v
bindkey -s '^o' 'code ~/Desktop/zsh\n'

# -----------
# PROMPTs
# https://zsh.sourceforge.io/Doc/Release/Prompt-Expansion.html#Prompt-Expansion
# -----------
# Left prompt
PROMPT='%F{blue} %1~: %f '

# Right prompt
RPROMPT='%K{blue}%F{red} %D%f%k'

# Styling
# %B  %b  #Bold
# %U  %u  # Underline
# %S  %s  #Highlight
# %F{color}   %f  #Foreground color
# %K{color}   %k  #Background color

# -----------
# PLUGINS
# -----------

# syntax highlighting
[[ -f "$ZDOTDIR/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" ]] && source "$ZDOTDIR/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh"

# autosuggestions
[[ -f "$ZDOTDIR/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" ]] && source "$ZDOTDIR/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh"

```
