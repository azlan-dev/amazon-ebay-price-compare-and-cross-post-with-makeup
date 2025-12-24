# Amazon-eBay Product Management System

A full-stack application for managing product listings between Amazon and eBay marketplaces. Search eBay products by ISBN and automatically calculate Amazon prices with markup.

## 🚀 Features

- Search eBay products using ISBN numbers
- Automatic price calculation with customizable markup
- User authentication and authorization
- Admin dashboard for product and user management
- Bulk product processing
- Excel export functionality

## 🛠 Tech Stack

**Backend:** FastAPI, PostgreSQL, SQLModel, JWT Authentication  
**Frontend:** Next.js 14, TypeScript, Tailwind CSS, Redux Toolkit

## 📋 Prerequisites

- Node.js 18+
- Python 3.10+
- PostgreSQL 14+
- eBay API credentials
- Amazon API credentials

## ⚡ Quick Start

### 1. Clone Repository
```bash
git clone <repository-url>
cd amazon_ebay
```

### 2. Backend Setup
```bash
cd backend
python -m venv venv
venv\Scripts\activate  # Windows
pip install -r requirements.txt
```

Create `.env` file in `backend` directory:
```env
POSTGRES_USER=your_user
POSTGRES_PASSWORD=your_password
POSTGRES_SERVER=localhost
POSTGRES_PORT=5432
POSTGRES_DB=amazon_ebay_db
```

Add eBay credentials to `backend/app/token/ebay_oauth/`:
- `ebay_apiuser.txt`
- `ebay_apisecret.txt`
- `ebay_token_basic.txt`

### 3. Frontend Setup
```bash
cd frontend
yarn install
```

Create `.env.local` file in `frontend` directory:
```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

### 4. Run Application

**Backend:**
```bash
cd backend
uvicorn app.main:app --reload --port 8000
```

**Frontend:**
```bash
cd frontend
yarn dev
```

Visit: `http://localhost:3000`

## 📁 Project Structure

```
amazon_ebay/
├── backend/
│   ├── app/
│   │   ├── api_client/      # Amazon & eBay API clients
│   │   ├── routes/          # API endpoints
│   │   ├── token/           # OAuth credentials
│   │   ├── models.py        # Database models
│   │   ├── crud.py          # Database operations
│   │   └── main.py          # FastAPI app
│   └── requirements.txt
│
└── frontend/
    ├── src/
    │   ├── app/             # Next.js pages
    │   ├── components/      # React components
    │   ├── hooks/           # Custom hooks
    │   └── context/         # State management
    └── package.json
```

## 🔑 Key API Endpoints

### Authentication
- `POST /api/v1/register` - Register new user
- `POST /api/v1/login` - User login

### Products
- `POST /api/v1/product/search` - Search products by ISBN
- `GET /api/v1/product/get_ebay_all` - Get all eBay products
- `GET /api/v1/product/get_ebay_item` - Get single product

### Users
- `GET /api/v1/user/all` - Get all users (admin)
- `POST /api/v1/user/allow` - Activate/deactivate user

## 📖 Usage

1. **Register** - Create account at `/auth/register`
2. **Wait for Activation** - Admin must activate your account
3. **Add ISBNs** - Go to Settings and add ISBN numbers
4. **Search Products** - Set markup percentage and search
5. **Manage Products** - View and edit products in Admin dashboard

## 🔒 Security Notes

- Never commit `.env` files or API credentials
- Use strong passwords for database and JWT
- Keep API tokens secure

## 📄 License

MIT License

## 💬 Support

Open an issue in the repository for questions or problems.

---

**API Documentation:** `http://localhost:8000/docs` (when backend is running)
