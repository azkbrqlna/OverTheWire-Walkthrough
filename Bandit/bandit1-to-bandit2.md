# Bandit Level 1 → Level 2

### Challenge

The password for `bandit2` is in a file named `-` inside `/home/bandit1`. Running `cat -` fails because `cat` treats `-` as standard input (`stdin`) instead of a filename.

### Walkthrough

1.  Log in to the server as `bandit1` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit1@bandit.labs.overthewire.org -p 2220
    ```

2.  Check the files inside `/home/bandit1`:

    ```
    ls -la
    ```

    You will see the file `-` (`-rw-r----- 1 bandit2 bandit1`).

3.  Prefix the filename with `./` (or use `--` / input redirection `<`) so `cat` treats `-` as a file path instead of reading from `stdin`:

    ```
    cat ./-
    ```

    Alternatives: `cat -- -`, `cat < -`, or `cat /home/bandit1/-`.

    ```
    PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
    ```

---

### Credentials Found

- **username:** `bandit2`
- **Password:** `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`
