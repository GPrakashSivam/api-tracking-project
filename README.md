
# Scalable Tracking Number Generator API

This project is a RESTful API built with Django and Django REST Framework. It generates unique tracking numbers for parcels, ensuring scalability, efficiency, and high concurrency handling.

## Features

- Generates unique tracking numbers for parcels.
- Conforms to a specific regex pattern (`^[A-Z0-9]{1,16}$`).
- Supports scalability and high concurrency.
- Customizable via query parameters.

## Requirements

- Python 3.8 or higher
- Django 4.x
- Django REST Framework
- PostgreSQL (optional, for production)

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/GPrakashSivam/api-tracking-project.git
cd api-tracking-project
```

### 2. Set Up a Virtual Environment

Create a virtual environment to isolate your project dependencies:

```bash
python -m venv venv
```

Activate the virtual environment:

- **For macOS/Linux**:
  ```bash
  source venv/bin/activate
  ```
- **For Windows**:
  ```bash
  api-tracking-venv\scripts\activate
  ```

### 3. Install Dependencies

Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables (Optional)

Create a `.env` file in the root directory to store your environment variables:

```bash
touch .env
```

Add the following variables to your `.env` file:

```env
SECRET_KEY=your-secret-key
DEBUG=True
DATABASE_URL=sqlite:///db.sqlite3  # For local development using SQLite
```

Replace `your-secret-key` with a Django secret key. You can generate one using an online generator or by running:

```bash
python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
```

### 5. Apply Migrations

Run the migrations to set up your database:

```bash
python manage.py migrate
```

### 6. Create a Superuser (Optional)

If you want to access the Django admin interface, create a superuser:

```bash
python manage.py createsuperuser
```

Follow the prompts to set up the superuser account.

### 7. Run the Development Server

Start the Django development server:

```bash
python manage.py runserver
```

The API will be accessible at `http://127.0.0.1:8000/`.

## Usage

### API Endpoint

- **GET /api/next-tracking-number/**

#### Query Parameters

- `origin_country_id` (string): The order’s origin country code in ISO 3166-1 alpha-2 format (e.g., "MY").
- `destination_country_id` (string): The order’s destination country code in ISO 3166-1 alpha-2 format (e.g., "ID").
- `weight` (float): The order’s weight in kilograms, up to three decimal places (e.g., "1.234").
- `created_at` (string): The order’s creation timestamp in RFC 3339 format (e.g., "2024-09-03T12:34:56+08:00").
- `customer_id` (UUID): The customer’s UUID (e.g., "de619854-b59b-425e-9db4-943979e1bd49").
- `customer_name` (string): The customer’s name (e.g., "RedBox Logistics").
- `customer_slug` (string): The customer’s name in slug-case/kebab-case (e.g., "redbox-logistics").

### Example Request

```bash
curl "http://127.0.0.1:8000/api/next-tracking-number/?origin_country_id=MY&destination_country_id=ID&weight=1.234&created_at=2024-09-03T12:34:56+08:00&customer_id=de619854-b59b-425e-9db4-943979e1bd49&customer_name=RedBox%20Logistics&customer_slug=redbox-logistics"
```

### Example Response

```json
{
  "tracking_number": "A1B2C3D4E5F6G7H8",
  "created_at": "2024-09-03T12:34:56.789Z",
  "customer_slug": "redbox-logistics"
}
```

## Testing
### Test with Postman

You can test the API using [Postman](https://www.postman.com/):

1. Open Postman and create a new GET request.
2. Enter the following URL: `http://127.0.0.1:8000/api/next-tracking-number/`.
3. Add the required query parameters.
4. Send the request and inspect the response.

## Deployment

### Deploying to Heroku

1. Follow the [Heroku deployment guide](#step-by-step-heroku-deployment-guide) to deploy your project to Heroku.

### Environment Variables on Heroku

Make sure to set the following environment variables on Heroku:

```bash
heroku config:set SECRET_KEY='your-secret-key'
heroku config:set DEBUG=False
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
