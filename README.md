# Amazon-eBay Product Management System

A full-stack web application that bridges Amazon and eBay marketplaces, enabling automated product listing management, price calculations with markup, and ISBN-based product searches across both platforms.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This application automates the process of managing products between Amazon and eBay marketplaces. It allows users to:
- Search for products on eBay using ISBN numbers
- Automatically calculate Amazon prices with configurable markup percentages
- Manage product listings from a centralized dashboard
- Track product statuses and inventory
- Handle user authentication and authorization

## ✨ Features

### Product Management
- **ISBN-based Search**: Search eBay inventory using ISBN numbers
- **Automated Price Calculation**: Automatically calculate Amazon listing prices with customizable markup
- **Bulk Operations**: Process multiple ISBNs simultaneously
- **Product Tracking**: Monitor product status (stored, listed, sold)
- **Detailed Product Information**: Track comprehensive product details including:
  - Book metadata (title, author, publisher, year, pages)
  - Pricing and shipping information
  - Category and condition
  - Images and URLs

### User Management
- **Authentication System**: Secure JWT-based authentication
- **User Registration & Login**: Email-based user accounts
- **User Activation**: Admin-controlled user activation system
- **Role-based Access**: Protected routes for authenticated users

### Admin Dashboard
- **Amazon Product Management**: View and manage Amazon listings
- **eBay Product Management**: Browse and edit eBay products
- **User Administration**: Manage user accounts and permissions
- **Settings Configuration**: Configure markup percentages and ISBN lists
- **Pagination Support**: Efficient data browsing with pagination

### UI/UX Features
- Modern, responsive design with Tailwind CSS
- Real-time notifications
- Loading states and error handling
- Search and filter capabilities
- Excel export functionality

## 🛠 Tech Stack

### Backend
- **Framework**: FastAPI (Python)
- **Database**: PostgreSQL with SQLModel ORM
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcrypt
- **API Integration**: 
  - eBay API (OAuth 2.0)
  - Amazon Product Advertising API
- **CORS**: Enabled for frontend integration

### Frontend
- **Framework**: Next.js 14 (React 18)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **State Management**: Redux Toolkit
- **HTTP Client**: Axios
- **Icons**: Heroicons
- **Excel Export**: xlsx library

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher)
- **Python** (v3.10 or higher)
- **PostgreSQL** (v14 or higher)
- **Yarn** package manager
- **Git**

### API Credentials Required
- eBay Developer Account and API credentials
- Amazon Product Advertising API credentials

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd amazon_ebay
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
yarn install
```

## ⚙️ Configuration

### Backend Configuration

1. Create a `.env` file in the `backend` directory:

```env
# Database Configuration
POSTGRES_USER=your_db_user
POSTGRES_PASSWORD=your_db_password
POSTGRES_SERVER=localhost
POSTGRES_PORT=5432
POSTGRES_DB=amazon_ebay_db

# JWT Configuration
SECRET_KEY=your_secret_key_here
ACCESS_TOKEN_EXPIRE_MINUTES=11520

# API Configuration
API_PREFIX=/api/v1
```

2. Configure eBay API Credentials:
   - Add your eBay API credentials in `backend/app/token/ebay_oauth/`:
     - `ebay_apiuser.txt`: Your eBay API username
     - `ebay_apisecret.txt`: Your eBay API secret
     - `ebay_token_basic.txt`: Your eBay OAuth token

### Frontend Configuration

1. Create a `.env.local` file in the `frontend` directory:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

### Database Setup

```bash
# Create PostgreSQL database
createdb amazon_ebay_db

# The application will automatically create tables on first run
```

## 🏃 Running the Application

### Start Backend Server

```bash
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The API will be available at `http://localhost:8000`
API documentation (Swagger UI): `http://localhost:8000/docs`

### Start Frontend Development Server

```bash
cd frontend
yarn dev
```

The application will be available at `http://localhost:3000`

## 📚 API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/v1/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "secure_password",
  "full_name": "John Doe"
}
```

#### Login
```http
POST /api/v1/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "secure_password"
}
```

### Product Endpoints

#### Search Products by ISBN
```http
POST /api/v1/product/search
Authorization: Bearer <token>
Content-Type: application/json

{
  "isbns": ["9781234567890", "9780987654321"],
  "ebayMakeUp": 20,
  "amazonMakeUp": 15
}
```

#### Get All eBay Products
```http
GET /api/v1/product/get_ebay_all?page=1&per_page=10
Authorization: Bearer <token>
```

#### Get Single eBay Product
```http
GET /api/v1/product/get_ebay_item?itemId=<item_id>
Authorization: Bearer <token>
```

### User Management Endpoints

#### Get All Users
```http
GET /api/v1/user/all
Authorization: Bearer <token>
```

#### Update User Status
```http
POST /api/v1/user/allow
Authorization: Bearer <token>
Content-Type: application/json

