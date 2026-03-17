
## Bashrc Backdoor

### What is `.bashrc`

* Executed **every time an interactive Bash shell starts**
* Located at: `~/.bashrc`
* Commonly used for:

  * Environment variables
  * Aliases / functions
  * Shell configuration

---

### Why Attackers Target It

* **Persistence**: runs automatically on login
* **User-level**: no root required
* **Stealthy**: users rarely inspect it
* Executes with **victim’s permissions**

---

### Common Abuse Patterns (Conceptual)

* Auto-executing hidden commands on login
* Running background processes
* Reading files the attacker can’t access directly
* Modifying PATH or aliases to hijack commands

> In CTFs, this is often used to execute something *as the victim*.

---

### Typical CTF Flow

1. Attacker gains **write access** to victim’s `~/.bashrc`
2. Victim logs in (or script simulates login)
3. `.bashrc` executes attacker-controlled logic
4. Action runs with **victim’s privileges**
5. Sensitive data (e.g. flag) becomes accessible

---

### Red Flags (Defense)

* Unexpected commands at end of `.bashrc`
* Obfuscated or base64-encoded lines
* Background execution (`&`, `nohup`)
* Network or file access on shell startup

---

### Mitigation

* Audit startup files:

  * `.bashrc`, `.bash_profile`, `.profile`
* Use file integrity monitoring
* Restrict write permissions on home directories

---

### Key Takeaway

> `.bashrc` = **automatic code execution on login**
> If you can write it, you can act *as the user* when they log in.
