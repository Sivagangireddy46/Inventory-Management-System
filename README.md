# Inventory-Management-System
Build a Python program to manage inventory for a store or warehouse. The system should allow users to add, edit, and delete products, track inventory levels,  and generate reports such as low- stock alerts or sales summaries. Implement features like user authentication, data validation, and graphical user interface (GUI) for better usability.
15 March 2025
11:25

import sqlite3

def create_tables():
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS users (
                        id INTEGER PRIMARY KEY AUTOINCREMENT,
                        username TEXT NOT NULL UNIQUE,
                        password TEXT NOT NULL)''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS products (
                        id INTEGER PRIMARY KEY AUTOINCREMENT,
                        name TEXT NOT NULL,
                        quantity INTEGER NOT NULL,
                        price REAL NOT NULL)''')
    
    conn.commit()
    conn.close()

def add_user(username, password):
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('INSERT INTO users (username, password) VALUES (?, ?)', (username, password))
    conn.commit()
    conn.close()

def get_user(username):
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM users WHERE username = ?', (username,))
    user = cursor.fetchone()
    conn.close()
    return user

def add_product(name, quantity, price):
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('INSERT INTO products (name, quantity, price) VALUES (?, ?, ?)', (name, quantity, price))
    conn.commit()
    conn.close()

def update_product(product_id, name, quantity, price):
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('UPDATE products SET name = ?, quantity = ?, price = ? WHERE id = ?', (name, quantity, price, product_id))
    conn.commit()
    conn.close()

def delete_product(product_id):
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('DELETE FROM products WHERE id = ?', (product_id,))
    conn.commit()
    conn.close()

def get_all_products():
    conn = sqlite3.connect('inventory.db')
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM products')
    products = cursor.fetchall()
    conn.close()
    return products![image](https://github.com/user-attachments/assets/f4f31f8d-27cd-4dde-b68f-73ac6f3af407)
    
