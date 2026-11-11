# Natas Level 3 → Level 4

### Challenge

**URL: http://natas3.natas.labs.overthewire.org/**
![alt text](images/image-8.png)

### Walkthrough

- The phrase _"No more information leaks!! Not even Google will find it this time..."_ points to `robots.txt`, which tells search engine crawlers which paths not to index.
  ![alt text](images/image-9.png)
- Open `http://natas3.natas.labs.overthewire.org/robots.txt`.
- It contains a `Disallow` entry for `/s3cr3t/`, showing that the directory exists on the server.
  ![alt text](images/image-10.png)
- Go to `http://natas3.natas.labs.overthewire.org/s3cr3t/`.
  ![alt text](images/image-11.png)
- Open `users.txt` from the directory listing to read the password for the next level.
  ![alt text](images/image-12.png)

---

### Credentials Found

- **username:** `natas4`
- **Password:** `QryZXc2e0zahULdHrtHxzyYkj59kUxLQ`
