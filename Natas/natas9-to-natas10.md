# Natas Level 9 → Level 10

### Challenge

**URL: http://natas9.natas.labs.overthewire.org/**

The search function on this page uses the PHP `passthru()` function to execute a system-level `grep` command. The backend code looks like this:

```
passthru("grep -i $key dictionary.txt");
```

The variable `$key` comes directly from the search box without sanitization, so we can pass additional file arguments to `grep` and read other files on the system.

### Walkthrough

1.  The `grep` command follows the format: `grep [options] [pattern] [file]`. By adding a space after our search pattern, we can trick `grep` into thinking we are providing a list of multiple files to search through.
2.  To read the password file for the next level, use the following input in the search box:

    ```
    .* /etc/natas_webpass/natas10
    ```

3.  The full command becomes `grep -i .* /etc/natas_webpass/natas10 dictionary.txt`. Because `.*` matches everything, `grep` prints lines from `/etc/natas_webpass/natas10` first and then searches `dictionary.txt`.

    ![alt text](images/image-23.png)

---

### Credentials Found

- **username:** `natas10`
- **Password:** `t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu`
