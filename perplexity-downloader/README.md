# Perplexity Thread Downloader

A Claude Code skill for downloading and exporting Perplexity.ai conversation threads as Markdown files.

## Features

- **Single Thread Download** — Export one Perplexity thread by URL
- **Bulk Export** — Download multiple threads from a URL list
- **Full History Export** — Extract all threads from your Perplexity account history
- **Sequential Processing** — Downloads one thread at a time (not in parallel)
- **Individual Files** — Each thread becomes its own `.md` file
- **Structured Output** — Preserves questions, answers, follow-ups, and citations
- **Index File** — Automatic index generation for bulk/history exports

## Installation

1. In Claude Code, go to **Settings** → **Skills**
2. Click **Import** or **+** to add a custom skill
3. Select `perplexity-downloader.skill`
4. The skill is now available

## Usage

### Single Thread

Download one Perplexity thread:

```
/perplexity-downloader https://www.perplexity.ai/search/your-query
```

Or trigger naturally:
> "Download this Perplexity thread: [URL]"

### Bulk Download

Download multiple threads from a URL list:

```
/perplexity-downloader
[paste list of URLs]
```

Or:
> "Download these threads: [URL1, URL2, URL3]"

### Full History Export

Export all threads from your Perplexity account:

```
/perplexity-downloader export all
```

Or:
> "Export all my Perplexity threads"

**Required:** You must be logged into Perplexity.ai. Provide your history page or URL.

## Output Format

### Filename Format

```
[YYMMDD]-[sanitized-title].md
```

Example:
```
260423-what-is-the-best-way-to-learn-japanese.md
```

### Directory Structure

**Single thread:** One `.md` file in `~/perplexity-downloader/outputs/`

**Bulk/History export:** Folder with index + individual thread files:

```
~/perplexity-downloader/outputs/
├── index.md                          # Table of contents
├── 260423-how-to-learn-python.md
├── 260423-best-practices-rest-apis.md
└── 260423-docker-vs-kubernetes.md
```

### Markdown Structure

Each thread file contains:

```markdown
# [Thread Title / First Question]

> Saved from Perplexity.ai
> URL: [original URL]
> Date: [save date]

---

## Turn 1

### Question
[user's question]

### Answer
[AI's response]

#### Sources
1. [Source title](URL)
2. [Source title](URL)

---

## Turn 2
[additional turns if present]
```

## Configuration

No configuration needed. Files are saved to `~/perplexity-downloader/outputs/` automatically.

## Features Explained

### Sequential Processing

Threads are downloaded one at a time, not in parallel. This ensures:
- Predictable progress updates
- Avoids rate limiting
- Maintains request order

During bulk/history export, you'll see:
```
Downloaded 15/42 threads...
```

### Source Preservation

All citations and source links are preserved exactly as found in the original Perplexity thread.

### Multi-turn Support

Handles threads with multiple questions and follow-ups, organizing each turn in the markdown file.

### Index Generation

For bulk and history exports, an `index.md` file is automatically created listing all downloaded threads with dates and links.

## Edge Cases

| Situation | Behavior |
|-----------|----------|
| Thread is private/login-gated | Skill asks you to paste the page manually |
| Single-turn thread | Creates file with just one `## Turn 1` section |
| 10+ turn thread | Processes all turns, notes turn count |
| No sources | Omits `#### Sources` section for that turn |
| Non-English thread | Preserves original language; no translation |
| Rate limiting during download | Pauses 5 seconds between requests |
| Some URLs fail | Downloads succesful ones, reports failures at end |

## Troubleshooting

### "I wasn't able to fetch this thread automatically"

The page may require a login or be access-restricted. Copy the full page text and paste it into the skill—it will parse and format it as Markdown.

### "Found 0 threads in your history"

Your history page may not have fully loaded. Scroll through the Perplexity sidebar to load all threads before copying the page.

### Large exports taking too long

For 100+ threads, consider:
- Exporting by date range (e.g., "last 30 days")
- Exporting in smaller batches
- Checking your internet speed

## Output Location

All files are saved to:
```
~/perplexity-downloader/outputs/
```

You can access them directly from your file manager or terminal:
```bash
open ~/perplexity-downloader/outputs/
# or
ls ~/perplexity-downloader/outputs/
```

## Performance

- **Single thread:** ~2-5 seconds
- **10 threads:** ~30-60 seconds
- **50 threads:** ~5-10 minutes
- **100+ threads:** 15-30 minutes

Times may vary depending on:
- Thread length and complexity
- Internet speed
- System performance

## Support

For issues or feedback:
- Check the edge cases section above
- Verify your Perplexity account is accessible
- Ensure threads are not private/restricted

## License

This skill is part of the claude-custom-skills repository.
