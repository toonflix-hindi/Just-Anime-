# ToonFlix — JustAnime-inspired Firebase website starter

A responsive anime catalogue with home page, anime details, episode watch page, and Firebase-authenticated admin studio. This is an original design inspired by common anime catalogue patterns; it does not copy JustAnime's proprietary assets or source code.

## Included
- `index.html`: homepage, search, trending cards, latest episodes
- `anime.html`: anime details and episode list
- `watch.html`: episode page with authorized embed URL
- `admin.html`: Firebase email/password login, anime CRUD, episode/source management, site settings
- `assets/firebase-config.js`: Firebase web config (database URL already filled in)
- Responsive CSS and demo catalogue for preview

## Firebase setup (required for admin writes)
The previous Firebase Realtime Database URL you shared was recovered from your earlier chat and is prefilled:
`https://anistreamx-903a-default-rtdb.firebaseio.com/`

1. Open Firebase Console → Project settings → General → Your apps. Register a Web app if needed.
2. Copy the web app config and replace `apiKey`, `messagingSenderId`, and `appId` in `assets/firebase-config.js`. Verify the project ID and auth domain match your Firebase project.
3. Authentication → Sign-in method → enable **Email/Password**.
4. Authentication → Users → add your admin email and a strong password. Do not place the password in source code.
5. Realtime Database → Rules: review `firebase-rules.example.json` and publish equivalent rules. The example allows public reads but requires a signed-in user for writes. For a production site, consider restricting writes to an admin allowlist/claim rather than any authenticated account.
6. The first signed-in admin can manage catalogue, episodes, video URLs, and site settings.

**Important:** the web config is not an admin secret. Never publish Firebase service-account JSON, private keys, or admin passwords. Do not use open write rules such as `.write: true`.

## Deploy on GitHub Pages
1. Create a public GitHub repository.
2. Upload the contents of this folder (not the ZIP itself) to the repository root.
3. Repository → Settings → Pages → Deploy from a branch → `main` / root.
4. Open the published URL. Wait a minute or two for the first build.
5. For a custom domain, follow GitHub Pages' DNS instructions.

This project uses plain HTML/CSS/JavaScript, so no Node build step is needed.

## Before production
- Replace demo cards and sample image URLs with assets you have rights to use.
- Replace all placeholder video URLs with video/embed links you own or are authorized to distribute.
- Add your final Firebase web config.
- Review and tighten database rules; a public client can be inspected by anyone.
- For truly private admin-only operations or secrets, use a trusted backend/Cloud Functions. GitHub Pages is static hosting and cannot keep server secrets.
- If Firebase config is incomplete, the site still displays demo data; admin login/database writes will not work until configured.

## Data paths
- `/catalogue/anime/{animeId}`
- `/catalogue/anime/{animeId}/episodes/{episodeId}`
- `/catalogue/episodes/{episodeId}`
- `/catalogue/settings`

The public pages listen to `/catalogue/anime` and `/catalogue/settings` for realtime updates.
