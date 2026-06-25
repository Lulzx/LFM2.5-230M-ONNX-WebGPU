# LFM2.5-230M-ONNX WebGPU Demo

Run [LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M) (via its ONNX export) **entirely in the browser** using WebGPU + ONNX Runtime.

No server, no API keys — the model runs on your GPU (or falls back gracefully).

- **Model**: ~200 MB (Q4 quantized version)
- **Engine**: [@huggingface/transformers](https://huggingface.co/docs/transformers.js) (WebGPU backend)
- **Source ONNX**: [LiquidAI/LFM2.5-230M-ONNX](https://huggingface.co/LiquidAI/LFM2.5-230M-ONNX) (or your mirror at `lulzx/LFM2.5-230M-ONNX`)

## Live Demo

Open `index.html` in a modern browser (see requirements below), or visit the GitHub Pages deployment once enabled.

## How to Run Locally

1. Clone this repo
2. Open `index.html` directly in Chrome/Edge (or serve it):

```bash
# Simple local server (recommended for modules)
npx serve .
# or
python -m http.server
```

3. Click "Load Model & Generate" (first run downloads ~200 MB, then it's cached in your browser).

## Browser Requirements

- **Chrome 113+**, **Edge 113+**, or **Firefox Nightly** with WebGPU enabled
- Go to `chrome://flags/#enable-unsafe-webgpu` (or equivalent) and enable **WebGPU** + restart
- Verify at `chrome://gpu` (search for "WebGPU")

The first load will take time (downloading + compiling the model to WebGPU shaders). Subsequent runs are fast.

## Using the ONNX Model Directly

This demo uses the high-level `pipeline` API from Transformers.js, which handles tokenization, chat templating, and generation.

For lower-level control (custom KV cache, custom sampling, etc.) see the examples in the [ONNX model README](https://huggingface.co/LiquidAI/LFM2.5-230M-ONNX#webgpu-transformersjs).

The ONNX export was specifically built with WebGPU compatibility in mind (Q4 via `GatherBlockQuantized` + `MatMulNBits`, FP32 embeddings for quality, external data files, etc.).

## Customization

Edit `index.html`:

- Change the `modelId` to your own mirror: `lulzx/LFM2.5-230M-ONNX`
- Adjust generation parameters (`max_new_tokens`, `temperature`, `top_k`, `repetition_penalty`)
- Add system prompt / multi-turn chat support
- Switch `dtype` to `"fp16"` (higher quality, larger download, requires more VRAM)

## License

The model weights are under the [LFM 1.0 License](https://huggingface.co/LiquidAI/LFM2.5-230M-ONNX/blob/main/LICENSE).  
This demo code is provided under MIT (or same as parent ONNX repo).

## Related

- ONNX model: https://huggingface.co/LiquidAI/LFM2.5-230M-ONNX
- Original model: https://huggingface.co/LiquidAI/LFM2.5-230M
- Full inference guide + Python / WebGPU examples: see the ONNX repo README
- Exporter: https://github.com/Liquid4All/onnx-export

Enjoy running small powerful LLMs locally in the browser! 🚀
