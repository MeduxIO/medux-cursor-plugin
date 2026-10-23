---
name: medux-media
description: Use the Medux MCP tools to generate and edit video, images, speech and audio, clone voices, and convert documents. Use when the user asks for media generation or file conversion.
---

# Medux media workflow

Medux tools are asynchronous. Most generation tools return a `task_id`; poll it with `medux_task_query` until the status is `SUCCEEDED`, then use `output_url`.

## Local files
1. Call `medux_file_create_upload_url` with `media_type` (e.g. `AUDIO`) and `extension`.
2. HTTP PUT the raw file to the returned `upload_url` with a matching `Content-Type`.
3. Pass the returned `file.file_id` to the tool that needs the file.

## Voice cloning and speech
1. `medux_clone_voice` with the uploaded `file_id` returns a voice `asset_id`.
2. Wait for the clone task to succeed, then call `medux_speech_create_audio` with `voice_asset_id`.

## Notes
- Tasks consume credits; tell the user before running expensive video jobs.
- Image jobs can take several minutes. Keep polling instead of resubmitting.
