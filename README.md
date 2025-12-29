```markdown
# Reddit Multi-Account Poster

A Streamlit-based web application for managing multiple Reddit accounts from a single interface.  
The application supports creating posts, verifying subreddits, managing comments, fetching flairs, and scheduling comments, with optional Firebase-based authentication.

---

## Overview

This application is designed to simplify Reddit operations across multiple accounts. It provides a clean UI for posting, moderation support, comment interaction, and scheduled engagement, making it suitable for research, marketing, moderation, or automation workflows.

---

## Key Features

### Authentication
- Firebase Email/Password authentication
- Secure login using Firebase Admin SDK and Firebase REST API
- Fallback demo mode when Firebase is not configured

### Multi-Account Reddit Support
- Load and manage up to 30 Reddit accounts
- Account configuration via environment variables or Streamlit secrets
- Seamless account switching within the UI

### Post Creation
- Text posts
- Link posts
- Image posts
- Optional flair application (ID or custom text)
- NSFW and spoiler tagging
- Reply notification control

### Subreddit Utilities
- Verify subreddit existence and accessibility
- Retrieve subreddit metadata such as subscriber count and description
- Fetch available post flairs

### Post & Comment Management
- View recent posts from selected accounts
- Filter posts by time range (day, week, month, all)
- Fetch comments for a given post
- Reply to comments using any loaded account

### Comment Scheduling
- Schedule comments for future posting
- Background execution using a scheduler thread
- View and cancel scheduled comment jobs

---

## Technology Stack

| Component | Technology |
|--------|------------|
| UI | Streamlit |
| Reddit API | PRAW |
| Authentication | Firebase Admin SDK, Firebase REST API |
| Scheduling | schedule, threading |
| Configuration | python-dotenv, Streamlit secrets |
| Logging | Python logging |

---

## Project Structure

```

.
├── app.py
├── firebase-service-account.json   # Optional
├── .env                            # Environment variables
├── requirements.txt
└── README.md

````

---

## Configuration

### Firebase Configuration (Optional)

#### Environment Variables
```env
FIREBASE_WEB_API_KEY=your_firebase_web_api_key
FIREBASE_CREDENTIALS_PATH=/absolute/path/to/serviceAccount.json
````

#### Streamlit Secrets

```toml
[firebase]
type = "service_account"
project_id = "your-project-id"
private_key_id = "..."
private_key = "..."
client_email = "..."
client_id = "..."
```

---

### Reddit Account Configuration

The application supports up to 30 Reddit accounts.

#### Environment Variable Format

```env
REDDIT_ACCOUNT_1_CLIENT_ID=xxxx
REDDIT_ACCOUNT_1_CLIENT_SECRET=xxxx
REDDIT_ACCOUNT_1_USERNAME=xxxx
REDDIT_ACCOUNT_1_PASSWORD=xxxx
REDDIT_ACCOUNT_1_USER_AGENT=your_app_name
```

Repeat the pattern for:

```
REDDIT_ACCOUNT_2_...
REDDIT_ACCOUNT_3_...
...
REDDIT_ACCOUNT_30_...
```

#### Streamlit Secrets Alternative

```toml
[reddit.account_1]
client_id = "..."
client_secret = "..."
username = "..."
password = "..."
user_agent = "..."
```

---

## Installation & Running

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run the Application

```bash
streamlit run app.py
```

---

## Application Workflow

1. User authenticates via Firebase or demo mode
2. Reddit accounts are loaded from environment variables or secrets
3. The user can:

   * Create posts
   * Verify subreddits
   * Fetch flairs
   * View posts and comments
   * Reply to comments
   * Schedule comments

---

## Design Notes

* Account isolation is handled using numeric account IDs
* Restricted or private subreddits are handled gracefully
* Scheduling runs in a background thread to avoid blocking the UI
* Authentication relies on stateless Firebase ID token verification
* Streamlit session state is used for UI persistence

---

## Limitations

* On Streamlit Cloud, scheduled comments may not execute reliably due to app sleep behavior
* Reddit API rate limits apply per account
* Image posts require temporary file storage
* Scheduling uses the server’s local time

---

## Security Considerations

* Do not commit `.env` files or Firebase credentials to version control
* Use Streamlit Secrets for production deployments
* Use strong, app-specific Reddit credentials where possible

---

## Possible Enhancements

* Persistent scheduling using a database (e.g., Firestore)
* Cron-based or distributed schedulers (e.g., APScheduler, Celery)
* Automatic retry handling for Reddit API rate limits
* Analytics and engagement tracking
* AI-assisted post and comment generation

```
```
