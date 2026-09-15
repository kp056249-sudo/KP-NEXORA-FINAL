# KP NEXORA — Local setup

1. Extract this ZIP into a **new folder**.
2. Open `start.bat`.
3. The launcher creates `.env` automatically if it does not exist.
4. Open `.env` and set your Groq key and Google Web OAuth client values.
5. `DATABASE_URL` may stay blank for local testing; the app uses SQLite.
6. `FLASK_SECRET_KEY` may stay blank; the app creates `.flask_secret` automatically. You may set your own secret instead.
7. Open `http://127.0.0.1:5000/setup-check` to verify configuration without exposing secrets.

## Google OAuth
Use a **Web application** OAuth client from the same Google Cloud project. Put these two URLs in **Authorized redirect URIs**:

- `http://127.0.0.1:5000/auth/google/callback`
- `http://127.0.0.1:5000/oauth/google/callback`

If you downloaded Google's OAuth client JSON, you can place it beside `app.py` as `google_client_secret.json`, `credentials.json`, or `client_secret.json`. The app can read the Web/installed client values from it.

If Google itself shows **Error 401: invalid_client / The OAuth client was not found**, this is a Google credential/client configuration problem, not a Flask database problem. Make sure the Client ID and Client Secret belong to the same active **Web application** OAuth client. A redirect URI problem normally produces a different `redirect_uri_mismatch` error.

## Groq AI
Set:

`GROQ_API_KEY=your_real_key`

`GROQ_MODEL=openai/gpt-oss-120b`

`GROQ_WEB_SEARCH=false`

The app shows explicit 401/429/400 Groq errors instead of a generic failure.
