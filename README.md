# wan-worker

Wan 2.2 image-to-video RunPod serverless worker (based on wlsdml1114/generate_video, ksampler branch).

Changes vs upstream:
- No RIFE frame interpolation (native 16 fps output; retiming happens in the edit).
- `seed` input is honoured (upstream ignored it).
- Defaults: 1024x576, 65 frames (~4 s).
- Output: uploads to S3-compatible storage (Cloudflare R2) when `S3_ENDPOINT`, `S3_BUCKET`, `S3_KEY`, `S3_SECRET` env vars are set and returns `video_url`; otherwise returns base64 `video`.
- Returns `seed`, `gen_seconds`, `bytes`; cleans temp files after each job.

Input: `image_url` | `image_base64` | `image_path`, `prompt`, `negative_prompt`, `width`, `height`, `length`, `seed`.
