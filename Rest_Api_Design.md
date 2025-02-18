# REST API Design for a Library Catalogue

## 1. Introduction
This document presents the design of a RESTful API for a Library Catalogue. The API manages books, authors, and categories, enabling users to search, filter, and manage library resources efficiently.

## 2. Entities
### 2.1 Book
- `id` (UUID, unique identifier)
- `title` (String, required)
- `author_id` (UUID, foreign key to Author)
- `category_id` (UUID, foreign key to Category)
- `published_date` (Date, optional)
- `isbn` (String, unique, required)
- `available_copies` (Integer, required)

### 2.2 Author
- `id` (UUID, unique identifier)
- `name` (String, required)
- `birth_date` (Date, optional)
- `nationality` (String, optional)

### 2.3 Category
- `id` (UUID, unique identifier)
- `name` (String, unique, required)

## 3. API Endpoints
### 3.1 Books
**GET /books**
- Returns a paginated list of books.
- Filters: `title`, `author_id`, `category_id`, `published_date`.
- HATEOAS links provided for navigation.

**POST /books**
- Creates a new book.
- Requires authentication.
- HATEOAS links included in the response.

**GET /books/{id}**
- Retrieves a single book by its ID.
- HATEOAS links included.

**PUT /books/{id}**
- Updates book details.
- Requires authentication.
- HATEOAS links included.

**DELETE /books/{id}**
- Deletes a book.
- Requires authentication.
- HATEOAS links included.

### 3.2 Authors
**GET /authors**
- Returns a paginated list of authors.
- Filters: `name`, `nationality`.
- HATEOAS links included.

**POST /authors**
- Creates a new author.
- Requires authentication.
- HATEOAS links included.

**GET /authors/{id}**
- Retrieves an author by ID.
- HATEOAS links included.

### 3.3 Categories
**GET /categories**
- Returns a list of categories.
- HATEOAS links included.

**POST /categories**
- Creates a new category.
- Requires authentication.
- HATEOAS links included.

## 4. Functional & Non-functional Requirements
### Functional:
- CRUD operations for books, authors, and categories.
- Filtering, sorting, and pagination support.
- Secure access control for modifications.
- HATEOAS for API discoverability.

### Non-functional:
- API must follow RESTful principles.
- High availability and performance optimizations.
- Caching for frequent queries.
- JWT authentication with token expiration handling.

## 5. Richardson Maturity Model
- **Level 1**: Resources represented as URLs.
- **Level 2**: Proper HTTP methods (`GET`, `POST`, `PUT`, `DELETE`).
- **Level 3**: Full HATEOAS support for discoverability.

## 6. Error Handling
- `400 Bad Request` – Invalid input.
- `401 Unauthorized` – Authentication failure.
- `403 Forbidden` – Access denied.
- `404 Not Found` – Resource not found.
- `429 Too Many Requests` – Rate limit exceeded.
- `500 Internal Server Error` – Unexpected server issue.

## 7. Authentication & Authorization
- Uses JWT-based authentication.
- Admin roles required for write operations.
- Role-based access control (RBAC) is implemented.

## 8. Pagination
- Default: 10 items per page.
- Query params: `?page=1&size=10`.
- HATEOAS links provided for pagination.

## 9. Caching Strategy
- Books list cached using ETag and Last-Modified headers.
- Frequent GET requests use Redis caching.
- Cache invalidation upon updates.
- Explanation of non-cached endpoints included.

---
This API follows industry standards to ensure maintainability, scalability, and efficiency.

