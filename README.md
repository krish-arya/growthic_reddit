# Reddit Multi-Account Poster

A Streamlit-based web application for managing multiple Reddit accounts from a single interface.
The application supports creating posts, verifying subreddits, managing comments, fetching flairs, and scheduling comments, with optional Firebase-based authentication.

---

## Overview

This application is designed to simplify Reddit operations across multiple accounts. It provides a centralized interface for posting, moderation support, comment interaction, and scheduled engagement, making it suitable for automation, research, moderation, and content management workflows.

---

## Key Features

### Authentication

* Firebase email/password authentication
* Secure login using Firebase Admin SDK and Firebase REST API
* Demo mode fallback when Firebase is not configured

### Multi-Account Reddit Support

* Manage up to 30 Reddit accounts
* Account configuration via environment variables or Streamlit secrets
* Seamless switching between accounts

### Post Creation

* Text posts
* Link posts
* Image posts
* Optional flair application (template ID or custom text)
* NSFW and spoiler tagging
* Reply notification control

### Subreddit Utilities

* Verify subreddit existence and accessibility
* Retrieve subreddit metadata (subscriber count, description, NSFW status)
* Fetch available post flairs

### Post and Comment Management

* View recent posts for any account
* Filter posts by time range (day, week, month, all)
* Fetch comments for a specific post
* Reply to comments using a selected account

### Comment Scheduling

* Schedule comments for future posting
* Background execution using a scheduler thread
* View and cancel scheduled comment jobs

---

## Technology Stack

| Component      | Technology                            |
| -------------- | ------------------------------------- |
| User Interface | Streamlit                             |
| Reddit API     | PRAW                                  |
| Authentication | Firebase Admin SDK, Firebase REST API |
| Scheduling     | schedule, threading                   |
| Configuration  | python-dotenv, Streamlit secrets      |
| Logging        | Python logging                        |

---

## Project Structure

.
├── app.py
├── firebase-service-account.json (optional)
├── .env
├── requirements.txt
└── README.md

---

## Configuration

### Firebase Configuration (Optional)

#### Environment Variables

FIREBASE_WEB_API_KEY=your_firebase_web_api_key
FIREBASE_CREDENTIALS_PATH=/absolute/path/to/serviceAccount.json

#### Streamlit Secrets

[firebase]
type = "service_account"
project_id = "your-project-id"
private_key_id = "..."
private_key = "..."
client_email = "..."
client_id = "..."

---

### Reddit Account Configuration

The application supports configuration of up to 30 Reddit accounts.

#### Environment Variable Format

REDDIT_ACCOUNT_1_CLIENT_ID=xxxx
REDDIT_ACCOUNT_1_CLIENT_SECRET=xxxx
REDDIT_ACCOUNT_1_USERNAME=xxxx
REDDIT_ACCOUNT_1_PASSWORD=xxxx
REDDIT_ACCOUNT_1_USER_AGENT=your_app_name

Repeat the same pattern for additional accounts:

REDDIT_ACCOUNT_2_...
REDDIT_ACCOUNT_3_...
...
REDDIT_ACCOUNT_30_...

#### Streamlit Secrets Alternative

[reddit.account_1]
client_id = "..."
client_secret = "..."
username = "..."
password = "..."
user_agent = "..."

---

## Installation and Running

### Install Dependencies

pip install -r requirements.txt

### Run the Application

streamlit run app.py

---

## Application Workflow

1. User authenticates using Firebase or demo mode
2. Reddit accounts are loaded from environment variables or Streamlit secrets
3. The user can perform the following actions:

   * Create posts
   * Verify subreddits
   * Fetch subreddit flairs
   * View posts and comments
   * Reply to comments
   * Schedule comments

---

## Design Notes

* Account isolation is handled using numeric account IDs
* Restricted and private subreddits are handled gracefully
* Scheduling runs in a background thread to avoid blocking the UI
* Authentication is stateless and based on Firebase ID token verification
* Streamlit session state is used for UI persistence

---

## Limitations

* Scheduled comments may not execute reliably on platforms where the app can sleep (e.g., Streamlit Cloud)
* Reddit API rate limits apply per account
* Image posts require temporary file storage
* Scheduling uses the server’s local time

---

## Security Considerations

* Do not commit `.env` files or Firebase credentials to version control
* Use Streamlit Secrets for production deployments
* Use strong and dedicated Reddit credentials where possible

---

## Possible Enhancements

* Persistent job storage using a database (e.g., Firestore)
* Cron-based or distributed scheduling (e.g., APScheduler or Celery)
* Automatic retry handling for Reddit API rate limits
* Analytics and engagement tracking
* AI-assisted post and comment generation
