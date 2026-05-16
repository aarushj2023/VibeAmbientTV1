# VibeAmbient — Android TV Nature Ambient Display

Listens to room audio, identifies the music vibe (Chill / Party / Focus / Romantic / Dark), and shows matching **nature photography** with a slow Ken Burns effect on your TV — like a living painting that responds to music.

---

## What you need

| Service | What for | Free tier |
|---|---|---|
| **Unsplash** | Nature photos | 50 req/hour — plenty |
| ACRCloud | Song recognition | 10,000/month |
| Spotify | Mood analysis (valence, energy) | Unlimited |

Only Unsplash is strictly required. Without ACRCloud + Spotify, the display defaults to "Focus" nature photos.

---

## Step 1 — Get API keys

### Unsplash *(required)*
1. Sign up at https://unsplash.com/developers
2. Click **New Application** → accept guidelines → any name
3. Copy your **Access Key**

### ACRCloud *(recommended)*
1. Sign up at https://acrcloud.com (free tier)
2. Create project → **Audio & Video Recognition**
3. Copy **Host**, **Access Key**, **Access Secret**

### Spotify *(recommended)*
1. Go to https://developer.spotify.com/dashboard
2. Create an App → check **Web API**
3. Copy **Client ID** and **Client Secret**

---

## Step 2 — Build the APK

1. Install [Android Studio](https://developer.android.com/studio)
2. Unzip and open the `VibeAmbientTV` folder
3. Wait for Gradle sync (~2 min, needs internet)
4. **Build → Build APK(s)** → APK is at `app/build/outputs/apk/debug/app-debug.apk`

---

## Step 3 — Install on TV

```bash
# Enable Dev Options: Settings → Device Prefs → About → tap Build 7×
# Enable USB Debugging, note TV's IP address

adb connect YOUR_TV_IP:5555
adb install app-debug.apk
```

Or copy APK to USB drive and install via a file manager on the TV.

---

## Step 4 — Configure

Open **VibeAmbient** on TV → enter your keys → **Launch Ambient Mode**

The app listens every ~30 seconds. When a song is recognized, it crossfades to nature photos that match the mood. Each photo displays for ~20 seconds with a slow zoom/pan (Ken Burns).

---

## Vibe → Visual mapping

| Vibe | Nature imagery | Triggers |
|---|---|---|
| **Chill** | Misty forest, calm lake, meadow sunrise | Energy < 0.45, Tempo < 108 BPM |
| **Party** | Aurora borealis, tropical waterfall, coral reef | Energy > 0.72, Danceability > 0.65 |
| **Focus** | Mountain peaks, desert dunes, bamboo forest | Everything else |
| **Romantic** | Cherry blossom, lavender fields, golden beaches | Valence > 0.60, Energy < 0.55 |
| **Dark** | Stormy ocean, volcanic lava, lightning cliffs | Valence < 0.35, Energy > 0.48 |

---

## Screensaver

```
Settings → Device Preferences → Screen saver → VibeAmbient
```

---

## Troubleshooting

**Black screen / no images** — check your Unsplash Access Key in settings.

**Song label says "Listening…"** — ACRCloud or Spotify keys may be wrong, but photos still show based on ambient energy level.

**Mic permission denied** — Settings → Apps → VibeAmbient → Permissions → Microphone.
