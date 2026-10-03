# 🐧 Day 1 Learning — Linux Basics

**Date:** 03-Oct-2026

---

## 1. Linux Basics

Linux is widely used for **servers, cloud infrastructure, DevOps, and web servers**.

> **Note:** The exact percentage of Linux vs. Windows web servers depends on the source and how servers are counted, so avoid treating the 8% / 60% figures as fixed numbers.

---

# 2. Basic Linux Commands

### 📁 File & Directory Commands

| Command  | Meaning                              | Example                  |
| -------- | ------------------------------------ | ------------------------ |
| `ls`     | List files and directories           | `ls`                     |
| `ls -l`  | List with detailed information       | `ls -l`                  |
| `ls -a`  | Show hidden files                    | `ls -a`                  |
| `ls -la` | Detailed list including hidden files | `ls -la`                 |
| `pwd`    | Print working directory              | `pwd`                    |
| `cd`     | Change directory                     | `cd /home`               |
| `cd ..`  | Go to parent directory               | `cd ..`                  |
| `cd ~`   | Go to user's home directory          | `cd ~`                   |
| `mkdir`  | Create a directory                   | `mkdir projects`         |
| `touch`  | Create an empty file                 | `touch test.txt`         |
| `cp`     | Copy a file/directory                | `cp test.txt backup.txt` |
| `mv`     | Move or rename a file/directory      | `mv old.txt new.txt`     |
| `rm`     | Remove a file                        | `rm test.txt`            |

### Important

Linux does not normally have a separate `rename` command for simple file renaming.

We use:

```bash
mv oldname.txt newname.txt
```

`mv` can therefore mean:

```text
mv → Move
mv → Rename
```

---

# 3. Viewing Files

| Command | Meaning                  | Example         |
| ------- | ------------------------ | --------------- |
| `cat`   | Display file contents    | `cat test.txt`  |
| `head`  | Show beginning of a file | `head test.txt` |
| `tail`  | Show end of a file       | `tail test.txt` |
| `less`  | Read a file page by page | `less test.txt` |

### Example

```bash
cat test.txt
```

Displays the complete file.

```bash
head test.txt
```

Shows the beginning of the file.

```bash
tail test.txt
```

Shows the end of the file.

For log files, this is very useful:

```bash
tail -f app.log
```

`-f` means **follow** — it continuously shows new lines being added to the file.

---

# 4. Users

### Find the current user

```bash
whoami
```

Example:

```text
rahul
```

### Get detailed information about a user

```bash
id rahul
```

Example:

```text
uid=1001(rahul) gid=1001(rahul) groups=1001(rahul),10(wheel)
```

This shows:

```text
UID    → User ID
GID    → Group ID
groups → Groups the user belongs to
```

### Find a user's groups

```bash
groups rahul
```

---

# 5. Linux Users Are Stored in `/etc/passwd`

Linux maintains user account information in:

```text
/etc/passwd
```

To see all users:

```bash
cat /etc/passwd
```

Or:

```bash
getent passwd
```

### Show only usernames

```bash
getent passwd | cut -d: -f1
```

Example:

```text
root
bin
daemon
ec2-user
rahul
```

> ❌ `sudo /etc/passwd` is not correct because `/etc/passwd` is a file, not a command.

---

# 6. Creating a User

There are different commands depending on the Linux distribution.

On Amazon Linux, a common approach is:

```bash
sudo useradd -m rahul
```

`-m` means:

> Create a home directory for the user.

So Linux creates:

```text
/home/rahul
```

You can then verify:

```bash
id rahul
```

---

# 7. Setting a User Password

To set the password for `rahul` as an administrator:

```bash
sudo passwd rahul
```

Then Linux asks:

```text
New password:
Retype new password:
```

### If you are already logged in as `rahul`

You can change your own password with:

```bash
passwd
```

---

# 8. Linux Groups

Groups are used to manage permissions for multiple users.

For example:

```text
Users
 │
 ├── rahul
 ├── amit
 └── rohit

Groups
 │
 ├── wheel
 └── developers
```

A user can belong to multiple groups.

Check:

```bash
groups rahul
```

---

# 9. `wheel` Group

On Amazon Linux, the `wheel` group is commonly used for users who should have **sudo privileges**.

Add `rahul` to the `wheel` group:

