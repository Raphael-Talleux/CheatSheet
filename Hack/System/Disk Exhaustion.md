## Disk Exhaustion Attack

### Core Idea

> **Filling the disk prevents programs from creating files and breaks the system.**

---

### Key Tool: `yes`

* Outputs text **forever**
* Extremely fast
* Commonly used to auto-confirm prompts
* Can be abused to **fill disk space**

---

### Attack Pattern (CTF)

1. Generate infinite output
2. Redirect it to a file
3. Disk fills up
4. File creation fails

---

### Detection

* Programs fail with:

  * `No space left on device`
* Temp files cannot be created
* System behaves erratically

---

### CTF Verification Flow

1. Checker tries to create a file (e.g., 1 MB)
2. Failure = disk full → stage passed
3. Attacker deletes large file
4. Checker retries
5. Success = system restored → flag

---

### Defense

* Disk quotas
* Monitoring free space
* Log rotation
* Alerts on low disk space
