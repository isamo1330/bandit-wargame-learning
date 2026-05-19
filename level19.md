# Level 18 → 19

## Objective
The password for the next level is stored in a file called `readme` in the home directory. However, the `.bashrc` has been modified to log you out immediately when you log in with SSH.

## Connection
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```
Password: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

## Solution

### Step 1 — Observe the problem
Attempting a normal SSH login immediately prints `Byebye!` and closes the connection. The `.bashrc` file has been configured to force a logout on interactive login.

### Step 2 — Execute a command directly via SSH
SSH allows you to pass a command as an argument, which runs on the remote server without starting an interactive shell (and therefore without sourcing `.bashrc`):

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

This connects, executes `cat readme`, prints the password, and disconnects — bypassing the `.bashrc` logout entirely.

### Alternative approach — Force a different shell
Another option is to use the `-T` flag to disable pseudo-terminal allocation, or explicitly request `/bin/bash` to bypass the default shell setup:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 /bin/bash
```

This drops you into a shell without the normal prompt, but commands like `ls` and `cat readme` still work.

## Password Found
`awhqfNnAbc1naukrpqDYcF95h7HoMTrC`

## What I Learned
- SSH can execute a single command remotely by appending it after the connection string
- `.bashrc` runs on interactive login — bypassing the interactive shell avoids it entirely
- The `-T` flag disables pseudo-terminal allocation, which can help avoid shell configuration scripts
- There are multiple ways to work around a hostile `.bashrc`: direct command execution, alternative shells, or disabling the terminal

## Screenshots
*Screenshots to be added.*
