# LibraryMS — Setup Guide (XAMPP)

## Project Structure
```
library/
├── index.html          ← Main admin panel (open this in browser)
├── database.sql        ← Import this into MySQL first
└── php/
    ├── config.php      ← DB connection (edit credentials here)
    ├── books.php       ← Books API
    ├── members.php     ← Members API
    ├── borrowings.php  ← Borrowings API
    ├── stats.php       ← Dashboard stats API
    └── lookup.php      ← Categories & authors dropdown data
```

---

## Step-by-Step Setup

### 1. Place the project folder
Copy the `library/` folder into your XAMPP `htdocs` directory:
```
C:\xampp\htdocs\library\
```

### 2. Start XAMPP
Open XAMPP Control Panel and start:
- ✅ Apache
- ✅ MySQL

### 3. Import the database
1. Open your browser and go to: http://localhost/phpmyadmin
2. Click **Import** tab (top menu)
3. Click **Choose File** → select `database.sql`
4. Click **Go** at the bottom

This creates the `library_db` database with all tables and sample data.

### 4. Open the app
Go to: **http://localhost/library/index.html**

---

## Database Credentials
Default XAMPP credentials are already set in `php/config.php`:
- Host: `localhost`
- User: `root`
- Password: *(empty)*
- Database: `library_db`

If you changed your MySQL password, edit `php/config.php`.

---

## Features
| Feature | Description |
|---|---|
| 📊 Dashboard | Stats overview + recent borrowings |
| 📚 Books | Add, edit, delete books with category & author |
| 👥 Members | Register, manage, suspend members |
| 🔄 Borrowings | Record loans, mark returns, track overdue |
| 🔍 Search | Live search on books and members |
| 🚦 Status | Auto-detects overdue books daily |

---

## Relational Database Schema

```
categories ─┐
            ├─ books ─── book_authors ─── authors
            │      └─── borrowings ──────── members
```

**Foreign Keys:**
- `books.category_id` → `categories.category_id`
- `book_authors.book_id` → `books.book_id`
- `book_authors.author_id` → `authors.author_id`
- `borrowings.book_id` → `books.book_id`
- `borrowings.member_id` → `members.member_id`
