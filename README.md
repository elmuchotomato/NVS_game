# Last Orders — Pub Quiz

A multiplayer pub quiz game built with vanilla JavaScript and Firebase Realtime Database. Teams answer on their phones while the host controls the big screen. Scoring rules change between rounds with special twists like negative marking, wagers, speed rounds, and even a score-swap finale.

## Features

- **15 Questions** with point values from 100–500
- **8 Scoring Twists**: Speed Kills, Negative Marking, Double or Nothing (wagers), Lone Wolf, Underdog Uprising, Bounty on the Leader, The Great Swap, Last Orders finale
- **Real-time Sync** via Firebase — all devices stay in perfect sync
- **Beautiful UI** with pub quiz aesthetic (brass accents, dark felt baize colors)
- **Responsive Design** — works on big screens (host) and phones (teams)
- **Runs ~20 minutes** end-to-end

## Setup

### 1. Create a Firebase Project

1. Visit [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Create a new project** (or use an existing one)
3. Give it a name, then click **Continue**
4. Disable Google Analytics (you won't need it) and **Create project**

### 2. Create a Realtime Database

1. In your Firebase project, go to **Build** → **Realtime Database**
2. Click **Create Database**
3. Choose a location (e.g., Europe, US)
4. Start in **Test mode** (for development; production needs proper rules)
5. Click **Enable**

### 3. Get Your Config

1. Go to **Project settings** (gear icon, top left)
2. Click the **Your apps** section
3. Click **Web app** (or the `</>` icon)
4. Copy the config object that looks like:

```javascript
const FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "myproject.firebaseapp.com",
  databaseURL: "https://myproject-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "myproject",
  appId: "1:123456:web:abc123"
};
```

### 4. Paste into index.html

1. Open [index.html](index.html) in your editor
2. Find the `FIREBASE_CONFIG` object near the top (around line 44)
3. Replace all the `PASTE_ME` placeholders with values from your config
4. Save the file

### 5. Run It

1. Open [index.html](index.html) in a web browser
2. You should see the home screen asking to "Host the quiz" or "Join a game"
3. On the host screen, you'll get a 4-letter room code
4. On other devices/browsers, join with that code and a team name

## Playing a Round

### Host (Big Screen)

1. **Lobby** — Teams join using the room code
2. **Twist card** (optional) — Host shows the current round's twist, then clicks "Show the question"
3. **Question** — Host reads the question aloud, teams answer on their phones
4. **Reveal** — Host clicks "Reveal now" (or it auto-triggers when everyone answers or 25 seconds elapse)
5. **Scores update** — Correct answers are highlighted green, wrong ones fade out
6. **Next question** — Host clicks to move to the next round

### Team (Phone)

1. **Join** — Enter 4-letter code and team name
2. **Twist card** — Watch the rule change (if any); if wagering, pick a multiplier ×1, ×2, or ×3
3. **Answer** — When the question appears, tap your answer (A, B, C, or D)
4. **Lock in** — Your choice locks immediately; can't change it
5. **Reveal** — See if you got it right and how many points you scored
6. **Board** — Check your position on the leaderboard

## Scoring Twists Explained

| Twist | Effect |
|-------|--------|
| **Speed Kills** | First team to answer correctly scores double |
| **Negative Marking** | Wrong: −100 pts. Guessing becomes risky |
| **Double or Nothing** | Pick multiplier before seeing the question |
| **Lone Wolf** | Only team correct = triple points |
| **Underdog Uprising** | Bottom half of leaderboard scores double |
| **Bounty on the Leader** | Beat the leader and collect +150 bonus |
| **The Great Swap** | 1st and 2nd place swap scores (yes, really) |
| **Last Orders** | Final question, 500 pts, wager multiplier |

## Customization

- **Edit questions**: Modify the `QUESTIONS` array in `index.html`
- **Adjust timer**: Change `SECONDS = 25` to your preferred countdown
- **Add more twists**: Create new twist objects in the `TWISTS` object
- **Colors**: Edit the CSS variables in `:root` at the top of the style block

## Technical Details

- **Single HTML file** — no build step needed
- **Firebase Realtime Database** — real-time sync without polling
- **Vanilla JavaScript** — no frameworks, ~800 lines total
- **ES modules** — uses CDN imports for Firebase
- **Responsive CSS** — clamp() for fluid scaling, flexbox layout

## Notes

- **Test mode** database rules allow anyone to read/write. For production, implement proper Firebase rules.
- **Room codes** are random 4-letter codes (no vowels, to avoid awkward words)
- **Automatic reveal** triggers after 25 seconds OR when all teams answer
- **Connection loss** is gracefully handled; teams rejoin when connection restores

Enjoy your quiz night! 🍺📚

---

**Need help?**  
Check the Firebase console for any errors. Make sure your config is pasted correctly and your database is in Test mode (or has proper read/write rules for your use case).
