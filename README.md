# simple-php-blog — Simple Blog (Posts & Comments)

A small PHP + MySQL web app built for a school project. It lets users create blog posts,
edit and delete their own posts, and leave comments on any post.

> ⚠️ **NOT FOR PRODUCTION USE**
> This is coursework only. It has **no authentication/login**, uses unescaped SQL in some
> queries (SQL injection risk), stores DB credentials in plain text, and enables
> `display_errors`. Do **not** deploy it on a public server or use it for real data.

## Features

- Create a post (title, content, author)
- List posts newest first
- Edit / delete a post (only shown when the session author matches the post author)
- Comment on any post
- Plain CSS styling in `style.css`

## Files

| File          | Purpose                                    |
|---------------|--------------------------------------------|
| `index.php`   | Create posts, list posts, show comments    |
| `comment.php` | Handle new comment submissions             |
| `edit.php`    | Edit an existing post                      |
| `delete.php`  | Delete a post                              |
| `db.php`      | MySQL connection settings                  |
| `sql.sql`     | Database + table schema                    |
| `style.css`   | Stylesheet                                 |

## Requirements

- PHP 7.4+ (with `mysqli` extension)
- MySQL 5.7+ / MariaDB 10.3+
- A local web server: Apache (XAMPP, WAMP, MAMP) or PHP's built-in server

## Installation

### 1. Get the code

```bash
git clone https://github.com/d3vnul10/simple-php-blog.git
cd simple-php-blog
```

### 2. Set up the database

Create the database and tables:

```bash
mysql -u root -p < sql.sql
```

Or import `sql.sql` via phpMyAdmin → Import.

### 3. Create the DB user (optional)

`db.php` expects the user `phpuser`:

```sql
CREATE USER 'phpuser'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT ALL PRIVILEGES ON blog.* TO 'phpuser'@'localhost';
FLUSH PRIVILEGES;
```

### 4. Configure the connection

Edit `db.php` and set `$host`, `$user`, `$pass`, `$dbname` to match your setup.

### 5. Run the app

**Option A — XAMPP / WAMP / MAMP**

1. Copy the project folder into `htdocs` (XAMPP) or `www` (WAMP).
2. Start Apache and MySQL.
3. Open <http://localhost/simple-php-blog/> in a browser.

**Option B — PHP built-in server (no Apache needed)**

```bash
php -S localhost:8000
```

Then open <http://localhost:8000>.

## Usage

1. Fill in title, content and author name, then click **Post**.
2. Your author name is stored in the session — Edit/Delete links appear only on your posts.
3. Scroll to a post's comment section, enter your name and comment, then click **Comment**.

## Known issues (intentional, coursework scope)

- SQL injection in `delete.php`, `edit.php` and the post insert query.
- No authentication — author matching is session-name based only.
- `sql.sql` creates `comments.author`, but the code reads/writes `comments.commenter`.
  Rename the column to keep them consistent:

  ```sql
  ALTER TABLE comments CHANGE author commenter VARCHAR(100) NOT NULL;
  ```
