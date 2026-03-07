# Syscall Calling Convention

## Register Usage by Architecture

| Arch       | Syscall NR | Return | arg0 | arg1 | arg2 | arg3 | arg4 | arg5 |
| ---------- | ---------- | ------ | ---- | ---- | ---- | ---- | ---- | ---- |
| **arm**    | r7         | r0     | r0   | r1   | r2   | r3   | r4   | r5   |
| **arm64**  | x8         | x0     | x0   | x1   | x2   | x3   | x4   | x5   |
| **x86**    | eax        | eax    | ebx  | ecx  | edx  | esi  | edi  | ebp  |
| **x86_64** | rax        | rax    | rdi  | rsi  | rdx  | r10  | r8   | r9   |

---

## Syscall Instruction

| Arch   | Instruction |
| ------ | ----------- |
| arm    | `svc #0`    |
| arm64  | `svc #0`    |
| x86    | `int 0x80`  |
| x86_64 | `syscall`   |

---

# Somes Syscalls (linux focus)

Full list + args : https://www.chromium.org/chromium-os/developer-library/reference/linux-constants/syscalls/#x86_64-64-bit

## 📌 Process & Control

| Syscall      | NR  | Description                        |
| ------------ | --- | ---------------------------------- |
| `exit`       | 60  | Terminate process                  |
| `exit_group` | 231 | Terminate all threads              |
| `fork`       | 57  | Create process                     |
| `vfork`      | 58  | Fork without copying address space |
| `clone`      | 56  | Low-level thread/process creation  |
| `execve`     | 59  | Execute a program                  |
| `wait4`      | 61  | Wait for process state change      |
| `getpid`     | 39  | Get process ID                     |
| `getppid`    | 110 | Get parent PID                     |


## 📂 File & I/O

| Syscall  | NR  | Description                  |
| -------- | --- | ---------------------------- |
| `read`   | 0   | Read from file descriptor    |
| `write`  | 1   | Write to file descriptor     |
| `open`   | 2   | Open file                    |
| `openat` | 257 | Open file relative to fd     |
| `close`  | 3   | Close file descriptor        |
| `lseek`  | 8   | Move file offset             |
| `stat`   | 4   | Get file info                |
| `fstat`  | 5   | Get file info (fd)           |
| `access` | 21  | Check permissions            |
| `dup`    | 32  | Duplicate fd                 |
| `dup2`   | 33  | Duplicate fd to fixed number |


## 🧠 Memory Management

| Syscall    | NR | Description              |
| ---------- | -- | ------------------------ |
| `brk`      | 12 | Change heap end          |
| `mmap`     | 9  | Map memory               |
| `munmap`   | 11 | Unmap memory             |
| `mprotect` | 10 | Change memory protection |
| `madvise`  | 28 | Memory usage hints       |


## 🔁 Signals & Timing

| Syscall        | NR | Description                     |
| -------------- | -- | ------------------------------- |
| `kill`         | 62 | Send signal                     |
| `rt_sigaction` | 13 | Install signal handler          |
| `rt_sigreturn` | 15 | Return from signal              |
| `nanosleep`    | 35 | Sleep with nanosecond precision |
| `alarm`        | 37 | Schedule SIGALRM                |


## 🌐 Networking (minimal set)

| Syscall    | NR | Description            |
| ---------- | -- | ---------------------- |
| `socket`   | 41 | Create socket          |
| `bind`     | 49 | Bind socket            |
| `listen`   | 50 | Listen for connections |
| `accept`   | 43 | Accept connection      |
| `connect`  | 42 | Connect socket         |
| `sendto`   | 44 | Send data              |
| `recvfrom` | 45 | Receive data           |
| `shutdown` | 48 | Shutdown socket        |


## 🧵 Threads & Synchronization

| Syscall           | NR  | Description          |
| ----------------- | --- | -------------------- |
| `futex`           | 202 | Fast userspace mutex |
| `set_tid_address` | 218 | Thread ID handling   |
| `sched_yield`     | 24  | Yield CPU            |


## 🧰 System Info / Misc

| Syscall         | NR  | Description                   |
| --------------- | --- | ----------------------------- |
| `uname`         | 63  | System information            |
| `gettimeofday`  | 96  | Current time                  |
| `clock_gettime` | 228 | High-resolution time          |
| `prctl`         | 157 | Process control               |
| `arch_prctl`    | 158 | Architecture-specific control |


