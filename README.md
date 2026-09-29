
> # Sprint 18 :  RapidDispatch

RapidDispatch is a refactored ShopIn backend focused on cleaner architecture, security, and a GraphQL API for more efficient client data fetching.

# **Codebase Audit**

* Booted the existing backend locally.
* Verified MongoDB connectivity.
* Reviewed backend routes, controllers, models, middleware, and configuration.
* Verified environment variables are loaded through `.env`.
* Checked the project with `npm audit`.

# **Legacy Refactoring**

Refactored large controller logic into reusable utility functions.

* Order calculation and validation moved to  -   `src/utils/orderUtils.js`
* Product sanitization and update handling moved to -  `src/utils/productUtils.js`
* User profile update handling moved to  -  `src/utils/userUtils.js`

This keeps controllers focused on HTTP requests and responses while reusable business logic stays separate.

# **GraphQL Migration**

Added Apollo Server and GraphQL alongside the existing REST API.

GraphQL endpoint:   `/graphql`

Current product queries include:

```graphql
query {
    products {
        title
        price
        image
    }
}
```

Clients can request only the fields they need:

```graphql
query {
    products {
        title
    }
}
```

This reduces unnecessary response data for clients such as mobile applications.

# **Tech Stack**

* Node.js
* Express
* MongoDB
* Mongoose
* Apollo Server
* GraphQL
* JWT
* Helmet
* CORS
* bcryptjs
* DOMPurify



# **Local Setup**

### *1. Clone the repository*

```bash
git clone <repository-url>
cd "Sprint 18 RapidDispatch/backend"
```

### *2. Install dependencies*

```bash
npm install
```

### *3. Configure environment variables*

Create a `.env` file inside `backend/`.

```env
PORT=4000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```

Do not commit `.env` to GitHub.

## *4. Start the backend*

```bash
npm start
```

The backend runs on:

```text
http://localhost:4000
```

Health check:

```text
http://localhost:4000/api/health
```

GraphQL:

```text
http://localhost:4000/graphql
```

## *GraphQL Example*

Request:

```graphql
query {
    products {
        title
        price
        image
    }
}
```

A client can also request only one field:

```graphql
query {
    products {
        title
    }
}
```

The response contains only the requested fields.

## *Security*

The backend uses:

* Helmet security headers
* JWT authentication
* Role-based authorization
* Password hashing with bcryptjs
* Input sanitization with DOMPurify
* Environment variables for secrets
* `.gitignore` protection for `.env`

## *Validation*

The project was tested locally with:

```bash
npm start
```

MongoDB connection:

```text
MongoDB connected
```

GraphQL endpoint:

```text
http://localhost:4000/graphql
```

Dependency audit:

```bash
npm audit
```

Result:

```text
found 0 vulnerabilities
```

# **Sprint 18 Outcome**   

Focuses on moving the existing backend toward a cleaner and more flexible API architecture without unnecessarily breaking the existing application.

The REST API remains available while GraphQL is introduced as the new targeted data-access layer.
