# archillect-cli

> songbird & izzy, 2026.

A command-line tool to download curated visual content from [archillect.com](https://archillect.com) — the AI-powered image curation blog by Murat Pak.

## Install

```bash
pip install requests
```

Then make the script executable and put it in your PATH:

```bash
chmod +x archillect-cli
ln -s $(pwd)/archillect-cli ~/.local/bin/archillect-cli
```

## Usage

```bash
# Download latest N posts
archillect-cli --latest 10

# Download to custom directory
archillect-cli --latest 5 --output ~/Pictures/archillect

# Download with metadata JSON files
archillect-cli --latest 20 --metadata

# Download a random post from the full collection (~410K posts)
archillect-cli --random

# Download specific post by ID
archillect-cli --id 410187

# Slow down requests (default 0.5s)
archillect-cli --latest 50 --delay 1.0
```

## How it works

Archillect hosts images on Tumblr (`66.media.tumblr.com`). This tool:

1. Fetches post IDs from archillect.com
2. Visits each post page to extract the `og:image` meta tag
3. Tries the raw Tumblr URL first, falls back to 1280px
4. Saves images + optional JSON metadata

## Output

```
archillect/
├── archillect_410187.jpg
├── archillect_410187.json
├── archillect_410186.jpg
└── ...
```

## Why

CLI is faster and more scriptable than browser automation. No puppeteer, no selenium — just HTTP requests. Works from cron, works in containers, works anywhere Python runs.

## License

MIT
