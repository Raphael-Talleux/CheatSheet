### Command (PATH) Hijacking

**What**
- Execute a malicious command by abusing the `PATH` lookup order.

**Why it works**
- Program calls a command without absolute path (e.g. `ls`)
- Attacker controls a directory earlier in `PATH`

**Requirements**
- Command called without full path
- Writable directory in `PATH`
- Target runs with higher privileges (SUID, sudo, cron, service)

**Impact**
- Arbitrary command execution
- Privilege escalation

**Example**
- Vulnerable call: `system("ls")`
- Hijack: create fake `ls` in attacker-controlled PATH directory

**Defense**
- Use absolute paths (`/bin/ls`)
- Sanitize PATH (`/usr/bin:/bin`)
- Clean environment in privileged programs
