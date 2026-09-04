# OctoFlow 3.8 PRO – Smart GitHub Client

**OctoFlow** is a powerful, client‑side GitHub repository and file manager. It allows you to manage multiple GitHub accounts, browse repositories, edit files (with rename support), upload/download ZIPs, and copy/move files across repos – all directly from your browser, without a backend server.

[![Version](https://img.shields.io/badge/version-3.8_PRO-blue.svg)](https://github.com/buildsaurora-collab/File-manager)
[![Made with JavaScript](https://img.shields.io/badge/Made%20with-JavaScript-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---

## ✨ Features

- **Multi‑Account Support**: Add multiple GitHub Personal Access Tokens and switch accounts instantly.
- **Repository Management**:
  - Create, rename, delete, or toggle visibility (Public/Private) of repositories.
  - Optimistic UI updates – see changes instantly.
- **File Explorer**:
  - Browse files and folders with breadcrumb navigation.
  - Download any folder as a ZIP archive.
  - Wipe entire folders.
- **Smart File Editor**:
  - Edit file content (with secret detection).
  - **Rename files and change extensions** directly from the editor header.
- **Upload & Extract**:
  - Upload individual files.
  - Upload and auto‑extract ZIP archives.
- **Clipboard**:
  - Copy or move files/folders between repositories (even across accounts).
- **Intelligent Caching**:
  - Optimistic UI updates + background polling for GitHub’s eventual consistency.
  - Cache‑busting query parameters to bypass CDN caches.

---

## 🚀 Getting Started

### 1. Generate a GitHub Personal Access Token

To use OctoFlow, you need a **GitHub Personal Access Token (classic)** with the right permissions.

1. Go to **GitHub Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**.
2. Click **Generate new token (classic)**.
3. Give it a descriptive name (e.g., `OctoFlow`).
4. Select the following **scopes**:
   - `repo` (full control of private repositories) – **required** for all operations.
   - If you only need public repos, you can use `public_repo` instead.
5. Click **Generate token** and **copy it immediately** (you won’t see it again).

> **⚠️ Security Note**  
> Your token is stored **locally in your browser** (IndexedDB) and is **never** sent to any server except GitHub’s official API. Treat it like a password – do not share it.

---

### 2. Add the Token to OctoFlow

1. Open the `Octaflow.html` file in your browser.
2. Click the **Tokens** button in the top‑right corner.
3. Paste your token into the input field.
4. Check **“Session only”** if you don’t want the token to persist after closing the browser.
5. Click **Save & Authenticate**.
6. Your account will appear on the Root page. Click it to see your repositories.

> **💡 Tip**: You can add multiple tokens to switch between different GitHub accounts.

---

### 3. Managing Repositories

| Action | How to do it |
|--------|--------------|
| **Create** | Click the **New Repo** button, enter a name, and confirm. |
| **Rename** | Click the ✏️ (pen) icon on a repo card. |
| **Toggle Privacy** | Click the 🔒 (lock) icon to switch between Public/Private. |
| **Delete** | Click the 🗑️ (trash) icon and confirm. |
| **Sync** | If changes aren’t visible immediately, click the **Sync** button to refresh the list. |

---

### 4. Browsing & Editing Files

- Click a repository to open the File Explorer.
- Click a **folder** to navigate into it.
- Click a **file** to open the Editor.

#### Renaming a File (New Feature!)
1. Open a file in the editor.
2. **Click on the filename** displayed in the header (e.g., `index.html`).
3. Edit the name – you can change both the name and the extension (e.g., `style.css` → `main.scss`).
4. Press **Enter** or click outside the input field to save the new name.
5. Click **Commit** – OctoFlow will create the new file and delete the old one automatically.

---

### 5. Using the Clipboard (Copy / Move)

- In the File Explorer, hover over any file or folder.
- Click the **Copy** (📋) or **Move** (✂️) icon.
- Navigate to another folder or repository.
- Click the **Paste** button that appears on the toolbar – the item will be copied or moved.

---

### 6. Upload & Extract ZIP

- Click the **Actions** menu (➕) in the File Explorer.
- Select **Upload & Extract ZIP** – choose a `.zip` file, and OctoFlow will extract its contents into the current folder.
- Or choose **Upload File(s)** to upload individual files.

---

## ⚖️ GitHub API Rate Limits & Caching

OctoFlow works directly with the **GitHub REST API**. Here’s what you need to know:

| Limit | Details |
|-------|---------|
| **Authenticated Requests** | 5,000 requests per hour per token. |
| **Cache‑Busting** | All requests append a timestamp (`?t=...`) to bypass CDN caches. |
| **Optimistic UI** | The UI updates instantly when you create, rename, or delete a repo – even before GitHub’s servers confirm the change. |
| **Background Polling** | After a mutation, OctoFlow polls GitHub briefly to confirm the change. This may use a few extra API calls. |
| **Repo Cache** | When you open a repository, OctoFlow fetches **all file contents** at once. This is fast for small/medium repos, but large repos (1,000+ files) may consume many requests and take time. |

> **💡 To avoid hitting rate limits**:
> - Use the **Sync** button sparingly.
> - For large repositories, consider opening fewer files at once.
> - If you hit a limit, wait an hour or switch to another token.

---

## 🛡️ Privacy & Data Safety

- **All data stays in your browser** – tokens, repository lists, and cached files are stored locally in IndexedDB.
- **No analytics, no tracking, no external servers** – all API calls go directly to `api.github.com`.
- **Session‑only tokens** are never written to disk – they are cleared when you close the tab.

---

## ❓ Troubleshooting

| Issue | Suggested Fix |
|-------|---------------|
| **“Nothing is visible” (blank page)** | Open the browser console (`F12` or `chrome://inspect`) and check for errors. Ensure you’re opening the file via a web server (e.g., `http://127.0.0.1:...`) – some browsers block `fetch()` from `file://` URLs. |
| **Repository list doesn’t update immediately** | Click the **Sync** button. GitHub’s internal databases can take a few seconds to reflect changes – this is normal. |
| **File rename fails with “already exists”** | Choose a different name – GitHub does not allow overwriting files via rename. |
| **“Rate limit exceeded”** | Wait an hour, or add a second token and switch accounts. |

---

## 📥 Download the App

To run OctoFlow locally, download the `Octaflow.html` file.

**Option 1 – Direct Download (click the button):**  
GitHub may open the raw file in your browser. If that happens, use your browser’s **“Save as”** (Ctrl+S / Cmd+S) or right‑click the button and select **“Save link as…“**.

<p align="center">
  <a href="https://raw.githubusercontent.com/buildsaurora-collab/File-manager/main/Octaflow.html" download="Octaflow.html" style="display: inline-block; padding: 14px 28px; background-color: #238636; color: white; text-decoration: none; border-radius: 8px; font-weight: bold; font-size: 1.1rem;">
    ⬇️ Download Octaflow.html
  </a>
</p>

**Option 2 – Right‑click the link above** and choose “Save link as…” to save the file directly.

**Option 3 – Command line (curl/wget):**  
```bash
curl -O https://raw.githubusercontent.com/buildsaurora-collab/File-manager/main/Octaflow.html
# or
wget https://raw.githubusercontent.com/buildsaurora-collab/File-manager/main/Octaflow.html
```

Once downloaded, open `Octaflow.html` in your browser.

---

## 📜 License

This project is provided as‑is for personal and educational use. Use at your own risk.

---

## 🙌 Acknowledgements

Built with:
- [Tailwind CSS](https://tailwindcss.com/)
- [Font Awesome](https://fontawesome.com/)
- [JSZip](https://stuk.github.io/jszip/)
- [GitHub REST API](https://docs.github.com/en/rest)

---

**Enjoy managing your GitHub repos with OctoFlow!** 🚀

## Updates
**It's Still in development Phase multiple updates appears so look out for it .
Current version is octaflow 3.8 pro .
we will launch multiple new updates
Thank you Aurora Codes**
