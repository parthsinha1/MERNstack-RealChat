
# MERN Chat App



### Overview

The MERN Chat App is a full‑stack, real‑time chat application built using the MERN stack (MongoDB, Express, React.js, and Node.js). The application enables users to register and authenticate, update their profile with Cloudinary‑stored profile pictures, and communicate instantly via real‑time messaging using Socket.io. The project uses RESTful APIs, secure JWT‑based authentication, and real‑time communication using a full‑stack development approach.
\
\
ι══════ι══════════════ι════════ιι══════ι══════════════ι════════ι
\
ι══════ι══════════════ι════════ιι══════ι══════════════ι════════ι
### TODO
- Implement group chat secret rooms functionality
- Allow uploads of larger file size for profile pics
- Implement custom themes feature
- Improve mobile responsiveness
_____________________________________________

### Live Demo
You can view the live version of the MERN Chat App deployed on Render here:

https://mernstack-realchatbot.onrender.com/

Simply click the link above to interact with the app in a live environment.
_____________________________________________

### Deployment
For production deployment, the project is hosted on Render. The frontend is built as static files and served along with the Express backend. Ensure you set the necessary environment variables for production, such as your MongoDB connection string, Cloudinary configuration, and JWT secret. This setup allows for both your RESTful API and real‑time Socket.io functionalities to work seamlessly on a single server.
_____________________________________________

**Key Features**\
─────────────────────────────────────────────
- Real‑time messaging using Socket.io
- User authentication and account management with JWT tokens
- Profile picture upload and storage via Cloudinary
- MongoDB for storage of user accounts and messages
- Express for routing, middleware, and HTTP utilities
- React.js for UI designing + frontend
- CORS configuration for enabling client--server communication 

**Technology Stack**\
─────────────────────────────────────────────
- MongoDB -- NoSQL database used to store user and message data
- Express -- Backend framework for RESTful API routing and middleware
- Node.js -- JavaScript runtime for executing backend code
- React.js -- Front‑end library for building responsive user interfaces
- Socket.io -- Real‑time bidirectional communication between server and client
- Cloudinary -- Cloud-based service used for storing and managing profile images
- Additional libraries: dotenv for environment configuration, cookie-parser for handling cookies, nodemon for development hot-reloading, and multer (if used) for handling file uploads

**Project Structure**\
─────────────────────────────────────────────\
The project is organized into separate backend and frontend folders:

backend/\
└── src/\
├── controllers/     # Contains route controllers (e.g., message.controller.js, auth.controller.js)\
├── middleware/     # Contains authentication middleware and error handlers\
├── routes/        # Express route definitions (e.g., auth.route.js, message.route.js)\
├── lib/        # Database connection and utility modules\
├── index.js       # Express server entry point\
├── socket.js       # Sets up Socket.io for real‑time connectivity\
└── config/\
└── cloudinaryConfig.js  # Configuration for Cloudinary integration (upload presets, API key, etc.)

frontend/\
└── (React application)\
├── public/\
├── src/\
├── components/   # React components (chat interface, login forms, profile pages, etc.)\
├── hooks/  # Custom hooks for Socket.io events and API calls\
└── App.js  # Main application component and routing configuration\
└── package.json   # React project dependencies and scripts

**Installation and Setup**\
─────────────────────────────────────────────

Prerequisites:
- Node.js (v14 or later)
- npm or yarn package manager
- A MongoDB Atlas account (or local MongoDB instance)
- A Cloudinary account for managing profile pictures

Steps to Run Locally:

1.  Clone the repository:
    git clone [repository URL]
    cd [repository-folder]

2.  Backend Setup:
    
    Navigate to the backend folder:
    cd backend
    
    Install dependencies:
    npm install
    
    Create a .env file in the backend folder with required variables:
    
    PORT=5001\
    MONGO_URI=your-mongodb-connection-string\
    JWT_SECRET=your-secret-key\
    CLOUDINARY_CLOUD_NAME=your-cloudinary-cloud-name\
    CLOUDINARY_API_KEY=your-cloudinary-api-key\
    CLOUDINARY_API_SECRET=your-cloudinary-api-secret\
    NODE_ENV=development
    
    
    Run the backend server (development mode):
    npm run dev\
    (The server will start on the specified PORT and log connection info.)

