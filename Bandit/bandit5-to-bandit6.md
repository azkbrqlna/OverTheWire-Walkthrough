# Bandit Level 5 → Level 6

### Challenge

The password for `bandit6` is in a file somewhere under `/home/bandit5/inhere` that is human-readable, 1033 bytes in size, and not executable.

### Walkthrough

1.  Log in to the server as `bandit5` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit5@bandit.labs.overthewire.org -p 2220
    ```

2.  Search for regular files that are exactly 1033 bytes (`c` specifies bytes in `find`):

    ```
    find . -type f -size 1033c
    ```

    ```
    ./inhere/maybehere07/.file2
    ```

    Only one file matches, and it is already non-executable (`-rw-r-----`) and plain `ASCII text`.

3.  Print the contents of `./inhere/maybehere07/.file2` with `cat`:

    ```
    cat ./inhere/maybehere07/.file2
    ```

    ```
    pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
    ```

---

### Credentials Found

- **username:** `bandit6`
- **Password:** `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`
