---
name: Question a PDF with MixerBox ChatPDF
description: Upload a PDF and ask questions against its contents using MixerBox ChatPDF.
api: openapi/mixerbox-chatpdf-openapi-original.json
operations: [uploadFile, queryFile]
method: generated
generated: '2026-07-20'
---

# Question a PDF with MixerBox ChatPDF

MixerBox ChatPDF ingests a PDF and answers questions grounded in it. Manifest declares `auth: service_http`. Base URL `https://chatpdf.mixerbox.com`, path prefix `/api/gpt_plugins/chat_pdf/`.

## Steps

1. **Upload the document** — call `uploadFile` (`POST /upload`) with the PDF URL/reference. Capture the returned document handle.
2. **Query the document** — call `queryFile` (`POST /query`) with the handle and the user's natural-language question; return the answer.

## Rules

- `uploadFile` returns HTTP 400 when the PDF is too large or has too many pages — surface that message to the user and ask for a smaller/split file rather than retrying identically.
- Ground answers only in `queryFile` output; do not invent content the API did not return.
