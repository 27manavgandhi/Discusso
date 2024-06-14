---

# Discusso

Discusso is a social discussion platform where users can create and engage in discussions through posts, comments, and interactions. The platform provides robust search functionality to find users and discussions based on text and hashtags. Users can follow each other, like posts and comments, and view the engagement metrics of their discussions.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Database Schema](#database-schema)
- [API Endpoints](#api-endpoints)
- [Setup Instructions](#setup-instructions)
- [Testing](#testing)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Features

1. **User Management**: Sign up, log in, update, delete, and search users.
2. **Discussions**: Create, update, delete, and search discussions by text and hashtags.
3. **Interactions**: Comment on posts, like posts and comments, and reply to comments.
4. **Follow System**: Follow and be followed by other users.
5. **Engagement Metrics**: View count of posts.
6. **Robust Search**: Find users and discussions using hashtags and text.

## Technology Stack

- **Backend**: Node.js with Express
- **Database**: MongoDB
- **Authentication**: JWT (JSON Web Token)
- **Storage**: AWS S3 for images
- **Frontend**: React.js (for Bonus UI)
- **API Testing**: Postman

## System Architecture

The system follows a microservice architecture to handle different functionalities. The services include:

- **User Service**: Handles user-related operations (create, update, delete, search).
- **Auth Service**: Manages user authentication and authorization.
- **Discussion Service**: Manages discussions (create, update, delete, search).
- **Interaction Service**: Manages likes, comments, and replies.
- **Search Service**: Facilitates searching users and discussions.

## Database Schema

### Users

- _id: ObjectId
- name: String
- mobile: String (unique)
- email: String (unique)
- password: String (hashed)
- followers: [ObjectId]
- following: [ObjectId]

### Discussions

- _id: ObjectId
- userId: ObjectId (reference to Users)
- text: String
- image: String (URL to S3)
- hashtags: [String]
- createdAt: Date
- viewCount: Number

### Comments

- _id: ObjectId
- discussionId: ObjectId (reference to Discussions)
- userId: ObjectId (reference to Users)
- text: String
- likes: [ObjectId] (reference to Users)
- replies: [ObjectId] (self-reference for nested comments)
- createdAt: Date

## API Endpoints

### User Service

- `POST /users`: Create User
- `PUT /users/:id`: Update User
- `DELETE /users/:id`: Delete User
- `GET /users`: List Users
- `GET /users/search`: Search Users by Name

### Auth Service

- `POST /auth/signup`: Signup
- `POST /auth/login`: Login

### Discussion Service

- `POST /discussions`: Create Discussion
- `PUT /discussions/:id`: Update Discussion
- `DELETE /discussions/:id`: Delete Discussion
- `GET /discussions/tags`: Get Discussions by Tags
- `GET /discussions/search`: Get Discussions by Text

### Interaction Service

- `POST /discussions/:id/comments`: Post Comment
- `PUT /comments/:id`: Modify Comment
- `DELETE /comments/:id`: Delete Comment
- `POST /comments/:id/like`: Like Comment
- `POST /comments/:id/reply`: Reply to Comment
- `POST /discussions/:id/like`: Like Post

## Setup Instructions

### Prerequisites

- Node.js
- MongoDB
- AWS S3 account (for image storage)

### Backend Setup

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/discusso.git
    cd discusso
    ```

2. Install dependencies:
    ```bash
    npm install
    ```

3. Set up environment variables in a `.env` file:
    ```plaintext
    MONGO_URI=your_mongo_uri
    JWT_SECRET=your_jwt_secret
    AWS_ACCESS_KEY_ID=your_aws_access_key_id
    AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key
    AWS_S3_BUCKET_NAME=your_s3_bucket_name
    ```

4. Start the server:
    ```bash
    npm start
    ```

### Frontend Setup (Bonus)

1. Navigate to the frontend directory:
    ```bash
    cd frontend
    ```

2. Install dependencies:
    ```bash
    npm install
    ```

3. Start the frontend server:
    ```bash
    npm start
    ```

## Testing

Use Postman to test the API endpoints. A Postman collection has been created to facilitate testing. Import the collection using the following link:

[Postman Collection](#)

## Documentation

Detailed documentation of each API endpoint, including request and response formats, can be found in the `docs` directory.

## Contributing

We welcome contributions! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
