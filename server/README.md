# Speech Streaming Backend

The backend connects a LiveKit conversation agent to an ElevenLabs speech relay.
See the [project README](../README.md) for full setup.

## Local services

| Process | Purpose | Default port |
| --- | --- | --- |
| `python tokenserver.py` | Issue LiveKit tokens and launch `agent_direct.py` | 8080 |
| `python ws_server.py` | Relay generated audio and character-alignment events | 8081 |

Run both commands from this directory in the same configured Python environment.
Copy `.env.example` to `.env` and set OpenAI, LiveKit, and ElevenLabs values.
Keep real credentials in the ignored `.env` file.

## Files

| File | Purpose |
| --- | --- |
| `agent_direct.py` | Microphone input, LLM responses, and speech requests |
| `ws_server.py` | WebSocket endpoints for agent and Flutter connections |
| `tts_streamer.py` | ElevenLabs streaming and character alignment |
| `file_logger.py` | Optional alignment/output logging |

The relay exposes `/client`, `/agent`, and `/stream_tts` WebSocket routes.
The token API exposes `/token`, `/health`, and `/debug`. Generated logs, PID
files, and room counters are ignored by Git.
