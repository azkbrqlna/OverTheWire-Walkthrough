# Natas Level 14 → Level 15

### Challenge

**URL: [http://natas14.natas.labs.overthewire.org/](https://www.google.com/search?q=http://natas14.natas.labs.overthewire.org/)**

This level demonstrates a classic **SQL Injection (SQLi)** vulnerability within a login authentication system. The PHP script takes user input from a POST request and directly concatenates it into a SQL query string. Because the input is enclosed in double quotes (`"`) and not sanitized, we can inject SQL commands to alter the logic of the query. The vulnerable query construction is: `$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";`

---

### Walkthrough

1. The database checks if both the username and password match a record in the `users` table. The query looks like this: `SELECT * FROM users WHERE username="[USER]" AND password="[PASS]"`. To bypass this without a valid password, we need to make the entire `WHERE` clause evaluate to **TRUE**.
2. While we can inject into either field, injecting into the `password` field allows us to bypass the requirement for a specific user match. By using the payload `" or "1"="1`, we terminate the password string and add a condition that is always true.
3. **The Payload:**
   - **Username:** `admin` (or any existing user, even blank)
   - **Password:** `" or "1"="1`

4. When submitted, the server executes the following: `SELECT * FROM users WHERE username="admin" AND password="" or "1"="1"`

   In SQL logic, the `AND` operator is evaluated before `OR`. The query is processed as: `(username="admin" AND password="") OR ("1"="1")`

   Even if the first part is false (because the password isn't blank), the second part (`"1"="1"`) is always **TRUE**. Therefore, the database returns a row, `mysqli_num_rows` becomes greater than 0, and the login is successful.

5. **Execution:**
   - Type `admin` in the **Username** field.
   - Type `" or "1"="1` in the **Password** field.
   - Click **Login**.
     ![alt text](images/image-30.png)

---

### Credentials Found

- **Username:** `natas15`
- **Password:** `SdqIqBsFcz3yotlNYErZSZwblkm0lrvx`
