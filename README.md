# Products API

A simple RESTful API for managing products using Node.js, Express, and MongoDB.

---

## Table of Contents

- [Overview](#overview)
- [Setup & Run](#setup--run)
- [Environment Variables](#environment-variables)
- [API Endpoints](#api-endpoints)
- [Example Requests & Responses](#example-requests--responses)
- [Error Handling](#error-handling)
- [License](#license)

---

## Overview

This API allows you to create, read, update, and delete products stored in a MongoDB database. It includes:

- Input validation for product data
- API key authentication for protected routes (POST, PUT, DELETE)
- Pagination and filtering for listing products
- Custom error handling

---

## Setup & Run

### Prerequisites

- Node.js (v14 or higher recommended)
- MongoDB running locally or accessible remotely

### Steps

1. Clone the repo:

   ```bash
   git clone https://github.com/PLP-MERN-Stack-Development/week-2-express-js-assignment-AngelNelly.git

   cd your-repo-name

   Install dependencies:
   ```

```
npm install

Create a .env file based on .env.example (see below) and configure your environment variables.

Start your MongoDB server if it’s not running:

```

mongod

Run the server:

````
node server.js
Your API will be accessible at: http://localhost:3000

Environment Variables
Create a .env file in the root folder. Here's an example .env.example file:

```ini
MONGO_URI=mongodb://localhost:27017/productsdb
API_KEY=my-secret-key
PORT=3000
Make sure to update these values according to your environment.

API Endpoints
Method	Endpoint	Description	Auth Required	Request Body
GET	/	Base route, returns a greeting	No	None
GET	/api/products	Get all products (with pagination & filtering)	No	Query params: page, limit, category, inStock
GET	/api/products/:id	Get a single product by ID	No	None
POST	/api/products	Create a new product	Yes	JSON product object (see example)
PUT	/api/products/:id	Update a product by ID	Yes	JSON product object
DELETE	/api/products/:id	Delete a product by ID	Yes	None

Example Requests & Responses
1. Create a new product (POST)
Request

POST /api/products
x-api-key: my-secret-key
Content-Type: application/json

{
  "name": "Samsung S22",
  "description": "Android smartphone",
  "price": 550.00,
  "category": "Electronics",
  "inStock": true
}
Response (201 Created)


{
  "_id": "60dfd8c9fc13ae1f64000001",
  "name": "Samsung S22",
  "description": "Android smartphone",
  "price": 550,
  "category": "Electronics",
  "inStock": true,
  "__v": 0
}
2. Get all products (GET)
Request


GET /api/products?page=1&limit=5&category=Electronics&inStock=true
Response (200 OK)


{
  "page": 1,
  "limit": 5,
  "total": 12,
  "data": [
    {
      "_id": "60dfd8c9fc13ae1f64000001",
      "name": "Samsung S22",
      "description": "Android smartphone",
      "price": 550,
      "category": "Electronics",
      "inStock": true,
      "__v": 0
    },
    ...
  ]
}
3. Update a product (PUT)
Request


PUT /api/products/60dfd8c9fc13ae1f64000001
x-api-key: my-secret-key
Content-Type: application/json

{
  "name": "Samsung S22 Ultra",
  "description": "Android smartphone - upgraded",
  "price": 650,
  "category": "Electronics",
  "inStock": true
}
Response (200 OK)


{
  "_id": "60dfd8c9fc13ae1f64000001",
  "name": "Samsung S22 Ultra",
  "description": "Android smartphone - upgraded",
  "price": 650,
  "category": "Electronics",
  "inStock": true,
  "__v": 0
}
4. Delete a product (DELETE)
Request


DELETE /api/products/60dfd8c9fc13ae1f64000001
x-api-key: my-secret-key
Response (200 OK)


{
  "message": "Product deleted",
  "product": {
    "_id": "60dfd8c9fc13ae1f64000001",
    "name": "Samsung S22 Ultra",
    "description": "Android smartphone - upgraded",
    "price": 650,
    "category": "Electronics",
    "inStock": true,
    "__v": 0
  }
}
Error Handling
403 Forbidden - Missing or invalid API key on protected routes.

400 Bad Request - Invalid or missing product data.

404 Not Found - Product not found for given ID.

500 Internal Server Error - Unexpected server error.

Error responses have this format:


{
  "error": "ErrorName",
  "message": "Detailed message"
}
License
This project is licensed under the MIT License.


````
