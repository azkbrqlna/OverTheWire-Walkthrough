# Bandit Level 1 → Level 2

### Challenge

The password for `bandit2` is stored in a file named `-` (a dashed filename) inside the `/home/bandit1` directory. Passing `-` directly to commands like `cat` fails because `-` is interpreted as standard input (`stdin`) or an option flag rather than a file path.

### Walkthrough

1.  **Connect via SSH:** Log in to the server as `bandit1` using the password obtained from the previous level:

    ```
    ssh bandit1@bandit.labs.overthewire.org -p 2220
    ```

2.  **List the Home Directory:** Check the files inside `/home/bandit1`:

    ```
    ls -la
    ```

    You will see the file `-` (`-rw-r----- 1 bandit2 bandit1`).

3.  **Read the Dashed Filename:** Prefix the filename with `./` (or use `--` / input redirection `<`) so `cat` treats `-` as a file path instead of reading from `stdin`:

    ```
    cat ./-
    ```

    (Alternative commands that also work: `cat -- -`, `cat < -`, or `cat /home/bandit1/-`.)

    ```
    PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
    ```

---

### Credentials Found

- **username:** `bandit2`
- **Password:** `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`
