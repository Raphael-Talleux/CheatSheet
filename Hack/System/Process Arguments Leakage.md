
## Process Arguments Leakage

### Core Idea

> **Command-line arguments are visible to other users**

Sensitive data passed as arguments can be **leaked via process listing**.

---

### Why This Is Dangerous

* `ps`, `top`, `/proc` expose process arguments
* Other local users can read them
* Passwords, tokens, flags can leak

---

### Example

```bash
ps aux
```

Output includes:

```
COMMAND
script.sh my_password
```

👉 `my_password` is exposed to anyone.

---

### Attack Pattern (CTF)

1. Victim runs a command/script with a **secret as an argument**
2. Attacker lists processes (`ps aux`)
3. Attacker extracts the secret
4. Attacker authenticates as victim (`su`)
5. Attacker abuses victim privileges (e.g. `sudo cat /flag`)

---

### Why sudo Matters

* Victim is allowed to use `sudo`
* Stolen password enables:

  * `su victim`
  * `sudo` commands
* Leads to privilege escalation

---

### Real-World Impact

* Leaked DB passwords
* Leaked API keys
* Credential theft on shared systems

---

### Defense

* Never pass secrets via CLI arguments
* Use:

  * stdin
  * environment variables (carefully)
  * protected config files
* Restrict process visibility (`hidepid`)

---

### Takeaway

> **If a secret is in the command line, it is not secret.**
