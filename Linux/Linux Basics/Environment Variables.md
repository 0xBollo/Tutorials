# Environment Variables

Environment variables provide programs with information about the environment in which they are executed. These variables store data such as paths to system files, configuration options, language or character encoding settings, user settings and more.

## Shell Variables vs. Environment Variables

**Shell variables** apply only to the current shell instance and are not passed on to child processes.
```bash
myShellVar='Hello World!'

# Access within the current shell
echo $myShellVar # output: Hello World!

# Access within a child process
bash -c 'echo $myShellVar' # output is empty    
```
**Environment variables**, on the other hand, are also passed on to all child processes.
```bash
export myEnvVar='Hello World!'

# Access within the current shell
echo $myEnvVar # output: Hello World!

# Access within a child process
bash -c 'echo $myEnvVar' # output: Hello World!
```

## Set Environment Variables

### Temporary Environment Variables
Environment variables can be set with the shell builtin command `export`. 
```bash
export myEnvVar='Hello World!'
```
If an environment variable is not defined in one of the dedicated configuration files (such as `~/.profile` or `/etc/environment`), it is only temporarily available in the current shell session.

### User Environment Variables
User environment variables apply specifically to an individual user and are only available in their sessions. They can be set in **user-specific shell startup files**.
- `~/.profile`
- `~/.bash_profile` / `~/.bash_login`
- `~/.bashrc`
- …

### System-wide Environment Variables
System environment variables apply to all users and are available system-wide. They are set in **global shell startup files**.
- `etc/profile`
- `etc/bash.bashrc`
- …

## References

Khera, G. (2023) 'How to Set and Unset Local, User and System Wide Environment Variables in Linux', Tecmint: Linux Howtos, Tutorials & Guides, available at: https://www.tecmint.com/set-unset-environment-variables-in-linux/.

Linuxize: Linux Tips, Tricks and Tutorials (2021) 'How to Set and List Environment Variables in Linux', available at: https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/.
