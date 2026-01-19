**An LLM-powered Email Agent for Real-time Placement Alerts**

Inbox Sentinel AI is a background Python service that watches your email inbox and instantly notifies you when *your ID* appears in:

- Email subject or body  
- Excel attachments (`.xlsx`)  

It uses **Ollama (local LLM)** to:
- Understand which *company* the email is about  
- Perform intelligent checks on Excel files  
- Work fully offline and privately on your machine  

Designed especially for **placement and recruitment tracking**.

---

## Features

- Monitors **only today's unread emails**
- Can filter mails from **specific senders**
- Checks:
    - Email subject & body for your ID  
    - Excel attachments for your ID (exact + AI-based)
- Extracts **company name** using Ollama
- Sends **desktop notifications**
- Runs continuously in the background
- Keeps emails **unread** in Gmail
- Fully local & private (no cloud LLM)

---

## Requirements

- Python 3.9+
- Windows
- Ollama installed

Install dependencies:

```bash
pip install -r requirements.txt
Install and prepare Ollama:

```bash
ollama pull llama3
ollama serve
```

## Configuration

Edit these values in `mail_id_watcher.py`:

```python
EMAIL = "yourmail@gmail.com"
PASSWORD = "your_app_password"   # Gmail App Password
YOUR_ID = "NEO871540"
CHECK_INTERVAL = 120  # seconds
IMAP_SERVER = "imap.gmail.com"
```

**Note:** Use a Gmail App Password, not your normal Gmail password.

### Getting Your Gmail App Password

Gmail does not allow normal account passwords for scripts.
You must generate an App Password.

Steps:

Go to:
https://myaccount.google.com/security

Enable 2-Step Verification (if it is not already enabled)

After enabling 2-Step Verification, open:
https://myaccount.google.com/apppasswords

Under Select app → choose Mail

Under Select device → choose Windows Computer (or “Other” → type InboxSentinel)

Click Generate

Google will show a 16-character password like:

abcd efgh ijkl mnop
## Run

```bash
python mail_id_watcher.py
```

You will see:

```
ID Watcher started
Checking today's mail...
```

The script will now:
- Check today's unread mails
- Read subject & body
- Detect company using LLM
- Scan Excel attachments
- Notify you if your ID is found
- Repeat every CHECK_INTERVAL seconds

## Auto-Start on Windows

Create two files:

**start_ollama.bat**
```batch
@echo off
ollama serve
```

**run_watcher.bat**
```batch
@echo off
python D:\path\to\mail_id_watcher.py
```

Press `Win + R` → `shell:startup` and place both `.bat` files there.

Now your system will start automatically when the laptop boots.

## Example Notification

```
ID found in EXCEL!
Company: AMAZON
Subject: Amazon – Shortlist Round 1
```
