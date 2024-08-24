# How to View Your Username and Password in PostgreSQL

## Viewing Your Current Username

To see your current username in PostgreSQL, follow these steps:

1. Connect to your PostgreSQL instance using the following command:
   ```bash
   psql -U postgres
   ```
2. Run the following SQL query to get your current username:
   ```SELECT current_user;

   ```
3. to see info detail:
   `\du`

## Important Note on Passwords

Passwords are stored in PostgreSQL in a hashed format for security reasons, so you cannot retrieve a user's password in plain text. If you forget the password, the best course of action is to reset it.

To reset the password for a user, you can use the following SQL command:

```ALTER USER your_username WITH PASSWORD 'new_password';

```
