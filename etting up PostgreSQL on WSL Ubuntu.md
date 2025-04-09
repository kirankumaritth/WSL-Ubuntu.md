# ✅ Part 1: Setting up PostgreSQL on WSL Ubuntu (Windows Subsystem for Linux)

---

### 🐧 Step 1: Install WSL (if not already done)

Open PowerShell as Admin and run:

```powershell
wsl --install
```

> This installs Ubuntu by default. Reboot if prompted.

---

### 🐧 Step 2: Open Ubuntu WSL

After reboot, open the **"Ubuntu"** app from Start Menu.

---

### 🧰 Step 3: Update Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

---

### 🐘 Step 4: Install PostgreSQL

```bash
sudo apt install postgresql postgresql-contrib -y
```

---

### 🔍 Step 5: Check PostgreSQL status

```bash
sudo service postgresql status
```

To start the PostgreSQL service if it's not running:

```bash
sudo service postgresql start
```

---

### 👤 Step 6: Switch to `postgres` user

```bash
sudo -i -u postgres
```

Now you're inside the `postgres` user and can use `psql`.

---

### 💡 Step 7: Set password for postgres user

```bash
psql
```

Inside the prompt:

```sql
ALTER USER postgres WITH PASSWORD 'yourpassword';
\q
```

Type `exit` to return to your user account.

---

## ✅ Part 2: Setup Code Screen Project

---

### 📁 Step 8: Create project folder and files

```bash
mkdir compass_code_screen
cd compass_code_screen
touch create_db.sh db_schema.sql users.sql function_view.sql
```

---

### ✏️ Step 9: Paste content into each file

**a. `create_db.sh`**
```bash
#!/bin/bash

DB_NAME="books_db"
DB_USER="postgres"

echo "🔄 Creating Database and Tables..."
psql -U $DB_USER -f db_schema.sql

echo "👥 Creating Users..."
psql -U $DB_USER -d $DB_NAME -f users.sql

echo "🧠 Creating Functions and Views..."
psql -U $DB_USER -d $DB_NAME -f function_view.sql

echo "✅ Done!"
```

Make it executable:

```bash
chmod +x create_db.sh
```

---

**b. `db_schema.sql`**
```sql
DROP DATABASE IF EXISTS books_db;
CREATE DATABASE books_db;

\connect books_db;

CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    subtitle VARCHAR(255),
    author VARCHAR(255) NOT NULL,
    publisher VARCHAR(255) NOT NULL
);
```

---

**c. `users.sql`**
```sql
-- Admin user
CREATE USER admin_user WITH PASSWORD 'AdminPass123';
GRANT ALL PRIVILEGES ON DATABASE books_db TO admin_user;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO admin_user;

-- View-only user
CREATE USER view_user WITH PASSWORD 'ViewPass123';
GRANT CONNECT ON DATABASE books_db TO view_user;
GRANT USAGE ON SCHEMA public TO view_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO view_user;
```

---

**d. `function_view.sql`**
```sql
-- Function to count books
CREATE OR REPLACE FUNCTION total_books()
RETURNS INTEGER AS $$
BEGIN
    RETURN (SELECT COUNT(*) FROM books);
END;
$$ LANGUAGE plpgsql;

-- View for book summary
CREATE VIEW book_summary AS
SELECT title, author FROM books;
```

---

## ✅ Part 3: Running the Script

---

### ▶️ Step 10: Execute the Bash Script

Back in your project directory:

```bash
./create_db.sh
```

You'll be prompted for the PostgreSQL password (enter the one you set earlier).

---

## ✅ Part 4: Verify Execution

---

### 🧪 Step 11: Login to PostgreSQL

```bash
psql -U postgres -d books_db
```

Run queries:

```sql
\dt                       -- See tables
SELECT * FROM books;      -- See data (empty table)

SELECT total_books();     -- Test function
SELECT * FROM book_summary; -- Test view
```

---

## 🧼 Step 12: Clean Up (optional)

If needed:

```bash
dropdb books_db
dropuser admin_user
dropuser view_user
```

---

## ✅ Summary

You now have:
- PostgreSQL setup on WSL Ubuntu
- A Bash script to automate DB creation
- Tables, users, function, and view
