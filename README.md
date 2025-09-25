# Cookie Session Authentication

A Node.js/Express application demonstrating secure session-based authentication using cookies, MongoDB session storage, and bcrypt password hashing.

## 🔐 Features

- **User Registration**: Secure user registration with password hashing
- **Session-based Authentication**: Uses Express sessions with MongoDB storage
- **Cookie Management**: HTTP-only cookies for enhanced security
- **Password Hashing**: Bcrypt for secure password storage
- **Protected Routes**: Middleware-based route protection
- **MongoDB Integration**: User data and session storage

## 🏗️ Project Structure

```
cookie_session_auth/
├── app.js                 # Main application file
├── models/
│   └── User.js           # User model with password hashing
├── routes/
│   └── auth.js           # Authentication routes
├── package.json          # Dependencies and scripts
└── README.md            # This file
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v14 or higher)
- MongoDB running locally on `mongodb://127.0.0.1:27017`

### Installation

1. Install dependencies:
```bash
npm install
```

2. Start MongoDB service on your local machine

3. Run the application:
```bash
node app.js
```

The server will start on `http://localhost:3000`

## 📚 API Endpoints

### Authentication Routes

All authentication endpoints are prefixed with `/auth`:

#### Register User
```http
POST /auth/register
Content-Type: application/json

{
  "username": "your_username",
  "password": "your_password"
}
```

#### Login
```http
POST /auth/login
Content-Type: application/json

{
  "username": "your_username",
  "password": "your_password"
}
```

#### Logout
```http
GET /auth/logout
```

#### Get User Profile (Protected)
```http
GET /auth/profile
```
*Requires valid session cookie*

## 🧪 Testing with curl

### 1. Register a new user:
```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpass123"}'
```

### 2. Login (save cookies):
```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpass123"}' \
  -c cookies.txt
```

### 3. Access protected profile route:
```bash
curl -X GET http://localhost:3000/auth/profile \
  -b cookies.txt
```

### 4. Logout:
```bash
curl -X GET http://localhost:3000/auth/logout \
  -b cookies.txt
```

## 🔧 Configuration

### Session Configuration
- **Secret**: `mysecretkey` (change in production)
- **Duration**: 1 hour (3600 seconds)
- **HTTP-Only**: True (prevents XSS attacks)
- **Secure**: False (set to true in production with HTTPS)

### MongoDB Configuration
- **Database**: `sessionAuth`
- **Connection**: `mongodb://127.0.0.1:27017/sessionAuth`

## 📦 Dependencies

- **express** - Web application framework
- **mongoose** - MongoDB object modeling
- **express-session** - Session middleware
- **connect-mongo** - MongoDB session store
- **cookie-parser** - Cookie parsing middleware
- **bcryptjs** - Password hashing library

## 🔒 Security Features

- **Password Hashing**: Bcrypt with salt rounds (10)
- **HTTP-Only Cookies**: Prevents XSS attacks
- **Session Storage**: MongoDB-based session persistence
- **Secure Headers**: Can be enhanced with helmet.js
- **Input Validation**: Basic validation (can be extended)

## 🌟 Key Implementation Details

### Password Security
- Passwords are hashed using bcrypt before storage
- Salt rounds: 10 (good balance of security and performance)
- Password comparison uses bcrypt's secure compare function

### Session Management
- Sessions stored in MongoDB using connect-mongo
- Automatic session cleanup for expired sessions
- Session cookie named `connect.sid` by default

### Route Protection
- Middleware checks for `req.session.userId`
- Unauthorized access returns 401 status
- User data retrieved without password field

## ⚠️ Production Considerations

- Change the session secret to a strong, random value
- Set `cookie.secure: true` when using HTTPS
- Implement rate limiting for auth endpoints
- Add input validation and sanitization
- Use environment variables for configuration
- Implement CSRF protection
- Add proper error handling and logging
- Consider using helmet.js for security headers

## 📝 License

ISC

## 👨‍💻 Author

Educational project for microservice authentication concepts.