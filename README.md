# 🎵  youtc2  A dumb YouTube C2 (Command and Control) Using Music Genre Playlists

This project implements a dumb covert C2 (Command and Control) channel over YouTube by encoding the output of a payload within music genre playlists and video comments. It leverages the YouTube Data API and a large dataset of music video links, providing an inconspicuous channel for sending commands and receiving payload output.

---

## ⚠️ WARNING

This tool is intended **strictly for educational or authorized security testing purposes**. Unauthorized use of this software **may violate laws**. Always obtain proper permission before conducting any testing.

---

## 🧩 How It Works

- The main script (`testin.py`) uses **YouTube playlists** and **video comments** as a covert channel.
- It listens for **commands posted as comments** on videos (e.g., `shikyrun id`).
- When a command is detected, it **reverses** (executes) the command on the target system and captures the output.
- The output of the payload is **encoded** (e.g., base64-encoded) and posted back as a **reply comment** to the same video.
- Example output comment:
```
comment: key:b'WzEzMjk1LCAxMDg4NiwgMTEwOTUsIDExNTE5LCAxNDcxMSwgMTE1MTksIDk0NzksIDExMDk1LCAxNzBd'
cipher:['https://youtube.com/watch?v=38WDfmIOjg8', 'https://youtube.com/watch?v=h9gHfwrWfzA', 'https://youtube.com/watch?v=RvMliuVIUMw', 'https://youtube.com/watch?v=xLoAbDqOWcs', 'https://youtube.com/watch?v=6KLWw18Jwk8', 'https://youtube.com/watch?v=E-vGmZJuK5E', 'https://youtube.com/watch?v=nXOOrxdW7C8', 'https://youtube.com/watch?v=TETVNH3k8Ag', 'https://youtube.com/watch?v=WWmZZ6N8p78']
```
- You can **decode the payload output** later using the provided script (`youtc2_decode.py`) with the **same music genre playlists** to retrieve the original data.


---

## 🚀 Setup Instructions

### 1️⃣ Google Cloud Configuration

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a **new project** or select an existing one.
3. **Enable the YouTube Data API v3**.
4. Navigate to:
 - **APIs & Services → Credentials**
 - Click **"Create Credentials" → "OAuth client ID"**.
 - Choose **"Desktop app"** as the application type.
 - Download the file (`client_secret_XXX.json`) and **rename it to `client_secrets.json`**.
5. Under **OAuth consent screen**:
 - Select your project.
 - Add the Gmail account you will use to log in as a **Test User**.
 - Save the configuration.

---
## Proof of Concept (PoC) 
https://github.com/user-attachments/assets/b0cd9764-99dc-4f76-8b16-bcd26add57c5

---
### 2️⃣ Install Dependencies

The script will attempt to install required Python modules automatically:

```bash
python3 -m pip install google-auth-oauthlib google-auth google-api-python-client
```
Alternatively, manually install:

```bash
pip install google-auth google-auth-oauthlib google-api-python-client
```
### 3️⃣ Get Your OAuth Token 
Before running `testin.py`, generate the `token.json` file with the provided helper script: 
```bash
python3 youtc2_get_token.py
```
* Follow the prompts to log in and authorize the app.
* This will create a `token.json` file with your OAuth credentials.
### 5️⃣ Run the Tool 
```bash 
python3 testin.py
```
### 6️⃣ Using the Tool
* Log in to your Google account when prompted (OAuth flow).

* Post commands as comments on videos within the playlists (e.g., shikyrun id).

* The script reads these commands, executes them, and posts back the encoded output as a comment.

### 7️⃣ Decode the Payload Output
To decode the payload output from the comments:
```bash
python3 youtc2_decode.py
```
* It uses the same music genre playlists to decode the output back to its original form.

---

### 📝 Important Considerations
* ✅ Stealth: Leverages YouTube’s normal traffic to blend in.
* ✅ API Quotas: Be mindful of API usage to avoid detection or rate-limits.
* ✅ Legal Implications: Always obtain explicit authorization before using this tool in any environment.
* ✅ **Stealth**: Blends with normal YouTube traffic and behavior.  
* ✅ **Bi-directional Communication**: Commands **from** video comments, output **to** video comments.  
* ✅ **Obfuscation**: Encoded and disguised as music playlist data.


