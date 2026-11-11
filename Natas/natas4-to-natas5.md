# Natas Level 4 → Level 5

### Challenge

**URL: http://natas4.natas.labs.overthewire.org/**

![alt text](images/image-13.png)

After logging in, the page shows an error message:

"Access disallowed. You are visiting from http://natas4.natas.labs.overthewire.org/, while authorized users should come only from http://natas5.natas.labs.overthewire.org/"

This level checks the HTTP `Referer` header, which tells the server which page the request came from.

### Walkthrough

- The server checks the `Referer` header of your request. It expects you to originate from the Level 5 URL. Since we are currently on Level 4, our browser automatically sends the Level 4 URL as the referrer.
- Intercept and modify the request using **Burp Suite**:
  - Open **Burp Suite** and enable the **Proxy Intercept**.
  - Refresh the Natas 4 page.
  - In the intercepted request, locate the line: `Referer: http://natas4.natas.labs.overthewire.org/`
    ![alt text](images/image-14.png)
  - Change the `4` to a `5`: `Referer: http://natas5.natas.labs.overthewire.org/`
  - Click **Forward**.
    ![alt text](images/image-15.png)

---

### Credentials Found

- **username:** `natas5`
- **Password:** `0n35PkggAPm2zbEpOU802c0x0Msn1ToK`
