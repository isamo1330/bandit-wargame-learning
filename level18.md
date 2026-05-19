# Level 17 → 18

## Objective
There are two files in the home directory: `passwords.old` and `passwords.new`. The password for the next level is in `passwords.new` and is the only line that has been changed between the two files.

## Connection
```bash
ssh bandit17@bandit.labs.overthewire.org -p 2220
```
Using the RSA private key obtained from level 16 → 17.

## Solution

### Step 1 — List files in the home directory
After logging in with the SSH key from the previous level:

```bash
ls
```

Two files are present: `passwords.old` and `passwords.new`.

### Step 2 — Compare the files with diff
The `diff` command compares files line by line and outputs only the lines that differ:

```bash
diff passwords.old passwords.new
```

The output shows one changed line (line 42), with `<` indicating the old line and `>` indicating the new line. The `>` line is the password for bandit18.

## Password Found
`hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

## What I Learned
- `diff` compares two files line by line and shows only the differences
- The `<` symbol represents lines from the first file, `>` represents lines from the second file
- The notation `42c42` means line 42 in the first file was changed to line 42 in the second file
- When two files are nearly identical, `diff` is the quickest way to spot the change

## Screenshots
*Screenshots to be added.*
