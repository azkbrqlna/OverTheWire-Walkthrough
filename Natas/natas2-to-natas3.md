# Natas Level 2 → Level 3

### Challenge

**URL: http://natas2.natas.labs.overthewire.org/**

![alt text](images/image-4.png)

The page says "there is nothing on this page", and the password is not in an HTML comment. Check for files or directories left accessible on the server.

### Walkthrough

- View the source code (`Ctrl + U`). An `<img>` tag points to `/files/`:
  ![alt text](images/image-5.png)
- Check whether directory indexing is enabled at `http://natas2.natas.labs.overthewire.org/files/`.
- Inside the directory listing, you will see two files:
  ![alt text](images/image-6.png)
- Open `users.txt`. This file contains a list of usernames and passwords. Look for the entry for `natas3`
  ![alt text](images/image-7.png)

---

### Credentials Found

- **username:** `natas3`
- **Password:** `3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH`
