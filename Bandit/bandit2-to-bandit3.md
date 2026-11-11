# Bandit Level 2 → Level 3

### Challenge

The password for `bandit3` is stored in a file called `--spaces in this filename--` inside the `/home/bandit2` directory. This filename combines two shell edge cases: spaces (which split unquoted filenames into separate arguments) and a leading `--` (which causes `cat` to interpret the argument as a command-line option).

### Walkthrough

1.  Log in to the server as `bandit2` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit2@bandit.labs.overthewire.org -p 2220
    ```

2.  Check the files inside `/home/bandit2`:

    ```
    ls -la
    ```

    You will see the file `--spaces in this filename--` (`-rw-r----- 1 bandit3 bandit2`).

3.  Quote the filename (or escape each space with `\`) so the shell treats it as one argument, and prefix it with `./` (or place `--` before it) so `cat` does not interpret `--spaces...` as an option:

    ```
    cat "./--spaces in this filename--"
    ```

    Alternatives: `cat -- "--spaces in this filename--"` or `cat ./--spaces\ in\ this\ filename--`.

    ```
    7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
    ```

---

### Credentials Found

- **username:** `bandit3`
- **Password:** `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`
