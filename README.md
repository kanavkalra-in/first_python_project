# FastAPI Application

A clean, well-structured FastAPI application with example routes and best practices.

## Project Structure

```
app/
├── __init__.py
├── main.py                 # Main FastAPI application
├── api/
│   ├── __init__.py
│   └── v1/
│       ├── __init__.py
│       ├── router.py       # Combines all v1 routes
│       ├── routes/         # API route handlers
│       │   ├── __init__.py
│       │   ├── items.py    # Items CRUD endpoints
│       │   └── users.py    # Users CRUD endpoints
│       └── services/       # Business logic layer
│           └── __init__.py
└── core/
    ├── __init__.py
    └── config.py           # Application configuration
```

## Features

- ✅ Clean project structure
- ✅ API versioning (v1)
- ✅ CORS middleware configured
- ✅ Environment-based configuration
- ✅ Example CRUD endpoints (Items & Users)
- ✅ Pydantic models for request/response validation
- ✅ Health check endpoint
- ✅ Auto-generated API documentation

## Installation

1. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Running the Application

### Method 1: Direct execution
```bash
python app/main.py
```

### Method 2: Using uvicorn
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Method 3: As a module
```bash
python -m app.main
```

## API Documentation

Once the server is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc
- **OpenAPI JSON**: http://localhost:8000/openapi.json

## API Endpoints

### Root & Health
- `GET /` - Welcome message
- `GET /health` - Health check

### Items API (`/api/v1/items`)
- `GET /api/v1/items` - Get all items
- `GET /api/v1/items/{item_id}` - Get item by ID
- `POST /api/v1/items` - Create new item
- `PUT /api/v1/items/{item_id}` - Update item
- `DELETE /api/v1/items/{item_id}` - Delete item

### Users API (`/api/v1/users`)
- `GET /api/v1/users` - Get all users
- `GET /api/v1/users/{user_id}` - Get user by ID
- `POST /api/v1/users` - Create new user

## Configuration

Configuration is managed through environment variables in `app/core/config.py`:

- `PROJECT_NAME` - Application name
- `PROJECT_VERSION` - Application version
- `API_PREFIX` - API route prefix (default: `/api/v1`)
- `HOST` - Server host (default: `0.0.0.0`)
- `PORT` - Server port (default: `8000`)
- `DEBUG` - Debug mode (default: `False`)
- `CORS_ORIGINS` - Allowed CORS origins (default: `*`)

You can create a `.env` file or set environment variables directly.

## Adding New Routes

1. Create a new route file in `app/api/v1/routes/`:
```python
from fastapi import APIRouter

router = APIRouter()

@router.get("/")
async def my_endpoint():
    return {"message": "Hello"}
```

2. Import and include it in `app/api/v1/router.py`:
```python
from app.api.v1.routes import my_route

api_router.include_router(my_route.router, prefix="/my-route", tags=["my-route"])
```

## Next Steps

- Add database integration (SQLAlchemy, MongoDB, etc.)
- Add authentication and authorization
- Add request validation and error handling
- Add logging
- Add unit tests
- Add Docker support

