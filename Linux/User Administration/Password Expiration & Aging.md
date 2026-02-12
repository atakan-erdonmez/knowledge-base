In Linux, managing when and how users must change their passwords is a core security function. This process is primarily controlled by settings stored for each user in the `/etc/shadow` file. You interact with these settings using the `chage` (change age) command.

## 1. The Data Source: `/etc/shadow` File Fields

Each user has a line in this file, and these fields are separated by colons (`:`).

| Field Name                     | Your Note's Description                                                          | Expanded Explanation                                                                                                                                                                                                                       |
| ------------------------------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Last Password Change**       | When the password was last changed                                               | The date the password was last modified, measured in **days since the Unix Epoch (January 1, 1970)**. The `chage -l` command translates this into a human-readable date for you.                                                           |
| **Minimum Password Age**       | The minimum number of days a password must be used before it can be changed.     | This prevents users from changing their password multiple times in a row to circumvent password history policies. A value of `0` means they can change it at any time.                                                                     |
| **Maximum Password Age**       | The maximum number of days a password can be used before it needs to be changed. | This is the core of password expiration policy. After this many days, the password "expires."                                                                                                                                              |
| **Password Warning Period**    | The number of days before a password expires that the user will be warned.       | If the `Maximum Password Age` is 90 and this value is 7, the user will start seeing warning messages upon login 7 days before the password expires.                                                                                        |
| **Password Inactivity Period** | The number of days after a password expires that the account will be disabled.   | This is the "grace period." After the password expires, the user has this many days to log in and change it. If they fail to do so within this window, the account is locked. **A value of -1 (or empty) means this feature is disabled.** |
| **Account Expiration Date**    | The date when the account will be disabled (optional).                           | This is an **absolute date** (e.g., 2025-12-31) when the account is locked, regardless of password status. It's also measured in days since the epoch. Useful for temporary accounts.                                                      |


---

## 2. The Administrator's Tool: The `chage` Command

The `chage` command is your primary tool for viewing and modifying these aging policies for individual users. You almost always need to run it with `sudo`.


| Flag                     | Purpose                      | Example Usage & Explanation                                                                                                                                                                                                      |
| ------------------------ | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-l <username>`          | **List**                     | **View the current aging settings for a user.** This is the first command you should run to see the current state before making changes.  <br>`sudo chage -l sysadmin`                                                           |
| `-M <days>`              | **Maximum Age (Expiration)** | Sets the maximum number of days a password is valid.  <br>`sudo chage -M 90 sysadmin` (Password expires after 90 days).                                                                                                          |
| `-m <days>`              | **Minimum Age**              | Sets the minimum number of days before a password can be changed.  <br>`sudo chage -m 1 sysadmin` (User must wait at least 1 day to change their password again).                                                                |
| `-W <days>`              | **Warning Period**           | Sets the number of days before expiration that the user receives a warning.  <br>`sudo chage -W 14 sysadmin` (Warn the user for 14 days before the password expires).                                                            |
| `-I <days>`              | **Inactive Period**          | Sets the grace period in **days after expiration** before the account is locked.  <br>`sudo chage -I 30 sysadmin` (After the password expires, the user has 30 days to log in and change it before being locked out).            |
| `-E <YYYY-MM-DD>`        | **Expire Date (Account)**    | Sets a **specific date** when the account will be locked. This is for the _account_, not the password.  <br>`sudo chage -E 2025-10-31 temp_user` (The account `temp_user` will be locked on October 31st, 2025, no matter what). |
| `-d <YYYY-MM-DD>` or `0` | **Last Change Date**         | Sets the date of the last password change. Setting this to `0` **forces the user to change their password on next login.**  <br>`sudo chage -d 0 someuser`                                                                       |

**Special Value:** As you noted, setting a value to `-1` for `M`, `W`, or `I` typically means "never" or that the feature is disabled.

---

## 3. The User's Experience: The Lifecycle Procedure

This clarifies your "Procedure" notes into a clear timeline.

- **Stage 1: Normal Use & Warning**
    
    - The user logs in normally.
        
    - Once the `(Maximum Age - Warning Period)` date is reached, the user will see a message upon login: `Warning: your password will expire in X days.`
        
- **Stage 2: Password Expired (Grace Period)**
    
    - The user's password has now passed its `Maximum Age`.
        
    - Upon the next login attempt, the system will immediately force them to change their password.
        
    - The prompt will say something like: `You are required to change your password immediately (password aged).`
        
    - They cannot access their shell or do anything else until they provide a new, valid password.
        
    - This is possible only during the `Inactive Period` (the grace period set by `-I`).
        
- **Stage 3: Password Inactive**
    
    - The `Inactive Period` has passed. The user has not logged in to change their expired password within the grace period.
        
    - When they try to log in, the authentication will fail. Their account is now **locked**.
        
    - They cannot fix this themselves. They must contact a system administrator (you) to have their password reset or the account unlocked.
        
- **Stage 4: Account Expired**
    
    - This is separate from password expiration. If a date was set with `chage -E`, the account is **locked** on that date.
        
    - This is an administrative lock, and the user must contact an admin to have the account re-enabled.
        

---

## 4. Global Policy: `/etc/login.defs`

Manually running `chage` on every new user is inefficient. For consistent policy, you set the **default** values in `/etc/login.defs`.

**Important:** Changes in `/etc/login.defs` **only apply to users created _after_ the change is made.** It does not affect existing users.

The relevant lines in this file are:

- `PASS_MAX_DAYS 90` (Corresponds to `chage -M`)
    
- `PASS_MIN_DAYS 1` (Corresponds to `chage -m`)
    
- `PASS_WARN_AGE 14` (Corresponds to `chage -W`)
    

These settings ensure that any new user you create with `useradd` will automatically have this password aging policy applied. This is crucial for maintaining a baseline security posture on your servers.