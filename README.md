# Slawburger Inventory Management System

A comprehensive inventory management system for restaurants built with Flask and SQLite.

## Features

- **Inventory Management**: Track ingredient stock levels in real-time
- **Goods Inward**: Record incoming deliveries and update stock
- **Inventory Adjustments**: Log manual adjustments, waste, and consumption
- **Recipe Management**: Define recipes and track ingredient usage
- **Order Integration**: Sync with Toast POS system
- **History Tracking**: Complete audit trail of all transactions
- **Responsive Dashboard**: Modern glass-morphism UI

## Requirements

- Python 3.8+
- Flask 3.0.0
- Gunicorn 21.2.0
- SQLite3

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Initialize the database:
```bash
python -c "from src.database import init_db; init_db()"
```

3. Run the application:
```bash
python app.py
```

The app will be available at `http://localhost:5000`

## Deployment

### Render (Cloud Deployment)

The application is configured for Render deployment with:
- `Procfile` for process configuration
- Automatic database initialization on startup
- SQLite database stored in `data/` directory
- Logs stored in `logs/` directory

### Environment Variables

No environment variables are required for basic operation. For Toast API integration:
- Toast API credentials are loaded from `logs/toast_credentials.txt`

## Project Structure

```
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── Procfile                        # Render deployment config
├── src/
│   ├── database.py                # Database connection and initialization
│   ├── inventory_manager.py       # Core inventory operations
│   ├── goods_inward.py           # Receiving goods operations
│   ├── inventory_adjustment.py    # Adjustment operations
│   ├── toast_api.py              # Toast POS integration
│   ├── logger.py                 # Logging utility
│   └── config.py                 # Configuration
├── static/
│   ├── css/style.css             # Main styling
│   └── js/                        # Frontend JavaScript
├── templates/
│   └── index.html                # Main HTML template
├── data/                          # SQLite database storage
└── logs/                          # Application logs
```

## API Endpoints

### Inventory
- `GET /api/stock` - Get all stock items
- `GET /api/recipes` - Get all recipes
- `POST /api/ingredients` - Add new ingredient
- `PUT /api/ingredients/<id>` - Update ingredient
- `DELETE /api/ingredients/<id>` - Delete ingredient

### Goods Inward
- `POST /api/receive` - Record single delivery
- `POST /api/receive/bulk` - Record multiple deliveries

### Adjustments
- `POST /api/adjust` - Log adjustment
- `POST /api/waste` - Log waste (legacy)

### History & Reporting
- `GET /api/history` - Get recent transactions
- `GET /api/orders` - Get orders
- `GET /api/orders/<id>` - Get order details
- `GET /api/orders/stats` - Get order statistics

### Toast Integration
- `POST /api/sync/toast` - Preview sync with Toast
- `POST /api/sync/toast/confirm` - Confirm Toast sync
- `GET /api/toast/menu` - Get Toast menu
- `GET /api/menu/local` - Get local menu items

## Development

For local development with debug mode:
```bash
python app.py
```

The application runs on `http://localhost:5000` with auto-reload enabled.

## Production

For production deployment (e.g., on Render):
```bash
gunicorn -w 2 -b 0.0.0.0:$PORT app:app
```

The Procfile handles this automatically.

## License

Proprietary - Slawburger Restaurant Management System
