# 🎙️ TaleTune

**Tell stories together, one voice at a time.**

TaleTune is a collaborative audio-storytelling mobile app. Friends join a room with a
6-digit code, take turns recording the lines of their characters while the script
highlights live (like lyrics in a karaoke app), then turn the whole story into a single
audiobook and share it on an Instagram-style feed.

## ✨ Features

- **Accounts & profiles** – email login, unique `@username`, photo and bio
- **Rooms** – create or join with a 6-digit code; members update in real time
- **Script engine** – paste a script (`Name: dialogue`), it is split into lines and characters, and the host assigns each character to a friend
- **Turn-based recording** – the current line is highlighted on every device; the person whose turn it is records, previews, re-records and sends
- **Listen together** – every recorded line can be played by everyone, plus "Play full story"
- **Audiobook** – all clips are merged into one audio with pauses between lines (Cloudinary transformations, chunked merge for long stories)
- **Publish with consent** – a story goes public only after every voice in the cast allows it
- **Social feed** – latest stories, likes, comments, follow/unfollow and a "Following" tab
- **Global mini player** – play, ⏪ 10s / 10s ⏩, seek bar, keeps playing while you browse
- **Lyrics view** – a full-screen player where the script scrolls and highlights in sync with the audio

## 🧱 Tech stack

| Area | Technology |
|---|---|
| App | React Native, Expo (SDK 57), Expo Router, TypeScript |
| Auth & database | Firebase Authentication, Cloud Firestore (real-time listeners, transactions) |
| Audio | `expo-audio` (recording, playback, seeking) |
| Media storage | Cloudinary (audio and images, unsigned uploads) |
| Merge server (optional) | Python, FastAPI, ffmpeg |

## 🗂️ Data model (Firestore)

```
users/{uid}                    profile, followersCount, followingCount
usernames/{username}           unique username → uid
users/{uid}/following|followers/{uid}
rooms/{code}                   host, members, status, characters, currentLineIndex, consent
rooms/{code}/lines/{n}         character, text, audioUrl, duration
posts/{id}                     title, audiobookUrl, author, cast, timeline, likesCount
posts/{id}/likes|comments/{id}
```

## 🚀 Getting started

```bash
git clone https://github.com/Pooja7345/taletune.git
cd taletune
npm install
cp .env.example .env     # then fill in your own keys
npx expo start
```

Create a Firebase project (Authentication → Email/Password, Firestore) and a free
Cloudinary account with an **unsigned** upload preset, then put the values in `.env`.

## 🔐 Security note

Firestore rules in this demo allow any signed-in user to read and write. Tighten them
(per-room membership, owner-only edits) before a public release.

## 🗺️ Roadmap

- [ ] Stricter Firestore security rules
- [ ] Import a story from PDF / Word / TXT
- [ ] AI assistant to play a character or write a story
- [ ] Search and notifications
- [ ] Android APK release

## 📸 Screenshots

_Add screenshots of: login, room with highlighted script, feed, lyrics player._

## 👩‍💻 Author

**Pooja Kumari** – [GitHub](https://github.com/Pooja7345) · [LinkedIn](https://www.linkedin.com/in/pooja-kumari-37b742220/)