4.  Frontend Setup:
    
    Navigate to the frontend folder:
    cd ../frontend
    
    
    Install dependencies:
    npm install
    
    
    Start the React development server:\
    npm start\
    (The application will open in your web browser at [http://localhost:5173](http://localhost:5173/).)

**Usage**\
─────────────────────────────────────────────
- Register a new account or log in with an existing account.
- Update your profile and upload a profile picture. The image is stored in Cloudinary, and its URL is saved in your MongoDB profile collection.
- Engage in real‑time messaging; once you're logged in, Socket.io connects your client to the server and maintains an active channel for sending and receiving messages.
- Online user status is updated in real‑time, letting you know when a contact comes online or disconnects.

**API Endpoints**\
─────────────────────────────────────────────\
The backend exposes several API endpoints, all of which require proper authentication (except login/registration):

Authentication (base URL: /api/auth)
- POST /api/auth/register -- Create a new user account (also supports profile picture uploads via Cloudinary)
- POST /api/auth/login   -- Authenticate an existing user
- GET /api/auth/logout   -- Log out the current user

User and Profile Management
- PUT /api/auth/profile -- Update user profile details and upload a new profile picture. The uploaded image is processed and stored via Cloudinary, and its secure URL is stored in the database.

Messages (base URL: /api/message or /api/messages)
- GET /users       -- Retrieve a list of available users (requires authentication)
- GET /:id        -- Retrieve chat messages exchanged with a given user
- POST /send/:id     -- Send a message to a user with the specified id

Real-Time Communication (Socket.io):
- Upon loading the chat application, the client automatically connects to the server using Socket.io.
- The server registers events such as "connection" and "disconnect" to maintain a mapping between user IDs and socket IDs, which is utilized for directly routing messages.
- Socket.io events enable immediate UI updates when new messages arrive or online user statuses change.

**Integration Details**\
─────────────────────────────────────────────

Cloudinary Integration
- Cloudinary is used for managing and serving profile images.
- When a user uploads a profile picture, the file is sent to an API endpoint that uses a Cloudinary wrapper (e.g., in cloudinaryConfig.js) to upload the image.
- Cloudinary returns a secure URL, which is then saved in the user's profile in MongoDB.
- This approach offloads image storage to Cloudinary, ensuring faster image retrieval and reduced server load.

Socket.io Integration
- Socket.io is set up in socket.js, where a new Socket.io server is created with CORS configured to allow requests from the frontend ([http://localhost:5173](http://localhost:5173/)).
- The same HTTP server is used to serve both Express routes and Socket.io endpoints, ensuring a single unified server for both RESTful API calls and real‑time communication.
- As soon as a client connects, Socket.io handles the handshake automatically, and the server maintains communication channels via a user-socket mapping for real‑time messaging functionality.

**Design Considerations**\
─────────────────────────────────────────────
- Security -- JWT-based authentication is used, with sensitive keys stored as environment variables.
- Cloud Storage -- Using Cloudinary for images ensures that large media files are handled by a service designed for that purpose, thereby keeping the backend light.
- Scalability -- The project's modular code structure enables future developments like group chats or new features with minimal codebase disruption.
- Real-Time Efficiency -- Socket.io allows persistent connections, ensuring that message delivery and online notifications are conducted in real-time.

**Testing and Deployment**\
─────────────────────────────────────────────
- Development mode leverages nodemon for automatic backend restarts on file changes.
- For production deployment, the frontend is built into static files served by Express (using the production environment configuration).
- Deployment can be performed on platforms such as Heroku, DigitalOcean, or any cloud provider by setting appropriate environment variables and serving both the API and the static React build.

**TODO**\
─────────────────────────────────────────────
- Implement group chat secret rooms functionality
- Allow uploads of larger file size for profile pics
- Implement custom themes feature
- Improve mobile responsiveness




