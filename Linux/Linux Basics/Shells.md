# Shells

## Interactive Shells vs. Non-Interactive Shells

An **interactive shell** accepts user input and returns the output to the user.

A **non-interactive shell**, on the other hand, executes a predefined sequence of commands without waiting for user input. Non-interactive shells are used, for example, when shell scripts are executed.

## Login Shell vs. Non-Login Shell

A **login shell** is started when a user logs into the system via a terminal or via SSH. When logging in via a display manager, no login shell is started. The login shell is typically the first process of a user after logging in and all other processes started by the user are child processes of the login shell. You can also explicitly start a login shell within an existing session.

A **non-login shell** is typically started when invoking a new shell within an existing session.

## Shell Startup Files

### User-defined Shell Startup Files

#### ~/.profile
`~/.profile` is sourced by **login shells** of a specific user if no shell-specific configuration file such as `~/.bash_profile` or `~/.zprofile` exists. This file is typically used to define user-specific spenvironment variables.

#### ~/.bash_profile and ~/.bash_login
`~/.bash_profile` or `~/.bash_login` is sourced by **Bash login shells** of a specific user. These files are used to define user-specific environment variables that only apply to Bash shells.

`~/.bash_profile` and `~/.bash_login` fulfill the same purpose. If `~/.bash_profile` exists, `~/.bash_login` is not sourced. So it only makes sense to have one of these files.

#### ~/.bashrc
`~/.bashrc` is sourced by **interactive non-login Bash shells**. Normally you put things in `~/.bashrc` that are not inherited by subshells (aliases, functions, …).

By default, `~/.bashrc` is explicitly sourced within `~/.profile` and is therefore also indirectly loaded by login shells.
```bash
if [ -f "$HOME/.bashrc" ]; then
    source "$HOME/.bashrc"
fi
```

### System-wide Shell Startup Files

#### /etc/profile
`/etc/profile` is sourced by all **login shells** of all users. This file is typically used to define system-wide environment variables.

#### /etc/profile.d
By default, all shell scripts within the `/etc/profile.d` directory are explicitly sourced within `/etc/profile`.
```bash
for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      source $i
    fi
done
```

#### etc/bash.bashrc
`etc/bash.bashrc` is sourced by all **interactive non-login Bash shells** of all users.

By default, `/etc/bash.bashrc` is explicitly sourced within `/etc/profile` and is therefore also indirectly loaded by login shells.
```bash
if [ -f /etc/bash.bashrc ]; then
    source /etc/bash.bashrc
fi
```
