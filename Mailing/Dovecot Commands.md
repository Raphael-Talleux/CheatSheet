
# Dovecot Commands


## 1. Authentication

Check if a user can log in:

```bash
doveadm auth test user@example.com
````

## 2. User Information

Show UID, GID, home directory, and mail location:

```bash
doveadm user user@example.com
```

## 3. Fetch Mail

* List all mail UIDs in a mailbox:

```bash
doveadm fetch -u user@example.com uid mailbox INBOX
```

* Show the content of mails:

```bash
doveadm fetch -u user@example.com text mailbox INBOX
```


## 4. Mailbox Management

* List mailboxes:

```bash
doveadm mailbox list -u user@example.com
```

* Create a mailbox:

```bash
doveadm mailbox create -u user@example.com NewBox
```

* Delete a mailbox:

```bash
doveadm mailbox delete -u user@example.com OldBox
```

* Rename a mailbox:

```bash
doveadm mailbox rename -u user@example.com OldBox NewBox
```


## 5. Password Testing

Check a password hash:

```bash
doveadm pw -t '{SHA512-CRYPT}$6$...'
```


## 6. Debugging

Verbose fetch with debugging:

```bash
doveadm -Dv fetch -u user@example.com text mailbox INBOX
```

Flags:

* `-D` → debug
* `-v` → verbose