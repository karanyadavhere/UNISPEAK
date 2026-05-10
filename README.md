<div align="center">

<br/>

```
██╗   ██╗███╗   ██╗██╗███████╗██████╗ ███████╗ █████╗ ██╗  ██╗
██║   ██║████╗  ██║██║██╔════╝██╔══██╗██╔════╝██╔══██╗██║ ██╔╝
██║   ██║██╔██╗ ██║██║███████╗██████╔╝█████╗  ███████║█████╔╝ 
██║   ██║██║╚██╗██║██║╚════██║██╔═══╝ ██╔══╝  ██╔══██║██╔═██╗ 
╚██████╔╝██║ ╚████║██║███████║██║     ███████╗██║  ██║██║  ██╗
 ╚═════╝ ╚═╝  ╚═══╝╚═╝╚══════╝╚═╝     ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝
```

**Practice speaking through real interaction.**

[![Live Demo](https://img.shields.io/badge/Live-Demo-ff6a00?style=for-the-badge&logo=github&logoColor=white)](https://karanyadavhere.github.io/UNISPEAK/)
[![Firebase](https://img.shields.io/badge/Firebase-10.x-ff6a00?style=for-the-badge&logo=firebase&logoColor=white)](https://firebase.google.com/)
[![AI Integration](https://img.shields.io/badge/AI-Planned%20Integration-ff9a3b?style=for-the-badge&logo=openai&logoColor=white)](#-roadmap)
[![License](https://img.shields.io/badge/license-MIT-888?style=for-the-badge)](LICENSE)

<br/>

*A communication skill platform where people post, interact, and grow — with an AI coach always in your corner.*

<br/>

</div>

---

## 🗣️ What is UniSpeak?

UniSpeak is where communication practice actually happens — not in a textbook, not in a forced corporate training, but in a **live social feed** where you post short updates, get feedback from peers, and level up with an AI coach.

A blend of social interaction, communication practice, and AI-assisted learning. Built for students, professionals, introverts trying to find their voice, and anyone who knows that the way you speak changes everything.

> **"The way you communicate is the way the world sees you."**

---

## ✨ Features

### 🔥 Skill Feed
Post quick communication wins, questions, or updates. Like and comment in real-time — no refresh needed. Filter by topic to find what matters to you.

### 🤖 SpeakCoach AI
An always-on AI communication coach built right into the home page *(AI integration planned)*. Ask about:
- Public speaking confidence
- Job interview preparation  
- Structuring presentations
- Cutting filler words (*um*, *uh*, *like*)
- Assertiveness and persuasion

Accessible guidance whenever needed.

### ⭕ Speak Circles
Create or join topic-based communities — *Confident Presenters*, *Interview Prep Warriors*, *Pitch Practice* — and see who's actively engaged.

### 🎙️ Voice Posting
Draft posts hands-free with your microphone using the Web Speech API. Speak your thoughts; we'll transcribe them.

### 📊 AI Feedback Panel
Paste your draft, click **Analyze** — get instant clarity and confidence suggestions before you post. Clear and actionable communication insights.

### 📅 Daily Challenge
A fresh speaking prompt every day to keep your skills sharp. Use it as your post starter, or just practice solo.

### 🏅 Word of the Day
Expand your vocabulary with a new word each day — definition, part of speech, and a real example sentence.

---

## 🛠️ Tech Stack

| Layer | Tech |
|-------|------|
| **Frontend** | Vanilla HTML/CSS/JS — no framework, no build step |
| **Auth** | Firebase Authentication (email/password) |
| **Database** | Firebase Firestore (real-time listeners) |
| **AI Coach** | Planned AI integration (coach UI ready) |
| **Voice Input** | Web Speech API (browser-native) |
| **Fonts** | Syne (display) + DM Sans (body) via Google Fonts |
| **Hosting** | GitHub Pages |

Built as a lightweight single-file application for simplicity, portability, and fast deployment.

---

## 🚀 Getting Started

### Prerequisites
- A Firebase project with **Firestore** and **Authentication** enabled

### Setup

```bash
# Clone the repo
git clone https://github.com/karanyadavhere/unispeak.git
cd unispeak
```

**1. Configure Firebase**

Replace the `firebaseConfig` object in `index.html` with your own project credentials:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID"
};
```

**2. Configure Firestore Rules**

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /posts/{postId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow delete: if request.auth.uid == resource.data.userUid;
      allow update: if request.auth != null;

      match /comments/{commentId} {
        allow read: if true;
        allow create: if request.auth != null;
      }
    }
    match /profiles/{userId} {
      allow read: if true;
      allow write: if request.auth.uid == userId;
    }
    match /circles/{circleId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow update: if request.auth != null;
    }
    match /notifications/{notifId} {
      allow read: if request.auth.uid == resource.data.toUid;
      allow create: if request.auth != null;
    }
  }
}
```

**3. Open `index.html`**

```bash
# Serve locally (any static file server)
npx serve .
# or just open index.html in your browser
```

That's it. No build. No install. Just open and go.

---

## 📁 Project Structure

```
unispeak/
│
├── index.html          # The entire app — HTML, CSS, and JS in one file
├── README.md           # You're reading it
└── LICENSE             # MIT
```

UniSpeak is intentionally a single-file app. Every feature, every style, every interaction lives in `index.html`. This makes it dead simple to deploy anywhere, fork, remix, or hand off to someone else.

---

## 🗺️ Firestore Collections

| Collection | Purpose |
|------------|---------|
| `posts` | All feed posts with likes, author info, topic tag |
| `posts/{id}/comments` | Threaded comments on each post |
| `profiles` | User display name, accent color, score, level |
| `circles` | Community circles with member lists |
| `notifications` | Like/comment notifications per user |

---

## 🎨 Design System

UniSpeak uses a custom CSS design system built on CSS custom properties. The accent color is **user-customizable** — each user picks their color at signup and the whole UI shifts to match.

```css
--bg:          #080808    /* Near-black canvas */
--accent:      #ff6a00    /* Signature orange (user-controlled) */
--accent2:     #ff9a3b    /* Warm amber */
--text:        #f0ede8    /* Warm off-white */
--surface:     #111111    /* Card backgrounds */
--font-display: 'Syne'   /* Bold display headlines */
--font-body:    'DM Sans' /* Clean readable body */
```

---

## 🤝 Contributing

Got an idea? Found a bug? PRs are welcome.

1. Fork the repo
2. Create a branch: `git checkout -b feature/your-feature`
3. Make your changes in `index.html`
4. Open a pull request with a clear description

Please keep the single-file architecture intact for now. Big refactors are welcome in a discussion first.

---

## 📋 Roadmap

- [ ] Streak tracking and XP leveling system
- [ ] Audio recording and playback on posts
- [ ] Circle-specific chatrooms
- [ ] Weekly communication digest emails
- [ ] Public profile pages
- [ ] Mobile app (PWA wrapper)
- [ ] Moderation tools for circle owners

---

## 👥 Team

UniSpeak is built and maintained by a team of four:

| Name | Role |
|------|------|
| P KARAN SAI YADAV | Lead Developer & Designer |
| MD AYAZ KHAN | Testing & Debugging assistance |
| M V V SATHYANARAYANA | Feature discussions & Requirement analysis |
| R YUVA RAJ | UI feedback and Ideation |

---

## 📄 License

MIT — use it, fork it, build on it. Feel free to use, modify, and build upon this project.

---

<div align="center">

Built with 🧡 for anyone who wants to speak up and be heard.

**[karanyadavhere.github.io/UNISPEAK](https://karanyadavhere.github.io/UNISPEAK/)** &nbsp;·&nbsp; Built with Firebase and interactive communication-focused features

</div>
