# DevLinks — Developer Portfolio Link-in-Bio Builder

> Build your developer profile page in minutes. Export clean HTML. Deploy anywhere.

![DevLinks](https://img.shields.io/badge/DevLinks-v1.0-39e07a?style=for-the-badge&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/dependencies-zero-39e07a?style=flat)

---

## 🎯 What Is This?

**DevLinks** is a browser-based visual builder for creating a personal developer link-in-bio profile page — similar to Linktree, but built specifically for developers and fully self-hostable.

Fill in your details on the left. See your card update live on the right. Export a clean, self-contained `index.html` and deploy it anywhere — GitHub Pages, Netlify, or even send it as a file.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🖊️ **Visual Editor** | Split-pane layout — edit on the left, see changes instantly on the right |
| 🔗 **11 Link Types** | GitHub, LinkedIn, Portfolio, Resume, Twitter, Instagram, Email, YouTube, Project, Blog, Custom |
| 🎨 **6 Themes** | Terminal (green), Midnight (blue), Ember (orange), Arctic (cyan), Rose (pink), Slate (grey) |
| 📤 **One-Click Export** | Downloads a complete, self-contained `index.html` — no dependencies, just works |
| 💾 **Auto-Save** | All edits persisted to `localStorage` — your data survives page refreshes |
| ⌨️ **Keyboard Shortcut** | `Ctrl/Cmd + S` to open export modal instantly |

---

## 🚀 How to Use

### Option 1 — Use the Builder
1. Open `index.html` in any browser (double-click — no server needed)
2. Fill in your **profile info** (name, role, bio, skills, location)
3. Add your **links** (GitHub, LinkedIn, portfolio, etc.)
4. Pick a **colour theme**
5. Click **export →** and download your profile page

### Option 2 — Deploy the Builder to GitHub Pages
1. Fork or clone this repo
2. Go to **Settings → Pages → Source: main branch / root**
3. Share the builder URL so others can use it too

### Deploying Your Exported Profile Page
After exporting, upload the downloaded `index.html` to:
- **GitHub Pages** — create a repo named `username.github.io`, upload the file as `index.html`
- **Netlify** — drag and drop the file at [netlify.com/drop](https://app.netlify.com/drop)
- **Any static host** — it's a single HTML file with zero dependencies

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 (semantic, single-file) |
| Styling | CSS3 — custom properties, grid, flexbox, animations |
| Logic | Vanilla JavaScript (ES6+) — no frameworks |
| Persistence | `localStorage` — auto-saves all state |
| Export | Blob API + `<a download>` — generates and downloads HTML file |

**Zero dependencies. Zero npm. Zero build step.**

---

## 📁 Project Structure

```
devlinks/
├── index.html    ← Entire builder: editor + preview + export engine in one file
└── README.md
```

---

## ⚙️ How It Works

### 1. Reactive State → Live Preview
All form inputs update a central `state` object. Every change triggers `renderPreview()`, which rebuilds the profile card DOM using the current theme and data — giving instant visual feedback.

```javascript
// Single state object drives everything
let state = {
  name:'', role:'', emoji:'', bio:'', tags:'', location:'', status:'',
  links:[], theme:'terminal', layout:'centered'
};

// Any input change → update state → re-render preview
el.addEventListener('input', () => {
  state[key] = el.value;
  saveState();       // persist to localStorage
  renderPreview();   // rebuild preview DOM
});
```

### 2. Theme System
Six complete themes, each defined as a colour token object. Applied to both the live preview and the exported HTML via inline CSS variable injection.

```javascript
const THEMES = {
  terminal: {
    bg:'#0a0e0a', surface:'#111811', accent:'#39e07a',
    text:'#c8e8d0', muted:'rgba(57,224,122,0.45)', ...
  },
  midnight: { accent:'#6c8ef5', ... },
  ember:    { accent:'#f07030', ... },
  // ...
};
```

### 3. Export Engine
On export, `generateExportHTML()` builds a fully self-contained HTML string — with all profile data, links, and theme tokens inlined as CSS variables. The Blob API converts this string to a downloadable file.

```javascript
function generateExportHTML() {
  const t = THEMES[state.theme];
  // Inlines all data + theme as a complete standalone HTML page
  return `<!DOCTYPE html>...<style>body{background:${t.bg}...}</style>...`;
}

// Download via Blob API
const blob = new Blob([generateExportHTML()], { type:'text/html' });
const a = document.createElement('a');
a.href = URL.createObjectURL(blob);
a.download = 'devlinks.html';
a.click();
```

### 4. localStorage Auto-Save
State is serialized to `localStorage` on every change and rehydrated on page load — so no work is ever lost on a refresh.

---

## 🎨 Design

- **Terminal aesthetic** — monospace font, scanline CSS overlay, traffic-light dots, green-on-dark palette
- **Split-pane layout** using CSS Grid — editor left, live preview right
- **Tab system** inspired by code editors — `profile.json`, `links.json`, `theme.css`
- **Forced dark theme** — no flash of white, no CDN dependencies, no layout shift
- **CSS custom properties** for a consistent design system throughout

---

## 🔮 Possible Extensions

- QR code generation for the profile URL
- Custom domain setup guide
- Analytics integration (Plausible or Fathom)
- More layout templates (horizontal card, minimal, dark glass)
- Image upload support for avatar (FileReader API)
- Shareable URL via encoded state in URL hash

---

## 👤 Author

Built by **Bhavya** — portfolio project demonstrating frontend engineering, DOM architecture, and UI/UX design skills.

---

## 📄 License

MIT — free to use, modify, and distribute.
