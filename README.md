# recruiter-spam-filter

A Gmail add-on that automatically detects and archives recruiter outreach emails using an AI classifier. Built for tech professionals who are tired of recruiter spam flooding their inbox.

## How it works

1. Runs automatically on your Gmail account
2. Scans incoming emails and identifies recruiter outreach
3. Recruiter spam is labeled **"_RecruiterSpam"** and archived
4. Legitimate emails are never touched

## Tech Stack

```
recruiter-spam-filter
├── Google Cloud Project (GCP)
│   ├── Gmail API
│   └── Workspace Marketplace SDK
├── Google Apps Script
│   ├── Gmail integration (read, label, archive)
│   └── PropertiesService (local caching storage)
├── AI Classification
│   └── OpenAI API (gpt-4.1-nano)
└── Distribution
    ├── Google Workspace Marketplace
    └── GitHub Pages (landing page + privacy policy)
```

## Project Structure

```
├── Main.gs          # Core loop — checkNewEmails()
├── Classifier.gs    # OpenAI API call — classifyEmail()
├── Storage.gs       # spamIds/hamIds persistence
├── Setup.gs         # onInstall trigger creation
├── Config.gs        # Constants (API key, label, limits)
├── index.html       # Landing page (GitHub Pages)
└── privacy.html     # Privacy policy (GitHub Pages)
```

## Storage

Thread IDs are persisted between runs using Google's `PropertiesService`, scoped per script per user. This ensures each email thread is only sent to the AI classifier once, keeping API costs minimal.

## Developer Setup

1. Go to [script.google.com](https://script.google.com) and create a new project
2. Copy the `.gs` files into your project
3. Add your OpenAI API key to `Config.gs`
4. Create a Google Cloud project, enable the Gmail API and Workspace Marketplace SDK
5. Link the Apps Script project to your Cloud project (Project Settings → GCP Project)
6. Configure the OAuth consent screen (External, add your email as a test user)
7. Run `checkNewEmails()` manually to test, then set up a time-based trigger

## Privacy

Email subject lines and a portion of the email body are sent to a third-party AI API for classification only. No email content is stored or logged. See [privacy policy](https://williamzhai.github.io/recruiter-spam-filter/privacy.html) for full details.
