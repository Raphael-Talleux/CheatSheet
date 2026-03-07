# Syscalls Memo

## `exit` syscall

- **Purpose:** Terminate the program with an exit code.
- **Syscall number:** 60  
- **Arguments:**  
  - `rdi` → exit code (integer)  

### Example:

```asm
SYS_EXIT equ 60

mov rax, SYS_EXIT   ; syscall number for exit
mov rdi, 0          ; exit code 0
syscall
```

---

## `write` syscall

* **Purpose:** Write data to a file descriptor (stdout, stderr, file, etc.)
* **Syscall number:** 1
* **Arguments:**

  * `rdi` → file descriptor (1 = stdout, 2 = stderr)
  * `rsi` → pointer to buffer (data to write)
  * `rdx` → length of buffer (in bytes)

### Example:

```asm
SYS_WRITE equ 1
STDOUT    equ 1

mov rax, SYS_WRITE   ; syscall number for write
mov rdi, STDOUT      ; file descriptor
mov rsi, msg         ; pointer to message
mov rdx, len         ; length of message
syscall
```


## `read` syscall

* **Purpose:** Lire des données depuis un descripteur de fichier (stdin, fichier, etc.)

* **Syscall number:** 0

* **Arguments:**

  * `rdi` → file descriptor (0 = stdin)
  * `rsi` → pointeur vers le buffer (où stocker les données lues)
  * `rdx` → nombre maximum d’octets à lire

* **Return value:**

  * `rax` → nombre d’octets effectivement lus (0 = EOF, < 0 = erreur)

### Exemple :

```asm
SYS_READ equ 0
STDIN   equ 0

mov rax, SYS_READ    ; syscall number for read
mov rdi, STDIN       ; file descriptor (stdin)
mov rsi, buffer      ; pointer to buffer
mov rdx, 100         ; max number of bytes to read
syscall
```
