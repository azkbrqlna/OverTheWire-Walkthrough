# Bandit Level 0 → Level 1

### Challenge

The goal of this level is to log into the Bandit server using SSH on port `2220`, then locate and read the `readme` file in the home directory to find the password for `bandit1`.

### Walkthrough

1.  **Connect via SSH:** Open a terminal and connect to `bandit.labs.overthewire.org` on port `2220` using the credentials provided above:

    ```
    ssh bandit0@bandit.labs.overthewire.org -p 2220
    ```

    Type `yes` if prompted to accept the host key, then enter the password `bandit0`.
2.  **List the Home Directory:** Once logged in (`/home/bandit0`), list the files in the directory to locate the file containing the password:

    ```
    ls -la
    ```

    You will see a file named `readme` (`-rw-r----- 1 bandit1 bandit0`).
3.  **Read the Password File:** Display the contents of `readme` using `cat` to reveal the password for the next level:

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
