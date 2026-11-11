# Bandit Level 3 → Level 4

### Challenge

The password for `bandit4` is in a hidden file inside `/home/bandit3/inhere`. On Linux, filenames starting with a dot (`.`) do not appear in a plain `ls` listing.

### Walkthrough

1.  Log in to the server as `bandit3` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit3@bandit.labs.overthewire.org -p 2220
    ```

2.  Move into the `inhere` directory and pass `-la` to `ls` so hidden files are listed:

    ```
    cd inhere
    ls -la
    ```

    A plain `ls` returns nothing here, while `ls -la` shows `...Hiding-From-You` (`-rw-r----- 1 bandit4 bandit3`).

3.  Print the contents of `...Hiding-From-You` with `cat`:

    ```
    cat ...Hiding-From-You
    ```

    ```
    xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
    ```

---

### Credentials Found

- **username:** `bandit4`
- **Password:** `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`
