# TAAMS Analyzer V3

Version 3 has **no demo account or sample results**. It supports two modes:

- **TikTok connection:** read-only Login Kit / Display API connection with the user's explicit consent.
- **Manual:** type statistics or import CSV/JSON; no TikTok connection required.

Analysis is calculated in the browser. The Node server handles OAuth and TikTok API requests so the client secret and tokens are not placed in browser code. OAuth tokens are held in server memory only and are cleared when the server restarts; disconnecting revokes the TikTok access token.

## Run the manual analyzer on this PC

1. Install Node.js 18 or newer if it is not already installed.
2. Double-click `demarrer-v3.bat`.
3. In a browser, open `http://localhost:3000`.
4. Enter stats or import a CSV/JSON file, then select **Analyser mes données**.

The manual mode works without TikTok credentials or an internet connection. The TikTok sign-in button stays disabled until the server is configured.

## Enable official TikTok sign-in

TikTok requires an HTTPS callback, a registered developer app, and approval for the requested API products/scopes. A GitHub Pages site alone cannot run the OAuth server; deploy this Node app to a host that provides HTTPS, then use that host's domain below.

1. In [TikTok for Developers](https://developers.tiktok.com/), create an app and add **Login Kit** and **Display API**.
2. Register the exact HTTPS redirect URI:
   `https://YOUR-HOST/auth/tiktok/callback`
3. Request the read-only permissions `user.info.basic`, `user.info.stats`, and `video.list`. TikTok must approve the products/scopes before they can return protected data.
4. On the Node hosting provider, set these environment variables (do not share them in chat or commit them):
   - `PUBLIC_BASE_URL=https://YOUR-HOST`
   - `TIKTOK_REDIRECT_URI=https://YOUR-HOST/auth/tiktok/callback`
   - `TIKTOK_CLIENT_KEY=...`
   - `TIKTOK_CLIENT_SECRET=...`
   - `PORT` if required by the host
5. Deploy the project and open its HTTPS address. Click **Se connecter avec TikTok** and approve the requested read permissions.

For local manual use, no `.env` file is needed. For a deployment, copy `.env.example` to `.env` only if your host supports environment files; keep `.env` private. Never put the client secret in `app.js`, `index.html`, or GitHub Pages.

The connected account supplies recent public video counts through TikTok's official API. Follower growth over time is not returned by this API, so that field remains available for manual input/history. The report is an indicative TAAMS score, not an official TikTok metric.

## CSV import

Use `exemple-import.csv` as an empty header template. Required column: `views` or `vues`. Supported columns include `title`, `likes`, `comments`, `shares` and French equivalents.

## JSON import

```json
{
  "username": "@moncompte",
  "followers": 12500,
  "followerGrowth": 4.8,
  "period": "30 derniers jours",
  "videos": [
    {"title": "Ma vidéo", "views": 50000, "likes": 4200, "comments": 180, "shares": 90}
  ]
}
```

## Official technical references

- [TikTok Login Kit for Web](https://developers.tiktok.com/docs/en/login-kit-web)
- [TikTok Display API setup](https://developers.tiktok.com/docs/en/display-api-get-started)
- [TikTok API scopes](https://developers.tiktok.com/docs/en/tiktok-api-scopes)
- [TikTok token management](https://developers.tiktok.com/docs/en/oauth-user-access-token-management)

