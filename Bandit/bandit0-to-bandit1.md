# Bandit Level 0 → Level 1

### Challenge

The goal of this level is to log into the Bandit server using SSH on port `2220`, then locate and read the `readme` file in the home directory to find the password for `bandit1`.

### Walkthrough

1.  Connect to `bandit.labs.overthewire.org` on port `2220` as `bandit0` (password `bandit0`):

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit0@bandit.labs.overthewire.org -p 2220
    ```

    Type `yes` if prompted to accept the host key, then enter the password `bandit0`.
2.  Once logged in (`/home/bandit0`), list the files in the directory:

    ```
    ls -la
    ```

    You will see a file named `readme` (`-rw-r----- 1 bandit1 bandit0`).
3.  Print the contents of `readme` with `cat`:

    ```
    cat readme
    ```

    ```
    Congratulations on your first steps into the bandit game!!
    Please make sure you have read the rules at https://overthewire.org/rules/
    If you are following a course, workshop, walkthrough or other educational activity,
    please inform the instructor about the rules as well and encourage them to
    contribute to the OverTheWire community so we can keep these games free!

    The password you are looking for is: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
    ```

---

### Credentials Found

- **username:** `bandit1`
- **Password:** `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`
