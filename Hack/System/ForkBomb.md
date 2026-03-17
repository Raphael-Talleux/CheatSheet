## Fork Bomb

### What It Is

> A **fork bomb** is a program that recursively creates new processes until the system can no longer create any.

---

### Core Mechanism

* Each process **spawns more processes**
* Growth is **exponential**
* Process table fills up
* `fork()` fails → no new processes can start

---

### Fork Bomb vs Infinite Loop

| Infinite Loop | Fork Bomb               |
| ------------- | ----------------------- |
| 1 process     | Thousands of processes  |
| High CPU      | Exhausts process limits |
| System usable | System unusable         |

---

### Why It Breaks the System

* Kernel has a **max process limit**
* Too many processes → resource exhaustion
* New shells / commands fail to start

---

### CTF Pattern

1. Launch a **monitor/check** process first
2. Trigger the fork bomb in another shell
3. Checker observes process creation failure
4. Flag is awarded

---

### Security Impact

* Denial of Service (DoS)
* Affects all users on the system
* No privileges required

---

### Defense

* Use `ulimit -u`
* Limit processes per user
* Container isolation
* Never run untrusted scripts

---

### Takeaway

> **Fork bombs kill systems by exhausting process creation, not by looping.**
