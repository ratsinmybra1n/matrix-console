# Matrix Console

A Matrix-themed chat terminal that runs in the browser and streams responses from a local [Ollama](https://ollama.com) model.

## Features

- Magenta digital-rain background rendered on `<canvas>`
- Boot animation with staggered blocks and a chime
- Streaming, token-by-token responses via Ollama's `/api/chat`
- Conversation history kept in memory for the session
- On-page error log for failed requests

## Requirements

- A modern browser
- [Ollama](https://ollama.com/download) installed and running (`ollama serve`)
- The model referenced in `index.html` pulled locally:

```sh
ollama pull qwen3.5:4b
```

## Run

Serve the folder over HTTP (opening the file directly with `file://` will break the CORS request to Ollama):

```sh
python -m http.server 8000
```

Then open <http://localhost:8000/>.

## Configuration

The model is set near the bottom of `index.html`:

```js
const MODEL = "qwen3.5:4b";
```

Change it to any model you have pulled (`ollama list`). The system prompt is defined in the same `sendMsg()` function.

## Notes

- Runs entirely against `http://localhost:11434`; nothing is sent to a remote server.
- Conversation history lives in memory and resets on page reload.

## License

MIT
