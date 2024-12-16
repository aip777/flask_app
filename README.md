# Flask Product API

This is a Flask-based REST API for managing user registration, login, and CRUD operations on products.

---

## Features

- User Registration
- User Login with JWT authentication
- Create, Read, Update, and Delete (CRUD) operations for products
- Pagination for listing products (default limit: 10 per page)
- Environment variable configuration with `.env`

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com:aip777/flask_app.git
   cd flask_app
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate
   ```

3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the project root with the following content:
   ```env
   DATABASE_NAME=products.db
   SQLALCHEMY_TRACK_MODIFICATIONS=False
   JWT_SECRET_KEY=your_jwt_secret_key
   SECRET_KEY=your_flask_secret_key
   API_LIMIT=10
   ```

---

## Usage

1. Initialize the database:
   ```bash
   flask shell
   from app import db
   db.create_all()
   exit()
   ```

2. Run the application:
   ```bash
   python app.py
   ```

3. The API will be available at `http://127.0.0.1:5000`.

---

## API Endpoints

### **Authentication**

#### 1. Register User
**POST** `/register`

- **Request Body:**
  ```json
  {
    "username": "example_user",
    "password": "example_password"
  }
  ```
- **Response:**
  ```json
  {
    "message": "User registered successfully"
  }
  ```

#### 2. Login
**POST** `/login`

- **Request Body:**
  ```json
  {
    "username": "admin",
    "password": "admin123123"
  }
  ```
- **Response:**
  ```json
  {
    "access_token": "jwt_token"
  }
  ```

### **Products**

#### 1. Create Product
**POST** `/products`

- **Headers:**
  `Authorization: Bearer <your_jwt_token>`
- **Request Body:**
  ```json
  {
    "name": "Automate the Boring Stuff with Python",
    "description": "A good book for beginners, this book presents practical programming concepts in an easy-to-understand",
    "price": 99.99
  }
  ```
- **Response:**
  ```json
  {
    "message": "Product created successfully"
  }
  ```

#### 2. Get All Products
**GET** `/products`

- **Headers:**
  `Authorization: Bearer <your_jwt_token>`
- **Query Parameters:**
  - `page` (optional): Page number (default: 1)
- **Response:**
  ```json
  {
    "products": [
      {
        "id": 1,
        "name": "Automate the Boring Stuff with Python",
        "description": "A good book for beginners, this book presents practical programming concepts in an easy-to-understand",
        "price": 99.99
      }
    ],
    "total_pages": 1,
    "current_page": 1
  }
  ```

#### 3. Get Product by ID
**GET** `/products/<product_id>`

- **Headers:**
  `Authorization: Bearer <your_jwt_token>`
- **Response:**
  ```json
  {
    "id": 1,
    "name": "Automate the Boring Stuff with Python",
    "description": "A good book for beginners, this book presents practical programming concepts in an easy-to-understand",
    "price": 99.99
  }
  ```

#### 4. Update Product
**PUT** `/products/<product_id>`

- **Headers:**
  `Authorization: Bearer <your_jwt_token>`
- **Request Body:**
  ```json
  {
    "name": "Boring Stuff with Python",
    "description": "Updated A good book for beginners",
    "price": 149.99
  }
  ```
- **Response:**
  ```json
  {
    "message": "Product updated successfully"
  }
  ```

#### 5. Delete Product
**DELETE** `/products/<product_id>`

- **Headers:**
  `Authorization: Bearer <your_jwt_token>`
- **Response:**
  ```json
  {
    "message": "Product deleted successfully"
  }
  ```

---
