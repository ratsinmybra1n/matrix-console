# Matrix Console

A Matrix-themed chat terminal that runs entirely in the browser. The language model runs locally on your GPU via [WebLLM](https://github.com/mlc-ai/web-llm) and WebGPU — no server, no API key, no data leaving your machine.

**Live demo:** https://ratsinmybra1n.github.io/matrix-console/

## Features

- Magenta digital-rain background rendered on `<canvas>`
- Boot animation with staggered blocks and a chime
- Streaming, token-by-token responses from an in-browser LLM
- Model cached in the browser after the first download
- On-page error log for failed requests

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

The model is set near the bottom of `index.html`:

```js
const MODEL_ID = "Qwen2.5-1.5B-Instruct-q4f16_1-MLC";
```

Any model from the [WebLLM prebuilt model list](https://github.com/mlc-ai/web-llm/blob/main/src/config.ts) can be used — smaller models load faster, larger ones answer better. The system prompt lives in `SYS_PROMPT` just above it.

## Deployment

This repo is plain static files and is served by GitHub Pages from the `main` branch root. Push to `main` and the site redeploys automatically.

## Notes

- WebGPU must be available. If the page reports it is missing, update your browser or try Chrome/Edge desktop.
- Conversation history lives in memory and resets on page reload.
- The model download happens once per browser; clearing site data re-downloads it.

## License

MIT
