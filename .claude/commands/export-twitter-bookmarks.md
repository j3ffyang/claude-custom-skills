---
description: Export X/Twitter bookmarks from bookmarks.json into Markdown files
---

Export my X/Twitter bookmarks to Markdown using the twitter-bookmarks-exporter skill.

Follow these steps exactly:

1. **Check for bookmarks.json** — verify the file exists at `twitter-bookmarks-exporter/bookmarks.json`. If it is missing, stop and tell the user:
   > `bookmarks.json` not found. To capture it:
   > 1. Open https://x.com/i/bookmarks in your browser
   > 2. Open DevTools (F12) → Network tab → filter requests by "Bookmarks"
   > 3. Scroll through your bookmarks page to trigger the API requests
   > 4. Right-click the Bookmarks request → Copy → Copy Response
   > 5. Save the copied JSON as `bookmarks.json` inside the `twitter-bookmarks-exporter/` folder, then run `/export-twitter-bookmarks` again

2. **Run the exporter** — execute `python twitter-bookmarks-exporter/scripts/main.py` and show its output.

3. **Verify output** — list the files created in `twitter-bookmarks-exporter/output/bookmarks/` and count them.

4. **Report results** — summarize: total bookmarks exported, output directory path, and show the first 5 filenames as a sample.
