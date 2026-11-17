# AI models

In-browser LLM models used by the chess-assist userscript for move-explanation
commentary. Loaded via [WebLLM](https://github.com/mlc-ai/web-llm) in the user's
browser — no external API calls, no API keys. First load downloads the full
model from this repo into IndexedDB; every reload after is instant from cache.

## Models

### `smollm2-360m/`
- **Source:** [mlc-ai/SmolLM2-360M-Instruct-q4f16_1-MLC](https://huggingface.co/mlc-ai/SmolLM2-360M-Instruct-q4f16_1-MLC)
- **Size:** ~200 MB (7 param shards + tokenizer + WASM runtime)
- **VRAM:** ~380 MB (WebGPU required)
- **Context:** 4096 tokens
- **WASM runtime:** `SmolLM2-360M-Instruct-q4f16_1-ctx4k_cs1k-webgpu.wasm`
  (sourced from [mlc-ai/binary-mlc-llm-libs](https://github.com/mlc-ai/binary-mlc-llm-libs/tree/main/web-llm-models/v0_2_48), WebLLM v0.2.48 ABI, compatible with web-llm 0.2.78)

Use the folder URL as the WebLLM `model` field; the runtime fetches
`ndarray-cache.json` and the `params_shard_N.bin` files relative to it.

Example WebLLM config:

```js
const appConfig = {
  model_list: [{
    model: 'https://raw.githubusercontent.com/ThatKidGlitchy/chess-engines/main/ai/smollm2-360m',
    model_id: 'SmolLM2-360M-Instruct-q4f16_1-MLC',
    model_lib: 'https://raw.githubusercontent.com/ThatKidGlitchy/chess-engines/main/ai/smollm2-360m/SmolLM2-360M-Instruct-q4f16_1-ctx4k_cs1k-webgpu.wasm',
    overrides: { context_window_size: 4096 },
  }],
};
```
