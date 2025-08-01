import sqlite3

# Connect to a new SQLite database (or open if exists)
conn = sqlite3.connect('my_database.db')
cursor = conn.cursor()

# Step 1: Create a table
cursor.execute('''
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    age INTEGER,
    email TEXT
)
''')

# Step 2: Insert sample data
sample_users = [
    ("Alice", 25, "alice@example.com"),
    ("Bob", 30, "bob@example.com"),
    ("Charlie", 22, "charlie@example.com")
]

cursor.executemany('INSERT INTO users (name, age, email) VALUES (?, ?, ?)', sample_users)
conn.commit()

# Step 3: Fetch and print all users
cursor.execute('SELECT * FROM users')
all_users = cursor.fetchall()

print("📋 User List:")
for user in all_users:
    print(f"ID: {user[0]}, Name: {user[1]}, Age: {user[2]}, Email: {user[3]}")

# Close the connection
conn.close()
