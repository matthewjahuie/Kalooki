# 🃏 Kalooki — Progressive Family Edition

A real-time multiplayer Progressive Kalooki card game built with React + Firebase. Play across Jamaica 🇯🇲, Canada 🇨🇦, and Japan 🇯🇵!

## Rules at a Glance

| Round | Cards | Contract |
|-------|-------|----------|
| 1 | 9 | 3 Sets of 3 |
| 2 | 10 | 2 Sets of 3 + 1 Run of 4 |
| 3 | 11 | 1 Set of 3 + 2 Runs of 4 |
| 4 | 12 | 3 Runs of 4 |
| 5 | 12 | 4 Sets of 3 |
| 6 | 13 | 3 Sets of 3 + 1 Run of 4 |
| 7 | 14 | 2 Sets of 3 + 2 Runs of 4 |
| 8 | 15 | 1 Set of 3 + 3 Runs of 4 |
| 9 | 16 | 4 Runs of 4 |

- **Set** = 3+ cards of same rank
- **Run** = 4+ consecutive cards of same suit
- **Joker** = wild card (costs 50 points if left in hand)
- **Black Ace** = 1 point | **Red Ace** = 15 points
- **Face cards** = 10 points each
- **Lowest score** after 9 rounds wins
- **Call Kalooki** = go out with your entire hand at once → others get **double points**
- **Call Button** = first player to tap grabs the discarded card

---

## Setup

### 1. Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com) and create a new project
2. Enable **Realtime Database** (in Build → Realtime Database)
   - Choose a region close to you
   - Start in **test mode** (or add these security rules):
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
3. Go to **Project Settings** → **General** → scroll to "Your apps"
4. Click **Add app** → Web → Register it
5. Copy your Firebase config values

### 2. Local Development

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/kalooki-game.git
cd kalooki-game

# Install dependencies
npm install

# Create your .env file
cp .env.example .env
# Edit .env and fill in your Firebase values

# Start dev server
npm run dev
```

Open `http://localhost:5173/kalooki-game/` in your browser.

### 3. Deploy to GitHub Pages

#### One-time GitHub setup:

1. Push your code to GitHub
2. Go to your repo → **Settings** → **Secrets and variables** → **Actions**
3. Add these repository secrets (one by one):
   - `VITE_FIREBASE_API_KEY`
   - `VITE_FIREBASE_AUTH_DOMAIN`
   - `VITE_FIREBASE_DATABASE_URL`
   - `VITE_FIREBASE_PROJECT_ID`
   - `VITE_FIREBASE_STORAGE_BUCKET`
   - `VITE_FIREBASE_MESSAGING_SENDER_ID`
   - `VITE_FIREBASE_APP_ID`
4. Go to **Settings** → **Pages** → Source: **GitHub Actions**
5. Make sure `vite.config.js` has `base: '/YOUR_REPO_NAME/'`

Every time you push to `main`, it auto-deploys. Your game will be at:
`https://YOUR_USERNAME.github.io/kalooki-game/`

---

## How to Play

1. **Host** creates a room and shares the room code
2. **Other players** join using the room code
3. **Host** starts the game when everyone is in (2–6 players)
4. Each round:
   - Draw a card from the deck or take the discard pile
   - Optionally **Open** (lay down your contract melds) or **Call Kalooki** (entire hand at once)
   - If you've opened, lay off cards onto existing melds
   - Discard one card
   - When you discard, the **CALL button** lights up for everyone else — first to tap gets it!
5. Round ends when someone goes out (or calls Kalooki)
6. Scores are tallied — lowest total after Round 9 wins!

---

## Tech Stack

- **React** + **Vite**
- **Firebase Realtime Database** (real-time sync across countries)
- Deployed via **GitHub Actions** to **GitHub Pages**
- No server needed — fully serverless!
