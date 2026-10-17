# Speech Streaming and Text Alignment

I built this experiment to synchronize generated speech with visible text in Flutter. A LiveKit agent handles the conversation, while an ElevenLabs streaming relay sends audio and character timing data for highlighting.

**Built with:** Flutter, Dart, Python, FastAPI, WebSockets, LiveKit, OpenAI, ElevenLabs.

## What it does

- Stream generated speech to a Flutter client.
- Highlight text using character-alignment events.
- Coordinate microphone input and assistant speech.
- Inspect alignment output while developing the audio flow.

## Run locally

Install Flutter with Dart 3 and Python 3.10 or newer. From `server/`:

```bash
python -m venv .venv
```

Activate the environment with `.venv\Scripts\Activate.ps1` in PowerShell or
`source .venv/bin/activate` on macOS/Linux, then install dependencies:

```bash
python -m pip install -r requirements.txt
```

Keep real credentials in your local `.env`, which is ignored by Git. Copy the
provided `.env.example` into that directory as `.env` and fill in your own values. Set OpenAI, LiveKit, ElevenLabs, voice, and model values.

```bash
# Terminal 1, from server/
python tokenserver.py
```

```bash
# Terminal 2, from server/
python ws_server.py
```

From the repository root, in another terminal:

```bash
cd example
flutter pub get
flutter run -d chrome
```

The token endpoint starts `agent_direct.py`; the WebSocket relay listens on port 8081.

## Project layout

| Path | Purpose |
| --- | --- |
| `lib/src/` | Connection, streaming audio, and text highlighting |
| `example/` | Flutter voice and alignment demo |
| `server/tokenserver.py` | LiveKit tokens and agent startup |
| `server/agent_direct.py` | Conversation worker |
| `server/ws_server.py` | Speech WebSocket relay |
| `server/tts_streamer.py` | ElevenLabs streaming client |
| `docs/FIX_OVERLAPPING_AUDIO.md` | Audio synchronization notes |

## Backend details

See [server/README.md](server/README.md) for the local services and endpoints.
