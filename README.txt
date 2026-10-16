KRSS DIGITAL — SECURE AI CHAT BACKEND
====================================

WHAT IS INCLUDED
- KRSS Digital responsive website and AI chat interface.
- Node.js + Express backend. The OpenAI API key remains server-side.
- AI chat endpoint: POST /api/chat.
- Health endpoint: GET /api/health.
- Server-side owner login endpoints with signed HTTP-only session cookie.
- Owner session endpoints: POST /api/auth/login, GET /api/auth/me, POST /api/auth/logout.
- Input validation, JSON size limit, rate limits, security headers and safe error messages.
- Static file serving is restricted to the website page; server source and environment files are not served as static files.

REQUIREMENTS
- Node.js 20 or newer.
- An OpenAI API key with API access and billing enabled.
- A long random SESSION_SECRET.

LOCAL SETUP (WINDOWS)
1. Extract the ZIP.
2. Open Command Prompt or PowerShell in the extracted krss_ai_backend folder.
3. Run: npm install
4. Copy .env.example to a file named .env.
5. Edit .env privately. Set OPENAI_API_KEY to your real API key.
6. Set SESSION_SECRET to a long random secret (at least 32 random characters). Never share it.
7. Configure owner login values privately in .env:
   OWNER_CEO_ID=84694
   OWNER_CEO_PASSWORD=<set the CEO password privately>
   OWNER_CEO_NAME=Tiwari Amit
   OWNER_SECOND_ID=Palak Jaa
   OWNER_SECOND_PASSWORD=<set the second owner's password privately>
   OWNER_SECOND_NAME=Palak Jaa
   Do not put real passwords in index.html or upload .env to public repositories.
8. Run: npm start
9. Open http://localhost:3000
10. Open http://localhost:3000/api/health. aiConfigured and ownerLoginConfigured should be true.
11. Test a chat question and test both owner logins.

PRODUCTION DEPLOYMENT
- Deploy as a Node.js web service on Render, Railway or a VPS (not as a static-only site).
- Start command: npm start.
- Set OPENAI_API_KEY, SESSION_SECRET, owner IDs/passwords, NODE_ENV=production and any allowed origins in the host's private environment settings.
- Set ALLOWED_ORIGINS to the exact production origin(s), comma-separated, e.g. https://example.com,https://www.example.com.
- HTTPS is required in production; Secure is automatically added to the session cookie when NODE_ENV=production.
- Check /api/health after deployment. Configure spending limits with your AI provider.

IMPORTANT LIMITATIONS / REMAINING SETUP
- The AI will not answer until a valid API key and API access are configured.
- Owner login will not work until SESSION_SECRET and both owner accounts are configured in the private server environment.
- Contact form uses mailto and opens the visitor's email app. Set BUSINESS_EMAIL in index.html to the official business email. Enquiries are not stored server-side.
- Owner dashboard is currently a secure login/session shell only. Owner management, payment controls, enquiry storage and other business operations still need dedicated backend endpoints and a database.
- Rate limiting is in-memory per server process. Multi-instance deployments should use a shared rate-limit store and may need CAPTCHA/abuse monitoring.
- Chat history is not stored in a database. Messages are sent to the configured AI provider for processing; publish an appropriate privacy notice.
- Never ask customers for passwords, OTPs, API keys, card details or UPI PINs in the chat.
