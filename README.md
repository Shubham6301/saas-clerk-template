TodoMaster - Role-Based Auth Todo App
TodoMaster is a powerful task management application built with Next.js, featuring role-based authentication using Clerk and a PostgreSQL database with Neon.

Getting Started
Prerequisites
Node.js (v14 or later)
npm (v6 or later)
A Clerk account (for authentication)
A Neon account (for PostgreSQL database)
Installation
Clone the repository:

git clone https://github.com/aryan877/todo-master.git
cd role-based-auth
Install dependencies:

npm install
Set up environment variables: Create a .env.local file in the root directory and add the following variables:

# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

# Neon Database
DATABASE_URL=your_neon_database_url

# Webhook Secret (for Clerk)
WEBHOOK_SECRET=your_webhook_secret
Set up the database:

npx prisma db push
Generate Prisma client:

npx prisma generate
Running the Application
To run the development server:

Open http://localhost:3000 with your browser to see the result.

Features
User authentication with Clerk
Role-based access control (Admin and User roles)
Todo management (Create, Read, Update, Delete)
Subscription-based todo limits
Admin dashboard for user management
Webhook Setup
This application uses a Clerk webhook to synchronize user data with the database. Specifically, it listens for the user.created event to create a corresponding user record in the database.

To set up the webhook:

Go to the Clerk Dashboard.
Navigate to the "Webhooks" section.
Click on "Add Endpoint".
Set the Endpoint URL to https://your-app-url.com/api/webhook/register (replace with your actual URL).
Under "Events", select "user.created".
Save the endpoint.
Copy the "Signing Secret" and add it to your .env.local file as WEBHOOK_SECRET.
The webhook handler is implemented in app/api/webhook/register/route.ts. It verifies the webhook signature and creates a new user record in the database when a user is created in Clerk.

@Codebase
Setting up an Admin User
To test the admin functionality, you need to manually set the user's role to "admin" in Clerk. Here's how to do it:

Log in to your Clerk Dashboard.
Go to the "Users" section.
Find the user you want to make an admin.
Click on the user to open their details.
Scroll down to the "Public metadata" section.
Add a new key-value pair:
Key: role
Value: admin
Save the changes.
