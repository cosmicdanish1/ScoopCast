This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
Got it! You're now building a community-driven movie/pop culture web app where:

Users can play games (Guess the Frame, Gaps, Curve, Eye, The Move, or Mixed).

Special users (with access) can contribute content (e.g., add new images, game rounds, etc.).

Game content includes:

Movie frame images

Cropped eye images

Curve/silhouette actor photos

Plot keywords

The entire frontend is in Next.js, with auth, profile customization, and AI profile pics.

Let me now give you EVERYTHING in detail – the final plan, sources, backend idea, and content management flow.

🧩 1. Game Types & Data Structure
🎥 Guess the Frame
Show a still frame from a movie.

User types the movie name.

Data needed:

Image URL

Correct movie title

Year (optional)

✅ Where to get images:

ShotDeck (best quality, needs approval)

MovieStillsDB (free w/ attribution)

Public domain movies (classic films)

Screenshots from YouTube trailers (for private/fair-use)

🧠 Gaps (Hangman-style Movie Name Guess)
Show blanks and let user guess one letter at a time.

Data needed:

Movie name

Hint (plot or genre)

✅ Where to get:

TMDB API

Use title and auto-generate hints using ChatGPT or a one-liner plot

🎭 Guess the Curve
Show a silhouette or high-contrast photo of an actor.

User guesses the actor.

Data:

Actor name

Curved image URL

✅ Where to get:

Scrape IMDb actor pages

Use Photoshop or filters (e.g., CSS filters or canvas) to apply "curve"

Use open-source celebrity face datasets (e.g., CelebA)

👁️ Guess the Eye
Show only the cropped eye of a celebrity.

Data:

Actor name

Cropped eye image

✅ Where to get:

Manually crop from high-res images (or automate via face detection)

Use datasets like CelebA

📖 The Move (Guess from Plot Keywords)
Show 3–5 keywords that represent a movie plot.

User guesses the movie.

Data:

Movie title

Plot keywords

✅ Where to get:

Use TMDB or OpenAI to extract keywords from summaries:

"Extract 5 main keywords from this movie plot..."

👥 2. Contributor Access (Game Builders)
You’ll support a Contributor Panel for trusted people who can add content.

🔐 Contributor Roles
Admin: Can edit/delete all content, approve contributions

Contributor: Can upload or create game content for approval

✅ Feature List
Upload frame images

Upload actor/eye images

Fill movie data (title, year, keywords)

Create game packs (e.g., 5 new Guess The Frame rounds)

🧱 Suggested Tech Stack
Frontend: Next.js (same project)

Backend:

Supabase (PostgreSQL + Auth + storage) OR Firebase

Auth roles via Supabase or Firebase Rules

Image storage in Firebase/Supabase buckets or S3

🗃️ 3. Database Structure (Simplified)
ts
Copy
Edit
// User
User {
  id
  name
  email
  role: 'user' | 'contributor' | 'admin'
  avatarUrl
  aiProfileUrl
}

// GameContent (generic for all game types)
GameContent {
  id
  type: 'frame' | 'gaps' | 'curve' | 'eye' | 'plot'
  title
  answer
  hint
  imageUrl
  options: { plotWords: [], letters: [], etc. }
  createdBy
  approved: boolean
}

// MixedGameSet
MixedGameSet {
  id
  name
  createdBy
  rounds: [GameContentId1, GameContentId2, ...]
}
📌 4. Final Roadmap (Revised with Contributor Support)
Phase 1–3:
✔️ Basic App Skeleton
✔️ Auth (Login/Signup)
✔️ Profile & Avatar
✔️ AI Profile Pic
✔️ Game Selector & Dummy Rounds

Phase 4: Game Types
🔄 Build each game (Guess the Frame, Gaps, etc.)
💾 Use static JSON or Supabase for questions

Phase 5: Contributor Panel
👤 Contributor login
🧾 Form to create game rounds
📷 Upload images to Firebase
📝 Submit new mixed mode sets
🛂 Admin approves

Phase 6: Multiplayer & Polish
🧑‍🤝‍🧑 4-player Socket.IO lobby
🎮 Real-time game syncing
🏆 Leaderboards
🎨 Framer Motion for transitions
🚀 Deploy to Vercel

✅ Summary: What To Work On First
Step	Feature	Description
✅ 1	app/ Folder	Set up basic routing for home, auth, game
✅ 2	Auth	Use NextAuth + MongoDB or Supabase
✅ 3	Profile UI	Avatar builder + AI pic
🔜 4	Game UI	Build static version of "Guess the Frame"
🔜 5	Contributor Panel	Form for uploading frame images and answers
🔜 6	Database	Use Supabase or Firebase to store game rounds
🔜 7	Mixed Mode	Combine rounds dynamically
🔜 8	Multiplayer	Real-time game syncing later
Would you like me to now:

Set up the Supabase schema for you?

Create the Contributor Dashboard UI scaffold?

Give you working code for a Guess the Frame page (static)?