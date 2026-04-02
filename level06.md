# Level 5 → 6

## Objective
The password is stored somewhere in the `inhere` directory tree. The file has these properties:
- Human-readable
- 1033 bytes in size
- Not executable

## Connection
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Password: `4oQYVPkxZOOE0O5pTW81FB8j81xXGUQw`

## Solution
Use `find` with flags to match all three criteria at once:
```bash
find . -type f -size 1033c ! -executable
```
- `-type f` — regular file only
- `-size 1033c` — exactly 1033 bytes (`c` = bytes)
- `! -executable` — not executable

This returns `./inhere/maybehere07/.file2`. Read it with:
```bash
cat ./inhere/maybehere07/.file2
```

## Password Found
`HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

## What I Learned
- `find` is extremely powerful for locating files by properties rather than name
- `-size 1033c` uses `c` for bytes (other units: `k` = KB, `M` = MB)
- `!` negates a condition in `find`
- Combining multiple flags narrows results down to exactly one match

## Screenshots
![find command locating the file and password](screenshots/level-05-06/step-01-password.png)
