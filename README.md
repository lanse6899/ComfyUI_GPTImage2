# ComfyUI_GPTImage2

Custom nodes for ComfyUI that integrate the **gpt-image-2** image generation model through the [gpt-best API](https://gpt-best.apifox.cn/).

## Features

- **Text-to-Image** — generate images from text prompts via `/v1/images/generations`
- **Image-to-Image** — transform an existing image with text guidance via `/v1/images/edits`
- **Image Edit / Inpainting** — edit specific regions of an image using a mask via `/v1/images/edits`
- **Chat Completion** — send messages via `/v1/chat/completions` and get text replies

## Installation

1. Copy the `ComfyUI_GPTImage2` folder into your ComfyUI's `custom_nodes` directory:

   ```
   ComfyUI/
   └── custom_nodes/
       └── ComfyUI_GPTImage2/
           ├── __init__.py
           ├── nodes.py
           ├── config.json
           └── requirements.txt
   ```

2. Install dependencies:

   ```bash
   cd ComfyUI/custom_nodes/ComfyUI_GPTImage2
   pip install -r requirements.txt
   ```

3. **Configure your API credentials** by editing `config.json`:

   ```json
   {
     "base_url": "https://gpt-best.apifox.cn/v1",
     "api_key": "your_api_key_here"
   }
   ```

   Or set environment variables:

   ```bash
   export GPTIMAGE2_BASE_URL="https://gpt-best.apifox.cn/v1"
   export GPTIMAGE2_API_KEY="your_api_key_here"
   ```

4. Restart ComfyUI.

## Nodes

### GPTImage2 Text to Image

Generates images from a text prompt via `/v1/images/generations`.

| Parameter | Options | Default | Description |
|---|---|---|---|
| `prompt` | string | — | Text description of the image |
| `model` | `gpt-image-2`, `gpt-image-1.5`, `gpt-image-1` | `gpt-image-2` | Model to use |
| `quality` | `low`, `medium`, `high` | `medium` | Generation quality |
| `size` | `1024x1024`, `1024x1792`, `1792x1024`, `1536x1024`, `1024x1536` | `1024x1024` | Output resolution |
| `n` | 1–10 | `1` | Number of images to generate |
| `output_format` | `png`, `jpeg`, `webp` | `png` | Output image format |

### GPTImage2 Image to Image

Transforms an input image using a text prompt via `/v1/images/edits`, preserving image structure.

| Parameter | Options | Default | Description |
|---|---|---|---|
| `image` | IMAGE | — | Input image |
| `prompt` | string | — | Transformation instruction |
| `model` | `gpt-image-2`, `gpt-image-1.5`, `gpt-image-1` | `gpt-image-2` | Model to use |
| `input_fidelity` | `low`, `high` | `high` | How closely to preserve the input image |
| `quality` | `low`, `medium`, `high` | `medium` | Generation quality |
| `size` | `1024x1024`, `1024x1792`, `1792x1024`, `1536x1024`, `1024x1536` | `1024x1024` | Output resolution |
| `output_format` | `png`, `jpeg`, `webp` | `png` | Output image format |

### GPTImage2 Edit (Inpaint)

Edits specific regions of an image using a mask via `/v1/images/edits`. White areas in the mask indicate the regions to be replaced.

| Parameter | Options | Default | Description |
|---|---|---|---|
| `image` | IMAGE | — | Input image |
| `mask` | MASK | — | Grayscale mask (white = edit area) |
| `prompt` | string | — | Description of what to draw in the masked area |
| `model` | `gpt-image-2`, `gpt-image-1.5`, `gpt-image-1` | `gpt-image-2` | Model to use |
| `quality` | `low`, `medium`, `high` | `medium` | Generation quality |
| `size` | `1024x1024`, `1024x1792`, `1792x1024`, `1536x1024`, `1024x1536` | `1024x1024` | Output resolution |
| `output_format` | `png`, `jpeg`, `webp` | `png` | Output image format |

### GPTImage2 Chat

Sends a chat completion request via `/v1/chat/completions` and returns the assistant's reply.

| Parameter | Type | Default | Description |
|---|---|---|---|
| `prompt` | STRING | — | User message |
| `model` | STRING | `gpt-4o` | Model ID (e.g. `gpt-4o`, `gpt-3.5-turbo`) |
| `system_prompt` | STRING | `You are a helpful assistant.` | System prompt |
| `temperature` | FLOAT | `0.7` | Sampling temperature (0–2) |
| `max_tokens` | INT | `2048` | Max tokens to generate |
| `stream` | BOOLEAN | `False` | Enable streaming output |

## Getting an API Key

1. Sign up / log in at [gpt-best.apifox.cn](https://gpt-best.apifox.cn/).
2. Navigate to **API Keys** and create a new key.
3. Copy the Base URL and API Key into `config.json`.

## Troubleshooting

**"No images were returned from the API"**
- Verify your `api_key` is correct in `config.json`.
- Check that your account has sufficient credits.
- Make sure the `base_url` ends with `/v1`.

**Request timeout**
- Increase the `timeout` parameter in `nodes.py`, or check your network connection.

**Image dimensions mismatch (img2img/edit)**
- Ensure the input image and mask are valid PNG/RGB images. The API will auto-resize internally.
