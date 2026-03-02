# RUKH — Jekyll Setup Guide
### rubserhii.github.io

---

## Prerequisites — what you need

- A computer running **macOS** (instructions below assume this; Windows notes at the end)
- **Git** installed — check by running `git --version` in Terminal
- A **GitHub account** at github.com/rubserhii
- The `rukh-site` folder from this project

---

## Step 1 — Install Ruby

Jekyll runs on Ruby. macOS ships with a system Ruby but it's old and
locked down. Use **rbenv** to install a modern version.

Open Terminal and run these commands one at a time:

```bash
# Install Homebrew (if you don't have it)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install rbenv (Ruby version manager)
brew install rbenv ruby-build

# Add rbenv to your shell (for zsh, which is macOS default)
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc

# Install Ruby 3.2
rbenv install 3.2.0
rbenv global 3.2.0

# Confirm it worked — should say 3.2.0
ruby -v
```

---

## Step 2 — Install Jekyll

```bash
gem install jekyll bundler
```

This installs Jekyll and Bundler (the Ruby package manager).
It may take a minute or two.

Confirm:
```bash
jekyll -v
# Should output: jekyll 4.x.x
```

---

## Step 3 — Set up your GitHub repository

1. Go to **github.com** and log in as `rubserhii`
2. Click **New repository** (the + icon, top right)
3. Name it exactly: `rubserhii.github.io`
4. Set it to **Public**
5. Do NOT tick "Add a README" — leave it empty
6. Click **Create repository**

---

## Step 4 — Put the site files on your computer

Move the `rukh-site` folder to wherever you keep projects.
A good place is `~/Projects/rubserhii.github.io`.

```bash
# If you downloaded a zip, unzip and move it:
mv ~/Downloads/rukh-site ~/Projects/rubserhii.github.io

cd ~/Projects/rubserhii.github.io
```

---

## Step 5 — Install the site's dependencies

```bash
# Inside your site folder:
bundle install
```

This reads the `Gemfile` and installs Jekyll and plugins.
You only need to do this once (or when you add new plugins).

---

## Step 6 — Run the site locally

```bash
bundle exec jekyll serve --livereload
```

Now open your browser and go to:
**http://localhost:4000**

You should see your site. The `--livereload` flag means the browser
refreshes automatically whenever you save a file.

To stop the server: press `Ctrl + C` in Terminal.

---

## Step 7 — Connect to GitHub and push

```bash
# Initialise git in your site folder
git init
git add .
git commit -m "Initial commit — Rukh site"

# Connect to your GitHub repo
git remote add origin https://github.com/rubserhii/rubserhii.github.io.git

# Push
git push -u origin main
```

---

## Step 8 — Enable GitHub Pages

1. Go to your repo on GitHub: **github.com/rubserhii/rubserhii.github.io**
2. Click **Settings** (top tab)
3. Click **Pages** (left sidebar)
4. Under "Source", select **Deploy from a branch**
5. Branch: **main** / folder: **/ (root)**
6. Click **Save**

Wait 1–2 minutes, then visit:
**https://rubserhii.github.io**

Your site is live. 🎉

---

## How to add a new Del Sol build log entry

This is your main workflow. It's designed to be as fast as possible.

**1. Create a new file in `_collections/del_sol/`**

Name it with the date and a short slug:
```
2026-03-15-coilover-fitment.md
```

**2. Paste this template at the top:**

```markdown
---
title: "Your entry title here"
date: 2026-03-15
entry_num: 3
tags: [Suspension]
excerpt_text: "One or two sentence summary shown on the homepage."
hero_image: /assets/images/del-sol-entry-003-hero.jpg
---

Write your entry here in plain text.

## A subheading if you want one

More text. Add photos with:

{% raw %}{% include image.html src="/assets/images/your-photo.jpg" caption="Optional caption" %}{% endraw %}
```

**3. Add your photos**

Put photos in `assets/images/`.
Rename them something sensible: `del-sol-entry-003-coilovers.jpg`

**4. Push to GitHub:**

```bash
git add .
git commit -m "Del Sol entry 003 — coilover fitment"
git push
```

GitHub rebuilds your site automatically. Live in ~60 seconds.

---

## Other hobby entries work the same way

| Hobby    | Folder                    | Example filename                        |
|----------|---------------------------|------------------------------------------|
| Del Sol  | `_collections/del_sol/`   | `2026-03-15-coilover-fitment.md`        |
| Cycling  | `_collections/cycling/`   | `2026-04-01-north-shore-loop.md`        |
| FPV      | `_collections/fpv/`       | `2026-04-10-new-5inch-build.md`         |
| Scuba    | `_collections/scuba/`     | `2026-05-03-porteau-cove-dive.md`       |

---

## Adding photos to an entry

**Single photo (hero):**
Add `hero_image: /assets/images/your-photo.jpg` to the front matter.

**Gallery at the bottom of the post:**
```yaml
gallery:
  - /assets/images/photo-a.jpg
  - /assets/images/photo-b.jpg
  - /assets/images/photo-c.jpg
```

**Inline photo inside the text:**
```markdown
![Description of photo](/assets/images/photo.jpg)
```

---

## Recommended image workflow

Phone photos are large. Before pushing, resize them so the site stays fast.

Install `imagemagick`:
```bash
brew install imagemagick
```

Resize a photo to max 1800px wide:
```bash
magick input.jpg -resize 1800x1800\> -quality 82 output.jpg
```

Or batch resize everything in a folder:
```bash
for f in *.jpg; do
  magick "$f" -resize 1800x1800\> -quality 82 "resized_$f"
done
```

---

## Updating the spec plate

The car spec block on the homepage is hardcoded in `index.html`.
Find the "SPEC PLATE" section and edit the values directly.

---

## Windows setup notes

If you're on Windows, use **WSL2** (Windows Subsystem for Linux):

1. Open PowerShell as Administrator:
   ```
   wsl --install
   ```
2. Restart your computer
3. Open the Ubuntu app from the Start menu
4. Follow the Linux/macOS instructions above inside the WSL terminal

---

## File structure reference

```
rubserhii.github.io/
│
├── _config.yml          ← Site settings (title, URL, collections)
├── Gemfile              ← Ruby dependencies
├── index.html           ← Homepage
├── del-sol.html         ← Del Sol index page
│
├── _layouts/
│   ├── default.html     ← Base HTML wrapper
│   └── entry.html       ← Individual post layout
│
├── _includes/
│   ├── header.html      ← Navigation
│   ├── footer.html      ← Footer
│   └── scripts.html     ← JS (scroll reveal, etc.)
│
├── _sass/
│   ├── _tokens.scss     ← Colours and fonts ← EDIT THIS to retheme
│   ├── _base.scss       ← Reset, typography, Markdown styles
│   ├── _header.scss
│   ├── _hero.scss
│   ├── _components.scss ← Cards, build log, hobbies, footer
│   └── _entry.scss      ← Individual post page styles
│
├── assets/
│   ├── css/main.scss    ← CSS entry point (don't edit this)
│   └── images/          ← Put all your photos here
│
└── _collections/
    ├── del_sol/         ← Del Sol build log entries (.md files)
    ├── cycling/         ← Cycling/bikepacking entries
    ├── fpv/             ← FPV drone entries
    └── scuba/           ← Scuba entries
```

---

*That's everything. The hardest part is the first setup — after that,
adding a new entry is: write Markdown → add photo → git push.*
