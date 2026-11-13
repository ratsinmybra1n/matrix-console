# Matrix Console

A Matrix-themed chat terminal that runs entirely in the browser. The language model runs locally on your GPU via [WebLLM](https://github.com/mlc-ai/web-llm) and WebGPU — no server, no API key, no data leaving your machine.

**Live demo:** https://ratsinmybra1n.github.io/matrix-console/

## Features

- Green digital-rain background rendered on `<canvas>`
- Boot animation with staggered blocks and a chime
- Streaming, token-by-token responses from an in-browser LLM
- Collapsible YouTube browser: search and play videos in a side panel
- Model cached in the browser after the first download
- On-page error log for failed requests

## YouTube browser

Click **YOUTUBE** in the header to open the side panel (or press `Esc` to close).

- Search runs through public Piped/Invidious instances — no API key. The page tries several instances and falls back automatically, and discovers more healthy Invidious instances at runtime.
- Paste a YouTube URL or an 11-character video ID and press **GO** to play it directly.
- Playback uses the official `youtube-nocookie.com` embed.
- Because these are community-run instances, search can occasionally fail or rate-limit; retry or paste a link if that happens.

## Requirements

- A WebGPU-capable browser (Chrome/Edge 113+, or another current Chromium-based browser)
- ~1.6 GB of GPU memory and a ~1 GB one-time model download
- Any static host (GitHub Pages, Netlify, `python -m http.server`, etc.)

## Usage

Open the live demo, or serve the folder locally:

```sh
python -m http.server 8000
```

Then open <http://localhost:8000/> and send a message. The first message downloads and loads the model; subsequent loads come from the browser cache.

## Configuration

The model picker in the header offers three sizes:

| Option | Model ID | First download | Notes |
| --- | --- | --- | --- |
| Fastest | `Qwen2.5-0.5B-Instruct-q4f16_1-MLC` | ~0.5 GB | Low-end GPUs |
| Balanced (default) | `Qwen2.5-1.5B-Instruct-q4f16_1-MLC` | ~1 GB | Good all-round demo |
| Stronger | `Qwen2.5-3B-Instruct-q4f16_1-MLC` | ~2 GB | Slower, better answers |

The choice is saved in `localStorage` (`matrix-model`) and remembered across visits. Edit the `MODELS` object near the bottom of `index.html` to add or remove entries — any model from the [WebLLM prebuilt model list](https://github.com/mlc-ai/web-llm/blob/main/src/config.ts) works. The system prompt lives in `SYS_PROMPT` just above it.

## Deployment

This repo is plain static files and is served by GitHub Pages from the `main` branch root. Push to `main` and the site redeploys automatically.

## Notes

- WebGPU must be available. If the page reports it is missing, update your browser or try Chrome/Edge desktop.
- Conversation history lives in memory and resets on page reload.
- The model download happens once per browser; clearing site data re-downloads it.

## License

MIT
