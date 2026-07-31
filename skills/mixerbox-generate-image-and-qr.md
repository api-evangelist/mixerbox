---
name: Generate images and QR codes with MixerBox
description: Create images from text with ImageGen, upscale with PhotoMagic, and generate a QR code from a URL.
api: openapi/mixerbox-imagegen-openapi-original.json
operations: [imageGeneration, EnhanceResolution, generateQr]
method: generated
generated: '2026-07-20'
---

# Generate images and QR codes with MixerBox

Three independent MixerBox media plugins, each a GPT Action with `auth: service_http`.

## Steps

1. **Text-to-image** — call `imageGeneration` (`GET /api/gpt_plugins/image_gen` on `imagegen.mixerbox.com`) with the prompt; return the generated image URL(s). Respect the `Rules` schema the response includes.
2. **Upscale / enhance** — call `EnhanceResolution` (`GET /api/gpt_plugins/photo_magic/super_resolution` on `photomagic.mixerbox.com`) with the source image to super-resolve it.
3. **QR code** — call `generateQr` (`POST /api/gpt_plugins/qr/generate` on `qr.mixerbox.com`) with a valid URL.

## Rules

- `generateQr` returns HTTP 400 for an invalid URL — validate the URL scheme before calling and relay the error message if it fails.
- Return only image URLs the APIs produce; never fabricate an image link.
