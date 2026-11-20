# Bandit Level 6 → Level 7

### Challenge

The password for the next level is stored somewhere on the server and has all of the following properties:
- Owned by user `bandit7`
- Owned by group `bandit6`
- 33 bytes in size

### Walkthrough

1.  Log in to the server as `bandit6` using the password from the previous level:

    ```
    ┌──(nothspec㉿Nothspec)-[~]
    └─$ ssh bandit6@bandit.labs.overthewire.org -p 2220
    ```

2.  Search the entire filesystem (`/`) for a regular file matching all the criteria, redirecting error messages (such as "Permission denied") to `/dev/null`:

    ```
    find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
    ```

    ```
    /var/lib/dpkg/info/bandit7.password
    ```

3.  Print the contents of the file with `cat`:

    ```
    cat /var/lib/dpkg/info/bandit7.password
    ```

    ```
    Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
    ```

---

### Credentials Found

- **username:** `bandit7`
- **Password:** `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`
