# Linux Permissions Cheat Sheet

A quick reference for understanding and using `chmod` and `ls -l`

---

## Permission Basics

Each file has 3 permission groups:

```
Owner | Group | Others
```

Each group can have:

- **r** = read (4)
- **w** = write (2)
- **x** = execute (1)

Add values to get numbers:

```
rwx = 7
rw- = 6
r-x = 5
r-- = 4
-wx = 3
-w- = 2
--x = 1
--- = 0
```

---

## chmod Numbers

Format:

```
chmod XYZ file
```

- X = owner
- Y = group
- Z = others

### Examples

```bash
chmod 755 script.sh   # rwxr-xr-x (executables)
chmod 644 file.txt    # rw-r--r-- (files)
chmod 700 secret.txt  # rwx------ (private)
chmod 777 open.txt    # rwxrwxrwx (unsafe)
```

---

## `ls -l` Output Explained

Example:

```bash
-rwxr-xr-- 1 user group 1234 Jun 29 file.sh
```

Breakdown:

```
[Type][Owner][Group][Others]
  1      3      3      3 chars
```

---

### File Type (1st character)

```
-  = regular file  
d  = directory  
l  = symbolic link  
b  = block device  
c  = character device
```

---

### Permissions (next 9 characters)

```
rwx r-x r--
│   │   └── others
│   └────── group
└────────── owner
```

---

### Convert to Numbers

```
rwx = 7
r-x = 5
r-- = 4
```

Example:

```
-rwxr-xr-- → 754
```

---

## Common Permission Sets

```bash
755 → rwxr-xr-x  (executables)
644 → rw-r--r--  (files)
700 → rwx------  (private)
750 → rwxr-x---  (team access)
```

---

## Quick Patterns

```
rw-r--r-- → 644
rwxr-xr-x → 755
rwx------ → 700
---       → no permissions
```

---

## Useful Tips

### Directories

- `r` → list files (`ls`)
- `w` → create/delete files
- `x` → enter directory (`cd`)

---

### Execute (`x`)

- Required to run scripts or binaries

---

### Symbolic Links

- Show as: `lrwxrwxrwx`
- Permissions are usually ignored

---

## Practice Example

```
drwxr-x---
```

- Type: directory  
- Permissions: `rwx r-x ---`  
- Number: **750**

---

## Memory Trick

```
r = 4, w = 2, x = 1 → just add them
```

```bash
600  → secrets
644  → normal files
755  → programs/scripts
700  → private stuff
750  → team-only access
```

----
## Think in questions
Ask yourself:

Who owns this?
- Just me → 6 or 7
- Shared → group matters

Should others modify it?
- No → avoid w for group/others
- Yes → very rare → think carefully

Does it need to be executed?
- Yes → add x
- No → remove it

Rule of thumb: `If it needs to be run, it needs x`
