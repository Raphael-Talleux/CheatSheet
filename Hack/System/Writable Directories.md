
## Linux Permissions: Writable Directories

### Key Concept

> **File permissions protect file contents**
> **Directory permissions protect filenames and structure**

---

### File vs Directory Permissions

#### File (`-rw-r--r--`)

* `r` → read file contents
* `w` → modify file contents
* `x` → execute file

#### Directory (`drwxrwxrwx`)

* `r` → list filenames
* `w` → create, delete, rename files
* `x` → access files inside (traverse)

---

### Critical Rule

> **Write access to a directory allows deleting and replacing files inside it**

Even if you **do NOT own** the file.

---

### Why This Works

* Filenames live in the **directory**, not in the file
* `rm` removes the **directory entry**, not the file contents
* Creating a new file with the same name creates a **new inode**

---

### Security Impact

* World-writable directories are dangerous
* Attackers can:

  * Delete sensitive files
  * Replace config files (`.bashrc`, `.profile`)
  * Hijack binaries via PATH

---

### Common Exploitation Pattern

1. Directory is world-writable
2. Attacker deletes victim’s file
3. Attacker recreates it with malicious content
4. Victim executes attacker-controlled code

---

### Defense

* Never make home directories world-writable
* Use the **sticky bit** (`+t`) on shared directories (e.g. `/tmp`)
* Audit permissions on startup files

---

### Takeaway

> **Writable directory = control over filenames inside it**
> Ownership of the file does not matter.