```bash
sudo usermod -aG wheel rahul
```

### Understand the command

```text
usermod → modify user
-a      → append
-G      → supplementary group
wheel   → group name
rahul   → username
```

### Verify

```bash
id rahul
```

You should see `wheel` in the groups.

For example:

```text
uid=1001(rahul) gid=1001(rahul) groups=1001(rahul),10(wheel)
```

> After adding a user to a group, log out and log back in for the new group membership to be applied to the login session.

---

# 10. Switching Users

To switch to another user:

```bash
su rahul
```

To switch with a login shell:

```bash
su - rahul
```

The `-` is useful because it loads the user's normal environment and takes you to their home directory.

You can verify:

```bash
whoami
```

---

# 11. Linux File Permissions

When you run:

```bash
ls -la
```

you may see:

```text
drwxr-xr-x  3 rc rc 4096 Oct 3 15:59 Oct2026_rahul_chauhan_Pathnex
```

The important part is:

```text
drwxr-xr-x
```

Let's divide it:

```text
d | rwx | r-x | r-x
  |     |     |
  |     |     └── Others
  |     └──────── Group
  └────────────── Owner
```

---

# 12. What Does `d` Mean?

The first character tells us the type of item:

```text
d → Directory
- → Regular file
l → Symbolic link
```

So:

```text
d
```

means this is a **directory**.

---

# 13. What Does `rwxr-xr-x` Mean?

There are three permission groups:

```text
Owner | Group | Others
```

So:

```text
rwx | r-x | r-x
```

### Owner

```text
rwx
```

The owner has:

```text
r → Read
w → Write
x → Execute
```

### Group

```text
r-x
```

The group has:

```text
r → Read
- → No write
x → Execute
```

### Others

```text
r-x
```

Other users have:

```text
r → Read
- → No write
x → Execute
```

---

# 14. Permission Numbers

Linux represents permissions using numbers:

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 4 + 2 + 1 = 7

r-x = 4 + 0 + 1 = 5

r-x = 4 + 0 + 1 = 5
```

So:

```text
rwx | r-x | r-x
 7  |  5  |  5
```

Therefore:

```text
drwxr-xr-x = 755
```

### Remember

```text
Read    → 4
Write   → 2
Execute → 1
```

Think of it as:

```text
4 + 2 + 1 = 7
```

---

# 15. `chmod` — Change Permissions

`chmod` stands for:

> **Change Mode**

Example:

```bash
chmod 755 myfolder
```

This gives:

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

So:

```text
755 = rwxr-xr-x
```

With `sudo`:

```bash
sudo chmod 755 myfolder
```

---

# 16. `chown` — Change Owner

`chown` stands for:

> **Change Owner**

Basic syntax:

```bash
chown <username> <file>
```

Example:

```bash
sudo chown rahul test.txt
```

Now `rahul` becomes the owner of `test.txt`.

### Change owner and group

```bash
sudo chown rahul:developers test.txt
```

Here:

```text
rahul       → Owner
developers  → Group
```

### Change ownership recursively

```bash
sudo chown -R rahul:developers myfolder
```

`-R` means **recursive** — apply the ownership change to the directory and everything inside it.

---

# 17. `chmod` vs `chown`

This is very important:

```text
chown → WHO owns the file?
chmod → WHAT can they do?
```

Example:

```bash
sudo chown rahul test.txt
sudo chmod 755 test.txt
```

Means:

```text
Owner       → rahul
Permissions → 755
```

---

# ⭐ Day 1 Commands to Remember

```bash
# Files & directories
ls
ls -l
ls -a
ls -la
pwd
cd
cd ..
cd ~
mkdir
touch
cp
mv
rm

# Viewing files
cat
head
tail
less

# Users
whoami
id
groups
getent passwd

# User management
sudo useradd -m rahul
sudo passwd rahul
sudo usermod -aG wheel rahul
su - rahul

# Permissions
ls -l
chmod
chown
```

## 🧠 Easy way to remember

```text
ls      → See files
pwd     → Where am I?
cd      → Move
mkdir   → Make folder
touch   → Make file
cp      → Copy
mv      → Move/Rename
rm      → Remove
cat     → Read file

whoami  → Who am I?
id      → User details
groups  → Group details

chmod   → Change permissions
chown   → Change ownership
```
