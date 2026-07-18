# ChariSmart - Donation & Surplus Food Redistribution Network

ChariSmart is a Flask + SQLite System Analysis & Design Lab prototype for surplus-food redistribution. It connects restaurants, wedding halls and household donors with NGOs/orphanages and volunteer riders.

## Core workflow

1. A donor submits surplus food with quantity, expiry time, pickup window and pickup address.
2. An NGO/orphanage submits a food request with beneficiary group, required meals, delivery address and needed-before time.
3. An admin approves or rejects each donation/request.
4. **On approval or rejection, the system creates an in-app notification and sends an email. It can also send an SMS when Twilio is configured and the user provided a phone number.**
5. The admin can auto-match an approved donation with a same-area request, then assign a volunteer/rider.
6. The volunteer marks pickup and delivery; the recipient confirms delivery and may add a rating/note.

## Notification setup

Copy `.env.example` to `.env`. Do not upload `.env` to GitHub.

### Email via Gmail SMTP

Use these values in `.env`:

```env
NOTIFICATION_EMAIL_ENABLED=true
MAIL_SERVER=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your.email@gmail.com
MAIL_PASSWORD=your-16-character-app-password
MAIL_FROM=ChariSmart <your.email@gmail.com>
EMAIL_USE_TLS=true
EMAIL_USE_SSL=false
```

Use a Google App Password, not your normal Gmail password. After configuring it, approve or reject a donation/request from the Admin Dashboard. The registered user receives an email containing the decision and any optional rejection reason.

### Optional SMS via Twilio

```env
NOTIFICATION_SMS_ENABLED=true
SMS_PROVIDER=twilio
TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_FROM_NUMBER=+1XXXXXXXXXX
```

The registration phone field accepts a Bangladeshi number such as `017XXXXXXXX`; the system converts it to international `+88017XXXXXXXX` format for SMS delivery.

When credentials are not configured, the app prints the email notification to the terminal. This makes the notification workflow demonstrable without exposing credentials in the lab submission.

## Run locally

```bash
cd ChariSmart_notifications
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

pip install -r requirements.txt
copy .env.example .env   # Windows
# or: cp .env.example .env
python app.py
```

Open: `http://127.0.0.1:5000`

## Default login

```text
Admin email: admin@example.com
Admin password: admin123
```

## Demo seed data

Set this before first run if you want demo accounts:

```env
SEED_DEMO=true
```

## Security note

Never commit a real `.env` file. Use `.env.example` only for placeholders. SMS/email credentials must remain private.

## Documentation

The `/docs` folder contains the SAD Lab final report, SRS, test plan, diagrams and defense presentation.
