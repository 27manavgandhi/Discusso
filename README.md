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

Here's a high-level system architecture diagram for the Twitter clone application built with Next.js, TypeScript, Tailwind CSS, and Firebase (Cloud Firestore and Cloud Storage):

```
+-------------------+
|   Client (Web)    |
+-------------------+
| Next.js           |
| TypeScript        |
| Tailwind CSS      |
| React Components  |
| State Management  |
| Authentication    |
| Real-time Updates |
+-------------------+
            |
            | HTTP(S)
            |
+-------------------+
|   Firebase        |
+-------------------+
| Authentication    |
|   - Google        |
|   - Email/Password|
|   - Other Providers
+-------------------+
            |
+-------------------+
| Cloud Firestore   |
+-------------------+
| - Users           |
| - Tweets          |
| - Trending Data   |
| - Real-time Updates
+-------------------+
            |
+-------------------+
| Cloud Storage     |
+-------------------+
| - Images          |
| - GIFs            |
+-------------------+
            |
+-------------------+
|   Twitter API     |
+-------------------+
| - Trending Data   |
+-------------------+
```

**Client (Web)**:
- The client-side application is built with Next.js, a React framework for server-side rendering (SSR) and static site generation (SSG).
- TypeScript is used for type-safe code and better developer tooling.
- Tailwind CSS is used for styling and building a responsive user interface.
- React components are developed for different UI elements like tweets, user profiles, sidebars, etc.
- State management is handled using React's built-in state management or a third-party library like Redux or MobX.
- Authentication is implemented using Firebase Authentication, allowing users to sign in with Google, email/password, or other providers.
- Real-time updates are handled using Cloud Firestore's real-time update capabilities, ensuring that changes in tweets, likes, retweets, and user profiles are reflected across connected clients in real-time.

**Firebase**:
- Firebase Authentication is used for user authentication, supporting Google sign-in, email/password authentication, and potentially other providers.
- Cloud Firestore is a NoSQL document database used for storing and retrieving application data, such as user profiles, tweets, and trending data.
- Cloud Firestore's real-time update capabilities are leveraged to provide real-time updates across connected clients.
- Cloud Storage is used for storing and serving user-uploaded images and GIFs associated with tweets.

**Twitter API**:
- The application can optionally fetch trending data from the Twitter API, which can be stored or cached in Cloud Firestore or an in-memory cache for display in the application.

The client application communicates with Firebase services (Authentication, Cloud Firestore, and Cloud Storage) over secure HTTP(S) connections. The client can also optionally communicate with the Twitter API to fetch trending data if required.

This architecture separates concerns by delegating different responsibilities to different components:
- The client application handles the user interface, state management, and real-time updates.
- Firebase Authentication manages user authentication and authorization.
- Cloud Firestore stores and retrieves application data, including user profiles, tweets, and trending data, and provides real-time updates.
- Cloud Storage stores and serves user-uploaded media (images and GIFs).
- The Twitter API (optional) provides trending data for display in the application.

This separation of concerns promotes modularity, scalability, and maintainability of the system. The architecture can be further extended or modified based on specific requirements, such as adding additional features, integrating with other services, or improving performance and security.

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
