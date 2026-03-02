# RUKH — Jekyll Setup Guide
### rubserhii.github.io

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
