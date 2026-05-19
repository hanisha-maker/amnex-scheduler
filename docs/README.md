# Amnex Interview Scheduler

**Zero-install. No Python. No server. Runs from GitHub Pages.**

## Deploy in 3 steps

### Step 1 — Push to GitHub
1. Create a new **public** GitHub repository (e.g. `amnex-scheduler`)
2. Upload the `docs/` folder to the repository root
3. Go to **Settings → Pages → Source → Deploy from branch → `main` → `/docs`**
4. Your app will be live at: `https://yourusername.github.io/amnex-scheduler/`

### Step 2 — Set up EmailJS (sends all emails, free 200/month)
1. Go to [emailjs.com](https://emailjs.com) → Sign up free
2. **Add Email Service** → Connect Gmail → copy **Service ID**
3. **Create Email Template** × 3:
   - One for hiring manager slot request
   - One for candidate slot request  
   - One for confirmations (used for all confirmation emails)
   
   In each template, set the body field to: `{{html_body}}` (EmailJS will inject the full HTML)
   Set To Email: `{{to_email}}`, To Name: `{{to_name}}`
4. Copy all Template IDs
5. **Account → API Keys** → copy **Public Key**
6. Paste all keys into the app's **Setup & Config** page

### Step 3 — Set up Google Calendar API
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create project → Enable **Google Calendar API**
3. **Credentials → Create OAuth 2.0 Client ID → Web Application**
4. Add Authorized JS origins: `https://yourusername.github.io`
5. Add Authorized redirect URIs: `https://yourusername.github.io/amnex-scheduler/`
6. Copy **Client ID** → paste in app Setup page
7. Click **Sign in with Google** in the app → done

---

## How it works (no server needed)

```
HR opens app → fills form → clicks "Send to hiring manager"
       ↓
EmailJS sends email to Hiring Manager with 4-5 clickable slots
       ↓
HM clicks a slot → link opens app → auto-processes
       ↓
EmailJS sends email to Candidate with confirmed slot
       ↓
Candidate clicks to confirm → app creates Google Calendar event
       ↓
Confirmation emails sent to: Candidate + HM + ta@amnex.com + HRBP
All get Google Meet link + calendar invite
```

All data is stored in browser localStorage — no database needed.
