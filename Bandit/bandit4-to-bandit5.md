# Bandit Level 4 → Level 5

### Challenge

The password for `bandit5` is in the only human-readable file inside `/home/bandit4/inhere`. The directory contains ten files named `-file00` through `-file09`, most holding binary data, and all starting with `-`.

### Walkthrough

1.  Log in to the server as `bandit4` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit4@bandit.labs.overthewire.org -p 2220
    ```

2.  Move into `inhere` and inspect the type of every file with `file ./*` (prefixing `./` prevents `file` from reading the leading `-` as an option):

    ```
    cd inhere
    file ./*
    ```

    ```
    ./-file00: data
    ./-file01: data
    ./-file02: Non-ISO extended-ASCII text, with NEL line terminators, with escape sequences
    ./-file03: data
    ./-file04: data
    ./-file05: data
    ./-file06: data
    ./-file07: ASCII text
    ./-file08: data
    ./-file09: Non-ISO extended-ASCII text, with no line terminators
    ```

    Only `-file07` is plain `ASCII text`.

3.  Print `./-file07` with `cat`:

    ```
    cat ./-file07
    ```

    ```
    6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
    ```

---

### Credentials Found

- **username:** `bandit5`
- **Password:** `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`
