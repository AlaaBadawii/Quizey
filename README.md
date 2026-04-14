# Quizey

Quizey is a Flask-based quiz and exam API for teachers and students. It supports user registration and login, email verification, quiz creation, question banks, quiz attempts, answer submission, and quiz evaluation.

## What This Repository Contains

- A Flask application in `website/`
- Versioned API routes under `website/api/v1/routes/`
- SQLAlchemy models for users, quizzes, questions, attempts, answers, and question banks
- Alembic migration files in `alembic/`
- Endpoint reference in `endpoints_documentation.txt`

## Implemented Features

- User registration, login, profile update, profile deletion
- Email verification and password reset flows
- Teacher and student roles
- Quiz creation, update, deletion, publishing, and retrieval
- Multiple quiz types: `mcq`, `mixed`, `written`
- Multiple question types: `true_false`, `choose`, `written`
- Question bank creation and question reuse workflow
- Quiz attempts with submission and evaluation
- Attempt limits and participant limits
- Time-based quiz availability using start and end times

## Not Currently Implemented

The old README mentioned a few features that do not appear to be implemented in the current codebase:

- Shareable quiz links
- Leaderboards or ranking endpoints
- A fully built browser-facing website home page

The app currently exposes API endpoints, not a complete frontend experience.

## Project Structure

```text
Quizey/
├── README.md
├── endpoints_documentation.txt
├── alembic/
├── alembic.ini
└── website/
    ├── app.py
    ├── config.py
    ├── database.py
    ├── models.py
    ├── oauth2.py
    ├── requirements.txt
    ├── schema.py
    ├── utils.py
    ├── api/v1/routes/
    ├── static/
    └── templates/
```

## Requirements

- Python 3.10+
- PostgreSQL
- A `.env` file in the project root
- Google OAuth credentials for Gmail sending if you want registration verification and password reset emails to work

## Environment Variables

The application reads configuration from `.env`. These variables are required by `website/config.py`:

```env
database_hostname=
database_port=
database_password=
database_name=
database_username=
secret_key=
algorithm=
access_token_expire_minutes=
```

## Installation

1. Clone the repository:

```bash
git clone https://github.com/aligomaa56/Quizey.git
cd Quizey
```

2. Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

3. Install dependencies:

```bash
pip install -r website/requirements.txt
```

4. Create a PostgreSQL database and fill in the `.env` values.

5. Run the database migrations:

```bash
alembic upgrade head
```

6. Optional: set up Gmail API credentials if you want email verification and password reset emails to work.

- Create a Google Cloud project
- Enable the Gmail API
- Download OAuth credentials
- Place `credentials.json` in `website/`

## Running the App

Start the development server with:

```bash
python3 website/app.py
```

By default, Flask will run locally and expose API routes such as:

- `POST /api/v1/auth/register`
- `POST /api/v1/auth/login`
- `GET /api/v1/auth/users/<user_id>/profile`
- `POST /api/v1/views/users/<user_id>/quizzes`
- `POST /api/v1/views/users/<user_id>/quizzes/<quiz_id>/attempts`

This project is best tested with Postman, Insomnia, or `curl`.

## API Overview

Main API areas:

- Authentication
- User profile
- Quizzes
- Questions
- Quiz attempts
- Answers
- Question banks
- Attempt evaluation

For the endpoint list, see `endpoints_documentation.txt`.

## Notes

- Authentication uses bearer tokens.
- Many routes require an `Authorization: Bearer <token>` header.
- Some routes accept form data, especially authentication-related endpoints.
- Most quiz and question management routes expect JSON payloads.

## Contributing

Contributions are welcome. If you plan to contribute, please:

- Report bugs with reproduction steps
- Keep documentation aligned with code changes
- Update migration files when schema changes are introduced

## Contact

- Alaa Badawy: `alaa.badawy404@gmail.com`
- Ali Gomaa: `alielsayedgomaa@gmail.com`
