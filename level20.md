# Level 19 → 20

## Objective
Use the setuid binary in the home directory to access the password for the next level. Execute it without arguments to find out how to use it. The password is in the usual place (`/etc/bandit_pass`).

## Connection
```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```
Password: `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`

## Solution

### Step 1 — Research setuid
Started by reading the man page for setuid to understand the concept:

```bash
man setuid
```

### Step 2 — Identify the setuid binary
List the files in the home directory with full permissions:

```bash
ls -l
```

There is one file: `bandit20-do`, owned by `bandit20` with the setuid bit set (`-rwsr-x---`). The `s` in the owner's execute position means this binary runs with the privileges of its owner (bandit20), not the user who executes it (bandit19).

### Step 3 — Run the binary without arguments
```bash
./bandit20-do
```

Output: `Run a command as another user. Example: ./bandit20-do id`

### Step 4 — Read the password file
Since the binary runs commands as bandit20, and `/etc/bandit_pass/bandit20` is only readable by bandit20:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

This prints the password for bandit20.

## Password Found
`0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`

## What I Learned
- The setuid bit (`s` in permissions) allows a binary to run with the file owner's privileges, not the caller's
- `man setuid` explains how the setuid mechanism works at a system level
- `ls -l` shows the `s` flag in the owner execute position when setuid is active
- Setuid binaries are a common privilege escalation mechanism in Linux — and a common target in security assessments
- The `id` command is useful for verifying which user context a process is running under (`uid` vs `euid`)

## Screenshots
![Logged into bandit19, running man setuid to research the concept](screenshots/level-19-20/step-01.png)
*Additional screenshots to be added.*
