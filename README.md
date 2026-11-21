# VoiceAssistant

A small Python voice assistant. It listens through the microphone (Google Speech Recognition), answers with text-to-speech (gTTS), and reads your upcoming **Google Calendar** events.

## Setup

### 1. Install dependencies
```bash
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib \
            SpeechRecognition gTTS playsound==1.2.2 pyaudio
```
`pyaudio` needs the PortAudio library: on Windows `pip install pyaudio` usually works; on macOS run `brew install portaudio` first; on Ubuntu run `sudo apt install portaudio19-dev` first.

### 2. Create your own Google OAuth credentials (`credentials.json`)
The assistant needs read-only access to your calendar. You must create **your own** OAuth client; none is shipped with this repo.

1. Open https://console.cloud.google.com/ and create (or pick) a project.
2. **APIs & Services → Library** → enable **Google Calendar API**.
3. **APIs & Services → OAuth consent screen** → choose *External*, fill in the app name and your email, and add yourself under **Test users**.
4. **APIs & Services → Credentials → Create credentials → OAuth client ID** → application type **Desktop app**.
5. Click **Download JSON**, rename the file to `credentials.json`, and put it in the project folder next to `main.py`.

### 3. Run it
```bash
python main.py
```
On the first run a browser window opens asking you to sign in and allow calendar access. The resulting token is saved to `token.pickle` so you don't have to sign in again. If you change `SCOPES` in `main.py`, delete `token.pickle` and sign in again.

## ⚠️ Keep these files private
`credentials.json` (your OAuth client secret) and `token.pickle` (your personal access/refresh token) give access to your Google account. Both are listed in `.gitignore`. **Never commit them.**

> **Security note:** earlier versions of this repo contained a real `credentials.json` and `token.pickle`. They have been removed. If you used them, revoke the old access at https://myaccount.google.com/permissions and delete the old OAuth client in Google Cloud Console, then create new credentials as described above.

## Other scripts
- `SpeechRecognition.py`, `tryaudio.py`: microphone / speech-recognition experiments
- `WatsonSpeech.py`: records a 3-second `audio.wav` clip with PyAudio
- `recordandplay.py`: live microphone-to-speaker pass-through with PyAudio
