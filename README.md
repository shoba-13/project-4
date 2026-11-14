# Blog Platform

A full-stack blog application where users can sign up, log in, write posts, browse all blogs, and open any single blog on its own page. Data is stored in **MongoDB** (or **Supabase**).

![Blog Platform banner](./blog-banner.svg)

## Key Objectives

1. Connect the application with MongoDB or Supabase.
2. Store user credentials and blog post data securely.
3. Retrieve and display all blogs from the database.
4. Create a page to view individual blog details.

## Features

- User registration and login
- Passwords hashed with bcrypt (never stored as plain text)
- JWT-based authentication for protected routes
- Create, edit and delete your own blog posts
- Home page listing all blogs, newest first
- Blog detail page at `/blog/:id`
- Responsive layout

## Tech Stack

| Layer     | Technology                                  |
|-----------|---------------------------------------------|
| Frontend  | React (or HTML/CSS/JS), React Router        |
| Backend   | Node.js, Express                            |
| Database  | MongoDB with Mongoose, or Supabase          |
| Auth      | bcrypt, JSON Web Tokens                     |

## Project Structure

```
blog-platform/
├── client/
│   └── src/
│       ├── pages/
│       │   ├── Home.jsx          # all blogs
│       │   ├── BlogDetail.jsx    # single blog
│       │   ├── Login.jsx
│       │   └── Register.jsx
│       └── App.jsx
├── server/
│   ├── models/
│   │   ├── User.js
│   │   └── Blog.js
│   ├── routes/
│   │   ├── auth.js
│   │   └── blogs.js
│   ├── middleware/auth.js
│   ├── config/db.js
│   └── server.js
├── .env.example
└── README.md
```

## Getting Started

### 1. Clone and install

```bash
git clone https://github.com/<your-username>/blog-platform.git
cd blog-platform

cd server && npm install
cd ../client && npm install
```

### 2. Configure environment variables

Create `server/.env` (see `.env.example`):

```env
PORT=5000
JWT_SECRET=replace_with_a_long_random_string

# Option A: MongoDB
MONGO_URI=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/blogdb

# Option B: Supabase
SUPABASE_URL=https://<project-id>.supabase.co
SUPABASE_KEY=<your-service-key>
```

Never commit `.env` to Git. Add it to `.gitignore`.

### 3. Run the app

```bash
# terminal 1
cd server && npm run dev

# terminal 2
cd client && npm start
```

Open `http://localhost:3000`.

## Database Design

**users**

| Field     | Type     | Notes                |
|-----------|----------|----------------------|
| _id       | ObjectId | primary key          |
| name      | String   |                      |
| email     | String   | unique               |
| password  | String   | bcrypt hash          |
| createdAt | Date     |                      |

**blogs**

| Field     | Type     | Notes                |
|-----------|----------|----------------------|
| _id       | ObjectId | primary key          |
| title     | String   |                      |
| content   | String   |                      |
| author    | ObjectId | references users     |
| createdAt | Date     |                      |

## API Endpoints

| Method | Endpoint             | Description              | Auth |
|--------|----------------------|--------------------------|------|
| POST   | `/api/auth/register` | Create an account        | No   |
| POST   | `/api/auth/login`    | Log in, receive a token  | No   |
| GET    | `/api/blogs`         | Get all blogs            | No   |
| GET    | `/api/blogs/:id`     | Get one blog             | No   |
| POST   | `/api/blogs`         | Create a blog            | Yes  |
| PUT    | `/api/blogs/:id`     | Update your blog         | Yes  |
| DELETE | `/api/blogs/:id`     | Delete your blog         | Yes  |

## Security Notes

- Passwords are hashed with bcrypt before saving.
- Secrets live in environment variables, not in code.
- Protected routes check the JWT and confirm the user owns the post.
- Input is validated on the server before it reaches the database.

## Screenshots

Add your screenshots here:

- Home page with all blogs
- Single blog page
- Login and register pages

## Future Improvements

- Comments and likes
- Image upload for posts
- Search and tags
- Pagination

## Author

**Your Name**
[LinkedIn](https://linkedin.com/in/your-profile) · [GitHub](https://github.com/your-username)