{
  "email": "user@example.com",
  "is_active": true
}
```

## 📁 Project Structure

```
amazon_ebay/
├── backend/
│   ├── app/
│   │   ├── api_client/         # API integration modules
│   │   │   ├── amazon_api.py   # Amazon API client
│   │   │   └── ebay_api.py     # eBay API client
│   │   ├── routes/             # API route handlers
│   │   │   ├── main.py         # Main router
│   │   │   ├── product.py      # Product endpoints
│   │   │   └── user.py         # User endpoints
│   │   ├── token/              # OAuth token management
│   │   │   └── ebay_oauth/     # eBay credentials
│   │   ├── crud.py             # Database operations
│   │   ├── db.py               # Database connection
│   │   ├── main.py             # FastAPI application
│   │   ├── models.py           # SQLModel schemas
│   │   ├── settings.py         # Configuration
│   │   └── utils.py            # Utility functions
│   └── requirements.txt        # Python dependencies
│
├── frontend/
│   ├── src/
│   │   ├── app/                # Next.js app directory
│   │   │   ├── admin/          # Admin pages
│   │   │   │   ├── amazon/     # Amazon product management
│   │   │   │   ├── ebay/       # eBay product management
│   │   │   │   ├── settings/   # Settings configuration
│   │   │   │   └── user/       # User management
│   │   │   ├── auth/           # Authentication pages
│   │   │   │   ├── login/
│   │   │   │   └── register/
│   │   │   ├── layout.tsx      # Root layout
│   │   │   └── page.tsx        # Home page
│   │   ├── components/         # React components
│   │   │   ├── Amazon/         # Amazon-related components
│   │   │   ├── Ebay/           # eBay-related components
│   │   │   ├── common/         # Shared components
│   │   │   ├── Login/
│   │   │   ├── Register/
│   │   │   ├── Settings/
│   │   │   ├── Sidebar/
│   │   │   └── User/
│   │   ├── context/            # React context providers
│   │   ├── hooks/              # Custom React hooks
│   │   ├── lib/                # Utility libraries
│   │   └── type.tsx            # TypeScript types
│   ├── public/                 # Static assets
│   ├── package.json
│   └── tsconfig.json
│
└── README.md
```

## 📖 Usage Guide

### First Time Setup

1. **Register an Account**
   - Navigate to `/auth/register`
   - Fill in your details and create an account
   - Wait for admin approval (user activation)

2. **Admin Activation**
   - Admin logs in and navigates to User Management
   - Activates new user accounts

3. **Configure Settings**
   - Go to Admin > Settings
   - Add ISBN numbers to search
   - Set markup percentages for both platforms

### Searching for Products

1. Navigate to Settings > Add ISBN
2. Enter ISBNs (one per line or comma-separated)
3. Set eBay and Amazon markup percentages
4. Click Search
5. Products will be fetched from eBay and stored in the database

### Managing Products

1. **eBay Products**: Navigate to Admin > eBay to view all products
2. **Amazon Products**: Navigate to Admin > Amazon for Amazon listings
3. Use pagination to browse through products
4. Edit individual products by clicking on them
5. Export data to Excel for offline analysis

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guide for Python code
- Use TypeScript for all frontend code
- Write meaningful commit messages
- Add comments for complex logic
- Test your changes before submitting

## 🔒 Security Considerations

- Never commit `.env` files or API credentials
- Keep your eBay and Amazon API credentials secure
- Use strong passwords for database and JWT secret keys
- Regularly update dependencies to patch security vulnerabilities
- Implement rate limiting for API endpoints in production

## 🐛 Troubleshooting

### Common Issues

**Database Connection Error**
- Verify PostgreSQL is running
- Check database credentials in `.env`
- Ensure database exists

**eBay API Errors**
- Verify API credentials are correct
- Check token expiration
- Ensure proper OAuth flow

**Frontend Not Connecting to Backend**
- Verify backend is running on port 8000
- Check CORS settings in backend
- Verify `NEXT_PUBLIC_API_URL` in frontend `.env.local`

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

Your Name/Team Name

## 🙏 Acknowledgments

- FastAPI for the excellent backend framework
- Next.js team for the React framework
- eBay and Amazon for their APIs
- All contributors and users of this project

## 📞 Support

For support, email muhammadazlan@azlan.tech or open an issue in the repository.

---

**Note**: This is a development version. For production deployment, ensure proper security measures, environment configurations, and scalability considerations are implemented.
