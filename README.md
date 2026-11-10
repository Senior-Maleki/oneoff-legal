# One Off — public legal pages

This folder is the source for the public site that backs the **One Off Desktop**
OAuth application. Google will not let an External app leave *Testing* until its
Branding page has a **home page**, a **privacy policy**, and a **matching
authorized domain**. The greyed-out **Publish app** button is that requirement.

Three files, no build step, no dependencies:

| File | What it is |
|---|---|
| `index.html` | Home page — describes the app and the channel, links to both legal pages |
| `privacy.html` | Privacy policy — the two scopes, what is stored, how to revoke |
| `terms.html` | Terms of service |

---

## ⚠️ These URLs must NOT be part of `apex-projects`

`apex-projects` is **private** and contains client material. A Google authorized
domain is public, so the legal pages must live in their own **public** repo with
nothing else in it. Do not publish this folder from `apex-projects`.

---

## Setup (about 4 minutes, done once, in the browser)

### 1. Create the public repo

1. Go to <https://github.com/new>
2. **Repository name:** `oneoff-legal`
3. **Public** ← important
4. Do **not** initialise with a README (we already have one)
5. **Create repository**

### 2. Push these three files

From the folder that contains this README:

```bash
cd oneoff-legal
git init -b main
git add index.html privacy.html terms.html README.md
git commit -m "One Off: OAuth app home page, privacy policy, terms"
git remote add origin https://github.com/<YOUR-USERNAME>/oneoff-legal.git
git push -u origin main
```

> If you already pushed from inside `apex-projects`, skip this — the files are
> already there.

### 3. Turn on GitHub Pages

1. Repo → **Settings** → **Pages** (left sidebar)
2. **Source:** `Deploy from a branch`
3. **Branch:** `main` · **Folder:** `/ (root)` → **Save**
4. Wait ~1 minute. The page will show:
   **"Your site is live at `https://<YOUR-USERNAME>.github.io/oneoff-legal/`"**

### 4. Check it before telling Google about it

Open these three in a private/incognito window:

```
https://<YOUR-USERNAME>.github.io/oneoff-legal/
https://<YOUR-USERNAME>.github.io/oneoff-legal/privacy.html
https://<YOUR-USERNAME>.github.io/oneoff-legal/terms.html
```

All three must load **without logging in to GitHub**. If they ask for a login,
the repo is private — go back to step 1.

⚠️ **GitHub Pages URLs are case-sensitive after the domain.** Your username is
`Senior-Maleki` with a capital S. Test the exact URL you are going to paste into
Google, character for character.

### 5. Paste into Google Auth Platform → Branding

In the **App domain** section:

| Google field | What to paste |
|---|---|
| **Application home page** | `https://senior-maleki.github.io/oneoff-legal/` |
| **Application privacy policy link** | `https://senior-maleki.github.io/oneoff-legal/privacy.html` |
| **Application terms of service link** | `https://senior-maleki.github.io/oneoff-legal/terms.html` |
| **Authorized domains** → ADD DOMAIN | `senior-maleki.github.io` |

> **Add the authorized domain FIRST.** Google rejects the three links until their
> domain is on the authorized list. Then **SAVE**.

Then go back to **Audience** — **Publish app** is now enabled.

---

## What to do when it still refuses

| Message | Cause | Fix |
|---|---|---|
| `Missing domain: senior-maleki.github.io` | Domain not added before the links | Add the domain, save, then re-save the links |
| Links save but Publish stays grey | One of the three links 404s | Open all three in incognito; a typo in a path is the usual culprit |
| `home page cannot be only a login page` | Wrong URL pasted | You pasted a repo URL instead of the Pages URL |
| Publish enabled but consent screen shows the old name | Normal | App name and logo only appear after Google's brand verification; the app stays usable meanwhile |

## Why a separate repo, and not a domain

The brand has no domain and will not get one. A GitHub Pages URL is a real,
publicly reachable, HTTPS URL on a domain Google already accepts, and it costs
nothing. The only requirement Google actually enforces is that the privacy
policy sits on the same domain as the home page and is linked from it — all
three of these files satisfy that trivially.
