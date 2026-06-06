# Seek Construction LLC — website

A fast, single-page marketing site for Seek Construction LLC, plus a built-in
**Site Editor** so the owner can update content and photos without touching code.

- **Live site:** `https://rhendricksontu.github.io/seekconstruction/`
- **Site Editor:** `https://rhendricksontu.github.io/seekconstruction/admin.html`

## How it works

| File | Purpose |
|------|---------|
| `index.html` | The website. On load it fetches `data.json` and renders every section from it. |
| `data.json` | **All editable content** (text, lists, image references). This is the file the editor saves. |
| `admin.html` | The Site Editor. A friendly, password-protected page that edits `data.json` and uploads photos, committing straight to this repo. |
| `images/` | Photos. The editor uploads here automatically (`images/` for hero & gallery, `images/projects/` for project photos). |

There is **no server and no build step.** The editor talks to the GitHub API
directly from the browser. When the owner clicks **Save & publish**, it commits
the change, GitHub Pages rebuilds, and the live site updates in about a minute.

If `data.json` is ever missing, `index.html` falls back to the seed copy
embedded inside it, so the site never goes blank.

---

## For the owner — editing the site

1. Open the **Site Editor** bookmark.
2. Enter your **passcode**.
3. Use the tabs (Hero, Services, Projects, Gallery, etc.) to change text, add or
   remove projects, reorder things, and upload photos (drag a photo onto
   **Upload photo** — it's resized automatically).
4. Click **Save & publish**. Your changes go live in about a minute. Refresh the
   site to see them.

That's it — no token, no GitHub, no code.

---

## For the maintainer — one-time setup per device

The editor needs a GitHub **access token** the first time it's used on a given
computer/browser. The token is encrypted with the passcode and stored only on
that device — it is never put in the code or the repo.

### 1. Create a fine-grained personal access token

1. Go to **GitHub → Settings → Developer settings → Fine-grained tokens →
   Generate new token** (https://github.com/settings/tokens?type=beta).
2. **Resource owner:** `rhendricksontu`
3. **Repository access:** *Only select repositories* → **seekconstruction**.
4. **Permissions → Repository permissions → Contents → Read and write.**
   (Leave everything else as "No access".)
5. Set an expiration (e.g. 1 year — you'll re-issue it when it lapses).
6. Generate, and **copy the token** (`github_pat_…`). You won't see it again.

> Scope is deliberately tiny: this token can only read/write files in this one
> repo. Worst case if it leaks, someone could edit this website — nothing else.

### 2. Connect the editor

1. Open `admin.html` (the published https address — Web Crypto requires https).
2. On the **one-time setup** screen, paste the token, confirm owner/repo, and
   **create a passcode**.
3. It verifies access and drops you into the editor.

### 3. Hand off

Give the owner the **Site Editor URL** and the **passcode**. They never see the
token. To set them up on their own laptop, repeat step 2 there once (you'll need
the token again).

To disconnect a device, use **"Reset this device"** on the login screen — it
clears the saved token locally and does not affect the website.

---

## Notes & limitations

- The contact form's "Send" button currently opens the visitor's email app
  (`mailto:`) — it does **not** capture the typed Name/Phone/Details fields.
  Wiring it to a real form service (e.g. Formspree) is a worthwhile follow-up.
- Project percentage stats ("50% Public", etc.) are **calculated automatically**
  from the project list — no need to edit them by hand.
- Editing `data.json` by hand (or via GitHub's web editor) also works; the
  editor just makes it safer.
