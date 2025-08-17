# InstaClone (Mini) - Setup Guide (macOS)

This archive contains a simple Instagram-like app:
- Backend: Node.js + Express + MySQL (port 5000)
- Frontend: React (port 3000)

## Steps (basic - step by step)

1. Unzip this archive and open terminal.
   ```bash
   cd ~/Downloads/instagram-clone   # or wherever you extracted the zip
   ```

2. Install Homebrew (if you don't have it):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. Install Node.js and MySQL:
   ```bash
   brew install node
   brew install mysql
   ```

4. Start MySQL server:
   ```bash
   brew services start mysql
   ```
   Optionally run:
   ```bash
   mysql_secure_installation
   ```
   to set a root password.

5. Import the database schema:
   ```bash
   cd backend
   # if you set a MySQL root password, use -p and enter it when prompted:
   mysql -u root -p < db.sql
   # if you did NOT set a root password, run:
   # mysql -u root < db.sql
   ```

6. Configure backend DB password (if needed):
   - Open `backend/server.js` and edit the `password` field in the `db` config to match your MySQL root password (or leave as "password" if you set it to that).

7. Install & start backend:
   ```bash
   npm install
   npm start
   ```
   Backend will run on http://localhost:5000

8. Install & start frontend:
   ```bash
   cd ../frontend
   npm install
   npm start
   ```
   Frontend will open at http://localhost:3000

9. Use the app:
   - Sign up, login, upload images, like posts.

## Troubleshooting
- If `zsh: no such file or directory: backend/db.sql` — make sure you're inside the `instagram-clone` folder and `backend/db.sql` exists:
  ```bash
  pwd
  ls backend
  ```
  If the file is missing, re-extract the zip into a known folder.

- If MySQL connection fails, ensure the server is running (`brew services list`) and the credentials in `backend/server.js` match.

## Notes
- The server stores uploaded images in `backend/uploads/`. You may want to add that folder to `.gitignore` if using git.
- This is a minimal demo — do not use in production without adding proper validation, HTTPS, env vars, and secure JWT secret.
