
# 🎵 Spotify to Setlist

This project extracts **BPM, key, duration, and energy** from **Spotify playlists or individual tracks** using the **Tunebat API**.

## 📌 Features
- Fetches **track metadata** from Spotify.
- Uses **Tunebat API** for **BPM, key, duration, and energy**.
- **Batch processing** with retry logic to handle API rate limits.
- **Submodule integration** for `tunebat-api`.

---

## 🚀 Installation & Setup

### **1. Clone the Repository**
Since `tunebat-api` is a **submodule**, clone the repository with: 

```bash
git clone --recurse-submodules https://github.com/YOUR_USERNAME/spotify-to-setlist.git
```
If you already cloned it without submodules, initialize it manually:
```bash
git submodule update --init --recursive
```

---

### **2. Install Dependencies**
Navigate to the project directory and install dependencies:

```bash
cd spotify-to-setlist
npm install
```

Inside the `tunebat-api` submodule, install its dependencies:
```bash
cd tunebat-api
npm install
cd ..
```

---

### **3. Set Up Spotify API Credentials**
You need **Spotify API credentials** to fetch track metadata.

1. Go to the **[Spotify Developer Dashboard](https://developer.spotify.com/dashboard/)**.
2. Create an **app** and note the **Client ID** and **Client Secret**.
3. Set them as environment variables:

   ```bash
   export SPOTIFY_CLIENT_ID="your_client_id_here"
   export SPOTIFY_CLIENT_SECRET="your_client_secret_here"
   ```

For persistent storage, add them to your `.bashrc`, `.zshrc`, or `.env` file.

---

### **4. Running the Script**
To extract metadata from a **Spotify playlist**:

```bash
node spotify_to_setlist.js --link "https://open.spotify.com/playlist/YOUR_PLAYLIST_ID"
```

To extract metadata from an **individual track**:

```bash
node spotify_to_setlist.js --link "https://open.spotify.com/track/YOUR_TRACK_ID"
```

---

## 📄 Output
The script generates a CSV file named **`setlist.csv`** with the following columns:

| Song | Artist | BPM | Key | Duration (ms) | Energy (%) |
|------|--------|-----|-----|--------------|-----------|
| Example Song | Example Artist | 120 | 8A | 180000 | 0.85 |

---

## ⚠️ Troubleshooting

### **1. Tunebat API Throttling**
If you get **"Throttled. Waiting X seconds..."**, the Tunebat API is rate-limiting requests.  
✅ **Fix:** The script automatically handles **retries with exponential backoff and jitter**. If throttling persists:
- Reduce `batchSize` in `spotify_to_setlist.js` (e.g., `batchSize = 3` instead of `5`).
- Add **longer delays** between batches in `processTracksInBatches()`.

### **2. Missing Spotify API Credentials**
If you see:
```
Failed to retrieve Spotify access token
```
✅ **Fix:** Ensure your **Client ID & Secret** are set correctly:
```bash
echo $SPOTIFY_CLIENT_ID
echo $SPOTIFY_CLIENT_SECRET
```

### **3. Submodule Issues**
If `tunebat-api` is missing:
```bash
git submodule update --init --recursive
```

---

## 🤝 Contributing
Feel free to fork, submit pull requests, or report issues.

---

## 📜 License
MIT License © 2024 ethan hsu
```

