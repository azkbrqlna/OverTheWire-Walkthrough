# Natas Level 1 → Level 2

### Challenge

**URL: http://natas1.natas.labs.overthewire.org/**

![alt text](images/image-2.png)

The page content is identical to the previous level, but there is a security measure in place: Right-click has been disabled to prevent users from easily accessing the "Inspect" or "View Source" menu.

### Walkthrough

1. Since the context menu is blocked, you cannot right-click to inspect the page. You must use alternative methods to view the source code:

- **Keyboard Shortcut:** Press `Ctrl + U` (Windows/Linux) or `Cmd + Option + U` (Mac).
- **URL Prefix:** Manually type `view-source:` before the URL in your address bar: `view-source:http://natas1.natas.labs.overthewire.org/`
- **Developer Tools:** Press `F12` or `Ctrl + Shift + I` to open the Inspector directly.

2. Look within the HTML elements. Developers often leave comments in the code that are not visible on the rendered page.
   ![alt text](images/image-3.png)

---

### Credentials Found

- **username:** `natas2`
- **Password:** `TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI`
