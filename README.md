# Subscription Tracker

A subscription tracking application that allows users to log in, add subscriptions, and receive renewal reminder emails when their subscriptions are about to expire. Users are notified via email when their renewal date is 7, 5, 2, and 1 days away.

## Features
- User authentication with JWT tokens
- Secure API endpoints with Arcjet to prevent unauthorized access and spam
- Store user information and subscription data in MongoDB
- Automated email reminders using Upstash workflows
- Email notifications sent via Nodemailer

## Tech Stack
- **Backend:** Express.js
- **Security:** Arcjet
- **Database:** MongoDB
- **Authentication:** Custom JWT-based authentication
- **Workflow Automation:** Upstash
- **Email Service:** Nodemailer

## Installation & Setup

### Prerequisites
- Node.js installed on your machine
- MongoDB set up (local or cloud-based)
- Upstash account for workflow automation
- Arcjet account for endpoint protection

### Steps
1. Clone the repository:
   ```sh
   git clone https://github.com/your-username/subscription-tracker.git
   cd subscription-tracker
   ```

2. Install dependencies:
   ```sh
   npm install
   ```

3. Set up environment variables:
   Create two .env files based on environment as `.env.development.local` and `.env.production.local` in the root directory and add the following:
   ```env
   PORT = your_preferred_port
   SERVER_URL = your_server_url
   NODE_ENV = your_current_environment
   DB_URI = your_mongodb_connection_string
   JWT_SECRET = your_jwt_secret
   JWT_EXPIRES_IN = your_preferred_expiration_limit_of_JWT_TOKEN
   ARCJET_KEY = your_arcjet_key
   ARCJET_ENV = your_arcjet_environment
   QSTASH_URL = your_given_upstash_url
   QSTASH_TOKEN = your_given_upstash_token
   EMAIL_PASSWORD = your_app_password_from_gmail
   ```

4. Start the server:
   ```sh
   npm run dev
   ```

## API Endpoints

### Authentication
- **POST** `/api/v1/auth/sign-up` - Register a new user and receive a JWT token
- **POST** `/api/v1/auth/sign-in` - Login and receive a JWT token

### Subscriptions
- **GET** `/api/v1/subscriptions/user/:id` - Get all subscriptions for the logged-in user
- **POST** `/api/v1/subscriptions` - Create a new subscription 

### Users
- **GET** `/api/v1/users` - Get all users details
- **GET** `/api/v1/users/:id` - Get the user details

### Workflows
- **POST** `/api/v1/workflows/subscription/reminder` - Based on the renewal date of a subscription of a user this will trigger email to the user

## Email Reminders Workflow
Upstash is used to automate email reminders when a subscription is close to renewal. The workflow triggers emails at 7, 5, 2, and 1 days before expiration.

## License
This project is licensed under the MIT License.

