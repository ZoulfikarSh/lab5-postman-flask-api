# Lab 5 – Flask User API + Postman

A Flask REST API that creates, reads, updates and deletes users in a SQLite database (`database.db`), tested with Postman.

## Run it

```bash
python -m venv venv
venv\Scripts\activate          # Windows  (macOS/Linux: source venv/bin/activate)
pip install -r requirements.txt
python app.py
```

The server starts on `http://127.0.0.1:5000` and creates `database.db` with the `users` table on first run.

## Endpoints

| Method | Endpoint | Database function | Description |
|---|---|---|---|
| GET | `/api/users` | `get_users()` | List all users |
| GET | `/api/users/<user_id>` | `get_user_by_id()` | Get one user |
| POST | `/api/users/add` | `insert_user()` | Add a user (JSON body) |
| PUT | `/api/users/update` | `update_user()` | Update a user (JSON body with `user_id`) |
| DELETE | `/api/users/delete/<user_id>` | `delete_user()` | Delete a user |

Example JSON body for add:

```json
{
    "name": "John Doe",
    "email": "jondoe@gamil.com",
    "phone": "067765434567",
    "address": "John Doe Street, Innsbruck",
    "country": "Austria"
}
```

For update, include `"user_id"` as well.

## Postman (graded exercise)

The `postman/` folder contains:

- `Flask_user_app.postman_collection.json` – the **Flask user app** collection with all 5 requests, each with a saved example response.
- `Flask_user_app.postman_environment.json` – the **Flask user app - Local** environment with `base_url = http://127.0.0.1:5000`. Every request uses `{{base_url}}`.

To use them: in Postman click **Import**, drop in both files, select the **Flask user app - Local** environment (top-right), start `python app.py`, and send the requests.

## Git workflow used

1. `main` – database code (`connect_to_db`, `create_db_table`, `insert_user`, `get_users`, `get_user_by_id`, `update_user`, `delete_user`).
2. `rest-api` branch – Flask REST endpoints added on top of the DB code, then the Postman collection.
3. `rest-api` merged back into `main`.
