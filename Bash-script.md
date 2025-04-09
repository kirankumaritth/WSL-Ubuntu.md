## ✅ Task Breakdown

You're asked to:
1. Create a **PostgreSQL database** with relevant **tables** (books info).
2. Create **admin and view-only users**.
3. Create at least one **function/procedure** and **view**.

---

## 🗂 File Structure Suggestion

```
compass_code_screen/
│
├── create_db.sh                   # Main Bash script
├── db_schema.sql                  # SQL to create database and tables
├── users.sql                      # SQL to create admin/view users
├── function_view.sql              # SQL function and views
```

---

## 🧠 Step-by-Step Implementation

### 🧾 1. `create_db.sh` (Main Bash Script)

```bash
#!/bin/bash

# Variables
DB_NAME="books_db"
DB_USER="postgres"

echo "Creating Database and Tables..."
psql -U $DB_USER -f db_schema.sql

echo "Creating Users..."
psql -U $DB_USER -d $DB_NAME -f users.sql

echo "Creating Functions and Views..."
psql -U $DB_USER -d $DB_NAME -f function_view.sql

echo "✅ Database setup completed!"
```

> Make sure to `chmod +x create_db.sh` before running it.

---

### 📘 2. `db_schema.sql` (Database + Table Setup)

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

### 👥 3. `users.sql` (Admin + View-Only Users)

```sql
-- Admin user with full privileges
CREATE USER admin_user WITH PASSWORD 'AdminPass123';
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO admin_user;
GRANT ALL PRIVILEGES ON DATABASE books_db TO admin_user;

-- View-only user
CREATE USER view_user WITH PASSWORD 'ViewPass123';
GRANT CONNECT ON DATABASE books_db TO view_user;
GRANT USAGE ON SCHEMA public TO view_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO view_user;
```

---

### 🧠 4. `function_view.sql` (Procedure + View)

```sql
-- Function to count books
CREATE OR REPLACE FUNCTION total_books()
RETURNS INTEGER AS $$
BEGIN
    RETURN (SELECT COUNT(*) FROM books);
END;
$$ LANGUAGE plpgsql;

-- View for displaying book summaries
CREATE VIEW book_summary AS
SELECT title, author FROM books;
```

---

## 🧪 Test It

To test:
1. Start PostgreSQL server.
2. Run: `./create_db.sh`
3. Connect as `psql -U admin_user -d books_db`
4. Run: `SELECT * FROM book_summary;` or `SELECT total_books();`

---
