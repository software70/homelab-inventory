# Saff's Homelab Inventory

A live hardware spec dashboard, hosted on GitHub Pages.

## 🚀 First-time setup

1. Create a new **public** GitHub repo, e.g. `homelab-inventory`.
2. Upload these two files to the repo root:
   - `index.html`
   - `data.json`
3. Go to **Settings → Pages**.
4. Under "Build and deployment", set **Source: Deploy from a branch**.
5. Branch: `main`, folder: `/ (root)` → **Save**.
6. Wait ~1 minute. Your dashboard will be live at:
   `https://<your-username>.github.io/homelab-inventory/`

That's it — no build step, no dependencies, no server.

## ✏️ Making changes (the part you'll actually use)

You only ever need to edit **`data.json`**. Never touch `index.html` again.

1. On GitHub, open `data.json` in your repo.
2. Click the pencil icon (Edit this file).
3. Change a value, e.g. update RAM, add a new tag, flip a `"status"`.
4. Scroll down → **Commit changes**.
5. Refresh your GitHub Pages URL — the change is live within seconds (GitHub Pages caches lightly, so a hard refresh `Ctrl+Shift+R` may be needed).

## 📋 Editing cheatsheet

**Change a spec value**
```json
"CPU": "Ryzen 9 3950X"
```
Just edit the text on the right.

**Add a new spec field to a device**
```json
"specs": {
  "CPU": "Ryzen 5 5600G",
  "Storage": "12-disk ZFS array",
  "Firmware": "BIOS 2.40"   <-- new line, remember the comma above
}
```

**Change device status (controls the LED dot)**
```json
"status": "on"     // green pulsing LED
"status": "off"    // grey LED
"status": "plan"   // yellow pulsing LED
```

**Add a brand new NAS / device**
Copy an existing block inside the `"nas"` array (or `"workstation"` / `"planned"`), paste it as a new entry, and edit the values. Example:
```json
"nas": [
  { ...existing primary nas... },
  { ...existing secondary nas... },
  {
    "name": "Tertiary NAS",
    "subtitle": "Cold archive",
    "os": "TrueNAS SCALE",
    "osType": "truenas",
    "status": "on",
    "specs": {
      "CPU": "Ryzen 5 5600G",
      "RAM": "32GB DDR4"
    },
    "accents": { "CPU": "blue", "RAM": "purple" },
    "tags": ["Archive"]
  }
]
```

**Add/remove a switch or internet device**
Edit the `"switches"` or `"internet"` arrays the same way — copy a block, edit, save.

**Update the 3-2-1 strategy checklist**
Edit the `"strategy.items"` array — each item has an `icon`, `bold` label, and `text`.

## ⚠️ Common mistake: broken JSON

JSON is strict about commas and quotes. If the page shows a "Failed to load inventory data" error:
- Check you didn't leave a trailing comma after the last item in a list `[ ... , ]` ❌
- Check every `{` has a matching `}`
- Paste your `data.json` into [jsonlint.com](https://jsonlint.com) to validate before committing — catches errors instantly.

## 🎨 Available accent colors
For `accents` and `speedColor` fields: `blue`, `green`, `orange`, `yellow`, `purple`, `muted`.

## 🔒 Note on visibility
This repo needs to be **public** for free GitHub Pages hosting, meaning your hardware specs are visible to anyone with the link. If you'd rather keep it private, GitHub Pages on a private repo requires GitHub Pro/Team, or you could self-host this same `index.html` + `data.json` pair on your own NAS via Docker/nginx instead.
